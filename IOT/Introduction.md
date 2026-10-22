# Introduction générale à l'IoT

Module IOTE145 – Culture générale & Fondamentaux

---

## 1. Qu'est-ce que l'IoT ?

L'**Internet des Objets** (*Internet of Things* ou **IoT**) désigne l'écosystème d'objets physiques dotés de capteurs, de processeurs et de modules réseau, capables de **collecter**, d'**échanger des données** et d'**agir** sur leur environnement via Internet, sans intervention humaine directe.

On résume souvent une solution IoT à la règle des **3 C** :
1. **Capter :** Mesurer une grandeur physique du monde réel (température, présence, luminosité, pression, vibrations).
2. **Communiquer :** Transmettre la donnée via un réseau adapté (Wi-Fi, Bluetooth, LoRaWAN, 4G/5G).
3. **Calculer & Agir :** Analyser la donnée (localement ou dans le cloud) et déclencher une action (allumer une pompe, envoyer une alerte, réguler un chauffage).

```text
[ Monde Réel ] ──(Capteur)──> [ ESP32 / Objet ] ──(Réseau)──> [ Cloud / Serveur ] ──(Alerte / Dashboard)
      ▲                               │
      └─────────(Actionneur)──────────┘
```

---

## 2. Historique : De la machine à soda aux milliards d'objets

L'IoT ne date pas d'hier, mais sa démocratisation s'est accélérée grâce à la miniaturisation électronique et à la baisse des coûts des puces réseau.

### Les grandes dates clés :

- **1982 – Le premier ancêtre connecté (Carnegie Mellon University) :** 
  https://www.csd.cmu.edu/news/decoding-the-internet-of-things
  Des étudiants en informatique de l'université Carnegie Mellon relient un distributeur de canettes de Coca-Cola au réseau ARPANET (l'ancêtre d'Internet). L'objectif : savoir à distance depuis leur terminal si le distributeur contenait des canettes et si elles étaient fraîches, pour éviter de se déplacer inutilement.

- **1990 – Le grille-pain IP :**
  https://www.livinginternet.com/i/ia_myths_toast.htm
  John Romkey conçoit le premier grille-pain pilotable à distance via le protocole TCP/IP à la conférence InterOp.

- **1999 – Naissance du terme "Internet of Things" :**
  **Kevin Ashton**, chercheur au MIT et travaillant pour Procter & Gamble, invente l'expression pour promouvoir l'usage des puces RFID (*Radio-Frequency Identification*) dans la gestion logistique des chaînes d'approvisionnement.
  
- **2000 – Les premières tentatives grand public :**
  LG présente le premier réfrigérateur connecté à Internet (*Internet Digital DIOS*). Un échec commercial à l'époque (prix exorbitant de plus de 20 000 $ et utilité encore contestée).
  
- **2008 / 2010 – Le point de bascule de Cisco :**
  Pour la première fois dans l'histoire, **le nombre d'appareils connectés à Internet dépasse la population mondiale humaine**.
  
- **2014 – Le séisme ESP8266 :**
  La société chinoise **Espressif** commercialise la puce ESP8266 pour moins de 3 dollars, offrant un microcontrôleur avec Wi-Fi intégré. Cela révolutionne le monde des makers, de la recherche et de l'IoT industriel. En 2016 sortira son grand frère, l'**ESP32** (Wi-Fi + Bluetooth + double cœur).
  
- **Aujourd'hui :** Plus de 15 à 20 milliards d'objets connectés en activité dans le monde, avec une montée en puissance de l'IA embarquée (**Edge AI**) et des protocoles basse consommation unifiés comme **Matter**.

---

## 3. Pourquoi connecter des objets ? (Utilité & Valeur)

Connecter un objet n'a d'intérêt que s'il apporte une valeur ajoutée mesurable :

1. **Automatisation des processus :** Supprimer les relevés manuels récurrents (ex. télé-relève automatique des compteurs d'eau et de gaz Linky/Gazpar).
2. **Prise de décision factuelle :** Baser la stratégie d'une entreprise sur des métriques précises et mesurées en temps réel plutôt que sur des intuitions.
3. **Maintenance prédictive :** Détecter une anomalie vibratoire ou une surchauffe sur une turbine avant qu'elle ne casse, réduisant drastiquement les coûts d'arrêt de production.
4. **Optimisation énergétique et transition écologique :** Réduire la consommation électrique des bâtiments en adaptant la climatisation et l'éclairage à la présence réelle des collaborateurs.
5. **Sécurité et alertes temps réel :** Alerte immédiate par SMS/notification en cas de détection de fuite d'eau, de fumée ou d'intrusion.

---

## 4. Les domaines d'application aujourd'hui

```text
┌─────────────────┬─────────────────┬─────────────────┐
│   Smart Home    │   Smart City    │  Industrie 4.0  │
│  (Domotique)    │ (Villes intel.) │ (IIoT usines)   │
├─────────────────┼─────────────────┼─────────────────┤
│  Santé / IoMT   │   Agriculture   │   Logistique    │
│  (Médical)      │  (AgTech)       │ (Supply Chain)  │
└─────────────────┴─────────────────┴─────────────────┘
```

- **Smart Home & Bâtiment intelligent :**
  - Gestion automatique du chauffage, serrures connectées, volets solaires, surveillance de la qualité de l'air intérieur ($CO_2$).
- **Smart City :**
  - Lampadaires intelligents qui n'éclairent à 100% que lorsqu'un piéton ou une voiture approche.
  - Poubelles équipées de capteurs ultrasons prévenant les éboueurs dès qu'elles sont pleines (optimisation des tournées de ramassage).
  - Détection de places de stationnement libres via capteurs magnétiques au sol.
- **Industrie 4.0 (IIoT - Industrial IoT) :**
  - Traçabilité de chaque pièce sur une ligne d'assemblage.
  - Surveillance d'environnements dangereux (gaz toxiques dans les mines, pression des pipelines).
- **Santé & Médical (IoMT - Internet of Medical Things) :**
  - Capteurs de glycémie en continu pour diabétiques envoyant des alertes sur smartphone.
  - Pacemakers télé-surveillés par les cardiologues.
  - Traçabilité du transport des organes et vaccins.
- **Agriculture connectée (AgTech) :**
  - Sondes capacitives mesurant l'humidité du sol à plusieurs profondeurs pour n'irriguer que la juste quantité d'eau.
  - Colliers GPS/santé pour le suivi des troupeaux en alpage.
- **Logistique & Transport :**
  - Balises de géolocalisation et capteurs de chocs dans les conteneurs maritimes.
  - Enregistreurs de température vérifiant le respect continu de la chaîne du froid alimentaire et pharmaceutique.

---

## 5. Le Matériel : De quoi est composé un système IoT ?

### 5.1 Les Capteurs (Sensors)
Ils convertissent une grandeur physique en signal électrique :
- **Environnement :** DHT22 / BME280 (Température, Humidité, Pression).
- **Lumière :** Photorésistance (LDR), capteur UV.
- **Mouvement & Présence :** Détecteur infrarouge passif (PIR), radar Doppler, ultrasons (HC-SR04).
- **Position & Dynamique :** Accéléromètre / Gyroscope (MPU6050), GPS.
- **Qualité de l'air :** Capteurs de particules fines (PMS5003), monoxyde de carbone, gaz (série MQ).

### 5.2 Les Actionneurs (Actuators)
Ils exécutent une action physique commandée par le code :
- **Visuel :** LED simple, bandeau RGB Neopixel, écran OLED / e-Paper.
- **Sonore :** Buzzer piézoélectrique actif ou passif.
- **Mécanique :** Relais électromagnétique (pour piloter du 230V), servomoteur, électrovanne d'arrosage.

### 5.3 Le Cerveau : Microcontrôleur (MCU) vs Microprocesseur (MPU)

| Critère | Microcontrôleur (ex: ESP32, STM32) | Microprocesseur (ex: Raspberry Pi, PC) |
| :--- | :--- | :--- |
| **Système d'exploitation** | **Aucun** (exécute un seul binaire compilé) | OS complet (Linux, Windows) |
| **Consommation** | Minime (quelques $\mu A$ en veille, dizaines de $mA$ actif) | Élevée (500 $mA$ à 3 $A$) |
| **Alimentation possible** | Piles, batterie solaire pendant plusieurs années | Alimentation secteur ou batterie volumineuse |
| **Gestion du temps** | Déterministe au cycle d'horloge près (idéal C/temps réel) | Soumise aux interruptions de l'OS |
| **Coût unitaire** | 2 à 5 € | 40 à 100 € |

### 5.4 Les Réseaux de communication

Il n'existe pas un réseau unique parfait : le choix dépend du compromis **Portée / Débit / Consommation d'énergie**.

```text
    Débit élevé ▲
                │     Wi-Fi / Ethernet
                │           4G / 5G
                │
                │     BLE / Zigbee
                │                       LoRaWAN / Sigfox / NB-IoT
    Faible débit▼─────────────────────────────────────────────────►
                Faible portée                   Longue portée
```

1. **Courte portée / Débit élevé :**
   - **Wi-Fi :** Présent partout, idéal pour transférer beaucoup de données, mais très gourmand en énergie (inadapté pour des capteurs sur pile bouton).
2. **Courte portée / Faible consommation (PAN) :**
   - **BLE (Bluetooth Low Energy) :** Pour les montres, balises iBeacon, objets personnels.
   - **Zigbee / Thread / Matter :** Réseau maillé (*mesh*), standard de la domotique moderne.
3. **Longue portée / Faible consommation (LPWAN) :**
   - **LoRaWAN / Sigfox :** Portée de 2 à 15 km, traverse les murs, batterie durant jusqu'à 10 ans ! En contrepartie, le débit est minuscule (quelques octets par message, idéal pour une mesure de température toutes les heures).
   - **NB-IoT / LTE-M :** Dérivés des réseaux mobiles cellulaires optimisés pour les objets.

---

## 6. Les Grands Défis de l'IoT

### 1. La Cybersécurité
L'IoT est historiquement la cible privilégiée des cyberattaques :
- Matériel à ressources limitées rendant parfois le chiffrement lourd difficile.
- Mots de passe par défaut conservés en production (`admin` / `admin`).
- Absence de mises à jour de sécurité des micrologiciels (firmwares).
- *Exemple historique :* L'attaque DDoS massive du botnet **Mirai** (2016), où des centaines de milliers de caméras IP et routeurs mal sécurisés ont mis à terre des géants du web comme Twitter, Netflix et GitHub.

### 2. L'Autonomie énergétique
Comment maintenir un capteur agricole ou un capteur en forêt en vie pendant 5 à 10 ans sans changer de pile ?
- Nécessite l'usage de modes d'endormissement profond (**Deep Sleep**), où le microcontrôleur s'éteint quasi totalement entre deux mesures.

### 3. L'Interopérabilité
Pendant longtemps, chaque constructeur utilisait son propre protocole fermé (enfermement propriétaire). L'arrivée récente de consortiums et de standards ouverts comme **MQTT** et **Matter** vise à unifier la communication des objets hétérogènes.

---

## 7. Synthèse : Pourquoi l'informaticien doit maîtriser l'IoT ?

L'informatique ne s'arrête plus à l'écran de l'ordinateur ou à la base de données :
- C'est l'IoT qui **génère les données brutes** qui alimenteront ensuite le Big Data, le Cloud et l'Intelligence Artificielle.
- Comprendre les contraintes physiques du hardware et le langage C permet d'écrire du code plus optimisé, plus résilient et de dialoguer efficacement avec les ingénieurs systèmes et réseaux.
