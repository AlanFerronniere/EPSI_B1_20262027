# ÉVALUATION PRATIQUE : INTÉGRATION & DÉBOGAGE WEB

**École :** EPSI — Année B1 (2026-2027)  
**Module :** Développement Web — HTML5 & CSS  
**Barème total :** / 20 points  

---

## Mise en situation professionnelle

Vous venez d'arriver en stage au sein d'une agence web. Vous devez finaliser en urgence la page d'un blog animalier : **« FélinPourL'Autre »**.

Le développeur précédent a quitté le projet en laissant un code incomplet, parsemé de commentaires `todo`, d'erreurs de syntaxe et de tentatives de mise en page infructueuses :
- Le balisage HTML manque cruellement de **sémantique HTML5** (trop de `<div>`, d'anciens formatages obsolètes).
- La mise en page **Flexbox** est incomplète ou cassée à plusieurs endroits clés.
- La police d'écriture personnalisée n'est pas connectée.
- Des erreurs de syntaxe CSS et HTML empêchent le navigateur d'afficher la page correctement.

**Votre mission :** À l'aide des consignes de cette feuille, inspectez les fichiers `index.html` et `style.css` situés dans votre dossier de travail, résolvez chaque problème et rendez une page conforme au rendu professionnel attendu.

---

## Grille d'évaluation & Tâches à réaliser

### 1. Typographie & Google Fonts (/ 2 points)

- [ ] **1.1 Connexion de la police (1 pt)** :  
  Importez la police Google Fonts **Poppins** (graisses 400, 600 et 700 recommandées).
- [ ] **1.2 Application du style (1 pt)** :  
  Appliquez la police `Poppins` sur le `body` avec une police générique de secours (`sans-serif`).

---

### 2. Débogage de la syntaxe CSS (/ 3 points)

Plusieurs erreurs bloquent l'interpréteur CSS du navigateur. Corrigez-les.

---

### 3. Syntaxe HTML & Accessibilité (/ 3 points)

- [ ] **3.1 Image et texte alternatif (1 pt)** :  
  L'image de la première carte (Maine Coon) ne s'affiche pas. Et l'ancien développeur a laissé des commentaires sur les textes alternatifs manquants.
- [ ] **3.2 Cohérence des balises (1 pt)** :  
  Il y a plusieurs erreurs de balisage.
- [ ] **3.3 Listes à puces (1 pt)** :  
  Dans la barre latérale (`.tips-list`), les critères d'adoption sont de simples paragraphes précédés de tirets. Transformez-les en une véritable liste ordonnée ou non ordonnée (`<ul>` ou `<ol>` avec `<li>`).

---

### 4. Sémantique HTML5 (/ 6 points)

Remplacez les balises non sémantiques par des balises sémantiques.

- [ ] **4.1 En-tête et Navigation (2 pts)** 
- [ ] **4.2 Structure de page et cartes (2.5 pts)** 
- [ ] **4.3 Sidebar, Footer et Accentuation (1.5 pt)**

---

### 5. Mise en page Flexbox & Finitions (/ 6 points)

- [ ] **5.1 Alignement de l'en-tête (1.5 pt)**
- [ ] **5.2 Alignement de la navigation (1 pt)**  
- [ ] **5.3 Colonnes de la page (1.5 pt)**
- [ ] **5.4 Grille et structure des cartes (1.5 pt)**
- [ ] **5.5 Bonus / Media Query (0.5 pt)** :  
  À la fin de `style.css`, une tentative de Media Query a été ébauchée avec une syntaxe erronée. Et ce n'est pas terminé.

---

## Critères de validation visuelle (Rendu final attendu)

1. Le bandeau d'en-tête reste blanc et net avec le titre orange à gauche et les liens alignés à droite.
2. Les deux colonnes (articles à gauche, encadrés d'astuces à droite) s'affichent côte à côte sur écran d'ordinateur.
3. Les 3 cartes de chats sont présentées en grille ordonnée, avec une hauteur harmonisée et des images nettes.
4. L'ensemble de la page utilise une police sans empattement moderne et arrondie (Poppins).

# Rendu

https://forms.gle/8ehAF5EhVr7h5vS79
