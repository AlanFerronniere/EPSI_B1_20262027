# Projet BDD — Système de Suivi Écologique et d'Échantillonnage Côtier
## Cahier des Charges & Consignes d'Évaluation
**Commanditaire :** Institut Français de Recherche Océanologique (IFROCEAN)  
**Formation :** Bachelor 1 (B1) — EPSI  
**Module :** Conception de Bases de Données & Modélisation (UML / Merise / MySQL & MariaDB)  
**Modalités :** Travail en équipe de 2 à 3 étudiants maximum  

---

## 1. Contexte & Présentation du Projet

L'**IFROCEAN** (*Institut Français de Recherche Océanologique*) coordonne des programmes d'observation et de veille écologique sur le littoral atlantique et de la Manche. Dans le cadre de ses campagnes scientifiques (telles que le programme européen *Natura 2015*), l'institut mobilise des équipes de préleveurs et d'étudiants bénévoles pour réaliser des inventaires faunistiques sur les zones de balancement des marées (les **estrans**).

Actuellement, les données de terrain sont recueillies sur des formulaires papier puis ressaisies manuellement dans des tableurs disparates. Ce fonctionnement engendre des retards de traitement, des erreurs de saisie sur les noms d'espèces marines et rend les calculs statistiques d'extrapolation très fastidieux.

Pour moderniser sa chaîne de collecte, l'IFROCEAN engage la refonte complète de son système d'information.  
Le projet global se déroule en deux phases :
1. **Phase 1 (présente épreuve) :** Modélisation et implémentation de la **Base de Données relationnelle sous MySQL / MariaDB**.
2. **Phase 2 (ultérieure) :** Développement de l'**application web en PHP** interconnectée à cette base de données et déploiement sur serveur web.

---

## 2. Spécifications Fonctionnelles & Règles Métier

### 2.1. Gestion du référentiel géographique (Plages et Estrans)
L'administrateur du système doit pouvoir enregistrer la liste des plages ouvertes aux campagnes scientifiques.
* Pour chaque plage, le système conserve :
  * Un identifiant unique.
  * Le nom usuel de la plage (ex. *Plage de Pentrez*).
  * La commune de rattachement (ex. *Saint-Nic*).
  * Le département (ex. *Finistère - 29*).
  * La **superficie totale de l'estran étudié**, exprimée en mètres carrés ($m^2$). *Remarque : cette surface correspond à la zone intertidale échantillonnable et non à la totalité de la commune.*

### 2.2. Gestion des Campagnes et Études scientifiques
L'institut organise ses prélèvements sous forme d'**études** (ou campagnes d'observation).
* Une étude est identifiée par un code ou un titre officiel (ex. *Natura 2015*, *Observatoire Littoral 2026*), une date ou année de lancement et un descriptif de mission.
* Une étude porte sur un **ensemble de plages** prédéfinies. Une même plage peut être suivie dans plusieurs études distinctes au fil des années.

### 2.3. Référentiel des Espèces Marines (Lutte anti-fautes de frappe)
Sur le terrain, la saisie libre des noms d'espèces vivantes conduit à de multiples coquilles (ex. *Hediste diversicolor* orthographié avec une faute), ce qui fausse les regroupements statistiques.
* Le système doit intégrer un **référentiel d'espèces** (nom scientifique binomial en latin, nom vernaculaire / commun éventuel, classe ou embranchement biologique).
* Les équipes de terrain doivent sélectionner l'espèce parmi cette liste contrôlée. Le modèle de données doit garantir l'unicité et la cohérence de ce catalogue.

### 2.4. Sessions de prélèvement & Délimitation des Zones
Sur une plage donnée et dans le cadre d'une étude, des équipes d'étudiants bénévoles se déploient à marée basse :
* Chaque session/intervention terrain consigne :
  * L'étude concernée.
  * La plage étudiée.
  * La date de la sortie de prélèvement.
  * Le nombre de préleveurs ayant constitué l'équipe de comptage.
* **Délimitation géométrique de la zone (quadrilatère) :**
  * Les étudiants tracent un quadrilatère représentatif de la zone médiolittorale.
  * Les 4 sommets (points d'angle $A, B, C, D$) sont relevés au GPS (coordonnées de latitude et longitude).
  * *Règle géométrique :* Le polygone formé ne doit pas être croisé.
  * La surface réelle étudiée (en $m^2$) de la zone doit être stockée ou calculable à partir de ces sommets.

### 2.5. Comptage des individus par Zone
Dans chaque zone délimitée, l'équipe effectue le comptage des spécimens vivants :
* Pour chaque espèce observée dans la zone, on enregistre le nombre d'individus dénombrés (valeur entière positive).
* Une espèce non observée dans la zone n'est pas saisie (ou a un effectif nul).
* Une même espèce ne peut être saisie qu'une seule fois au sein d'une même zone.

### 2.6. Restitutions & Calculs Statistiques attendus
La base de données doit être capable de fournir, par requêtage SQL, les synthèses suivantes :
1. **À l'échelle de chaque plage :**
   * Le nombre total d'espèces distinctes rencontrées.
   * La **densité** de chaque espèce sur les surfaces effectivement échantillonnées :  
     $$\text{Densité (ind/m}^2\text{)} = \frac{\sum \text{Nombre d'individus de l'espèce}}{\sum \text{Surface des zones de prélèvement de la plage}}$$
   * La **population totale estimée** de chaque espèce sur l'estran (par extrapolation) :  
     $$\text{Population extrapolée} = \text{Densité} \times \text{Superficie totale de l'estran}$$
2. **À l'échelle de l'étude complète (toutes plages confondues) :**
   * Le nombre global d'espèces identifiées.
   * La population cumulée extrapolée pour chaque espèce sur l'ensemble des estrans étudiés.
   * La densité moyenne globale pour chaque espèce.

---

## 3. Travail Demandé & Livrables

Le travail s'effectue par groupe de **2 à 3 étudiants maximum**.

### Livrable 1 : Modélisation Conceptuelle (Schéma UML)
* Un **diagramme de classes UML** (ou MCD Merise formalisé sous forme de classes UML) modélisant l'intégralité du domaine métier :
  * Classes avec leurs attributs typés.
  * Identification claire des identifiants / clés candidates.
  * Associations avec leurs cardinalités (multiplicités `0..1`, `1..1`, `0..*`, `1..*`).
  * Justification écrite synthétique des choix de modélisation (notamment la gestion des 4 points GPS et la liaison Étude / Plage / Prélèvement).

### Livrable 2 : Schéma Relationnel de la Base de Données (Diagramme MLD)
* Le **schéma relationnel** (MLD) dérivé des règles de passage de l'UML vers le relationnel :
  * Tables normalisées (respect impératif de la 3ème Forme Normale - 3NF).
  * Clés primaires (`PK`) soulignées.
  * Clés étrangères (`FK`) préfixées ou fléchées vers les tables de référence.
  * Définition précise des types SQL MySQL envisagés pour chaque colonne (formats GPS, entiers, décimaux, chaînes).

### Livrable 3 : Script SQL MySQL / MariaDB Complet (`.sql`)
Un fichier script exécutable sous **MySQL / MariaDB** (compatible phpMyAdmin, MySQL Workbench, XAMPP / Laragon / Docker) contenant :
1. **Création du schéma (DDL) :**
   * Instruction `CREATE DATABASE` et `CREATE TABLE` avec moteur `ENGINE=InnoDB` et jeu de caractères `utf8mb4`.
   * Contraintes de clés primaires (`PRIMARY KEY`) et d'intégrité référentielle (`FOREIGN KEY`) avec options de cascade appropriées.
   * Contraintes de validation (`CHECK` pour entiers/surfaces positifs, `NOT NULL`, `UNIQUE` si nécessaire).
2. **Jeu d'essai complet (DML) :**
   * Insertion de données de test cohérentes et réalistes reprenant le cas d'étude du sujet :
     * Au moins 2 études (dont *Natura 2015*).
     * Au moins 2 plages (dont la *Plage de Pentrez* à Saint-Nic avec son estran de $325\,000\text{ m}^2$).
     * Au moins 5 espèces marines réelles (*Hediste diversicolor*, *Arenicola marina*, *Amblyosyllis formosa*, etc.).
     * Au moins 3 zones de prélèvement distinctes avec leurs coordonnées GPS.
     * Des relevés de comptage réalistes.
3. **Requêtes SQL d'exploitation :**
   * **Requête A :** Liste de tous les prélèvements d'une étude donnée avec nom de plage, date et nombre de préleveurs.
   * **Requête B :** Récapitulatif du nombre d'individus comptés par espèce pour une zone donnée.
   * **Requête C :** Calcul de la densité (nb/m²) et de la population extrapolée de chaque espèce sur la plage de Pentrez.
   * **Requête D :** Synthèse globale de l'étude affichant pour chaque espèce le nombre total d'individus comptés et la population totale extrapolée sur l'ensemble des plages de l'étude.

---

## 4. Modalités de Rendu

//TODO

---

## 5. Barème d'Évaluation (sur 20 points)

| Critère                                             | Description                                                                                                                                                              | Points  |
| :-------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-----: |
| **Compréhension Métier & Analyse**                  | Respect fidèle des exigences du cahier des charges IFROCEAN, identification correcte des règles métier et entités du système.                                            | **/ 3** |
| **Modélisation UML (Livrable 1)**                   | Justesse du diagramme de classes, cohérence des attributs et rigueur des multiplicités/cardinalités.                                                                     | **/ 5** |
| **Schéma Relationnel MLD (Livrable 2)**             | Respect des règles de passage UML $\rightarrow$ Relationnel, gestion correcte des tables, clés primaires et étrangères.                                                  | **/ 4** |
| **Script DDL MySQL (Livrable 3.1)**                 | Qualité du code SQL, moteur InnoDB, choix rigoureux des types (`DECIMAL`, `VARCHAR`, `INT`, `GEOMETRY` ou coordonnées), contraintes d'intégrité (`PK`, `FK`, `DEFAULT`). | **/ 4** |
| **Jeu de Test & Requêtes SQL (Livrable 3.2 & 3.3)** | Données de test cohérentes avec l'exemple Pentrez, validité des requêtes SQL de calcul statistique (agrégations, densités, extrapolations avec jointures).               | **/ 4** |
| **Bonus / Soin du rendu**                           | Propreté du code SQL (indentation, commentaires), clarté de la documentation, prise en compte élégante des coordonnées géographiques.                                    | **+ 1** |
