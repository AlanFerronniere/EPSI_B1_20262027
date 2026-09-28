Vous devez modéliser la BDD d'une compagnie aérienne.
L'idée est de garder l'historique des vols réels effectués par les avions de la compagnie, ainsi que les informations sur les avions et leur maintenance.

# Avions

Pour un avion on a :
- son immatriculation : chaîne de caractères unique à 15 caractères (max)
- son modèle : chaîne de caractères (max 50 caractères)
- sa marque : chaîne de caractères (max 50 caractères)
- Son nombre d'heures de vol total : entier positif
- Sa date de mise en service : date
- Son statut : actif ou inactif
- Sa date et aéroport de prochaine maintenance prévue
- Son historique de maintenance (plusieurs enregistrements par avion, voir plus bas)
- sa localisation actuelle (le dernier aéroport où il a atterri)
	(on pourrait regarder le dernier vol effectué, mais pour simplifier l'interrogation on stocke directement l'aéroport)
# Aéroports
Pour un aéroport on a :
- son code IATA : chaîne de caractères unique de 3 caractères (facultatif)
- son code ICAO (OACI) : chaîne de caractères unique de 4 caractères unique
- Ville
- Pays
# Vols
Pour un vol on a :
- une référence de vol commercial (facultatif)
- un aéroport de départ
- un aéroport d'arrivée théorique
- la date et heure de départ prévue
- la date et heure d'arrivée prévue
- la date et heure de départ réelle
- la date et heure d'arrivée réelle
- l'aéroport d'arrivée réel
- l'avion utilisé pour le vol

# Maintenance
Pour une opération de maintenance on a :
- l'avion concerné
- la date de début de la maintenance
- la date de fin de la maintenance
- le type de maintenance (préventive, corrective, etc.)
- la description des travaux effectués
- le nom du chef d'équipe de maintenance responsable
- l'aéroport où la maintenance a été effectuée

# Voyages
Un voyage est une séquence de vols effectués par un passager.
Pour un voyage on a :
- un identifiant unique de voyage
- un aéroport de départ
- un aéroport d'arrivée
- les vols composant le voyage (1 ou plusieurs vols par voyage)

> ! un vol peut ne pas faire partie d'un voyage (vol de transit, vol cargo, etc.). Et un vol peut être associé à plusieurs voyages (Par exemple un vol Paris-Hong-Kong fait partie de d'un voyage Paris-Hong-Kong et aussi d'un voyage Paris-Sydney qui fait escale à Hong-Kong).

# UML

```mermaid
classDiagram
    direction TB

    class Aeroport {
        +string code_oaci PK
        +string code_iata
        +string ville
        +string pays
    }

    class Avion {
        +string immatriculation PK
        +string marque
        +string modele
        +int heures_vol_total
        +date date_mise_en_service
        +string statut
        +date date_prochaine_maintenance
        #string code_oaci_prochaine_maint FK
        #string code_oaci_localisation FK
    }

    class Maintenance {
        +int id_maintenance PK
        #string immatriculation FK
        #string code_oaci_aeroport FK
        +datetime date_debut
        +datetime date_fin
        +string type_maintenance
        +string description
        +string chef_equipe
    }

    class Vol {
        +int id_vol PK
        +string ref_commerciale
        #string immatriculation FK
        #string code_oaci_depart FK
        #string code_oaci_arrivee_prevue FK
        #string code_oaci_arrivee_reelle FK
        +datetime date_heure_depart_prevue
        +datetime date_heure_arrivee_prevue
        +datetime date_heure_depart_reelle
        +datetime date_heure_arrivee_reelle
    }

    class Voyage {
        +int id_voyage PK
        #string code_oaci_depart FK
        #string code_oaci_arrivee FK
    }

    class EtapeVoyage {
        #int id_voyage PK, FK
        #int id_vol PK, FK
        +int ordre
    }

    %% Relations Avion & Aeroport
    Aeroport "1" <-- "0..*" Avion : est localisé à
    Aeroport "0..1" <-- "0..*" Avion : prochaine maintenance à

    %% Relations Maintenance
    Avion "1" <-- "0..*" Maintenance : concerne
    Aeroport "1" <-- "0..*" Maintenance : effectuée à

    %% Relations Vol
    Avion "1" <-- "0..*" Vol : assuré par
    Aeroport "1" <-- "0..*" Vol : départ de
    Aeroport "1" <-- "0..*" Vol : arrivée théorique à
    Aeroport "0..1" <-- "0..*" Vol : arrivée réelle à

    %% Relations Voyage
    Aeroport "1" <-- "0..*" Voyage : origine de
    Aeroport "1" <-- "0..*" Voyage : destination de

    %% Composition Voyage / Vol (relation N:M ordonnée)
    Voyage "1" -- "1..*" EtapeVoyage : composé de
    Vol "0..*" -- "0..*" EtapeVoyage : intervient dans
```

# MLD

```mermaid
erDiagram
    AEROPORT ||--o{ AVION : "héberge (localisation)"
    AEROPORT ||--o{ AVION : "prévoit prochaine maintenance"
    AEROPORT ||--o{ VOL : "départ"
    AEROPORT ||--o{ VOL : "arrivée prévue"
    AEROPORT ||--o{ VOL : "arrivée réelle"
    AEROPORT ||--o{ VOYAGE : "origine"
    AEROPORT ||--o{ VOYAGE : "destination"
    AEROPORT ||--o{ MAINTENANCE : "lieu de maintenance"

    AVION ||--o{ VOL : "effectue"
    AVION ||--o{ MAINTENANCE : "subit"

    VOYAGE ||--|{ VOYAGE_VOL : "est composé de"
    VOL ||--o{ VOYAGE_VOL : "fait partie de"

    AEROPORT {
        varchar(4) code_oaci PK "Code OACI 4 car. unique"
        varchar(3) code_iata UK "Code IATA 3 car. (facultatif)"
        varchar(100) ville
        varchar(100) pays
    }

    AVION {
        varchar(15) immatriculation PK "Immatriculation unique (max 15)"
        varchar(50) modele
        varchar(50) marque
        int heures_vol_total
        date date_mise_en_service
        varchar(20) statut "actif ou inactif"
        date date_prochaine_maintenance
        varchar(4) code_oaci_prochaine_maint FK "Aéroport prévu"
        varchar(4) code_oaci_localisation FK "Dernier aéroport d'atterrissage"
    }

    MAINTENANCE {
        int id_maintenance PK
        varchar(15) immatriculation FK "Avion concerné"
        varchar(4) code_oaci_aeroport FK "Aéroport d'intervention"
        datetime date_debut
        datetime date_fin "Nullable si en cours"
        varchar(50) type_maintenance "préventive, corrective, etc."
        text description
        varchar(100) chef_equipe
    }

    VOL {
        int id_vol PK
        varchar(20) ref_commerciale "Facultatif (ex: AF123)"
        varchar(15) immatriculation FK "Avion utilisé"
        varchar(4) code_oaci_depart FK "Aéroport départ"
        varchar(4) code_oaci_arrivee_prevue FK "Aéroport arrivée théorique"
        varchar(4) code_oaci_arrivee_reelle FK "Aéroport arrivée réel (si dérouté/atterri)"
        datetime date_heure_depart_prevue
        datetime date_heure_arrivee_prevue
        datetime date_heure_depart_reelle "Nullable"
        datetime date_heure_arrivee_reelle "Nullable"
    }

    VOYAGE {
        int id_voyage PK
        varchar(4) code_oaci_depart FK "Aéroport de départ"
        varchar(4) code_oaci_arrivee FK "Aéroport d'arrivée finale"
    }

    VOYAGE_VOL {
        int id_voyage PK,FK
        int id_vol PK,FK
        int ordre_vol "Ordre du vol dans la séquence du voyage"
    }
```

**Représentation textuelle du MLD :**
- **AEROPORT** (<u>code_oaci</u>, code_iata, ville, pays)
- **AVION** (<u>immatriculation</u>, marque, modele, heures_vol_total, date_mise_en_service, statut, date_prochaine_maintenance, #code_oaci_prochaine_maint, #code_oaci_localisation)
- **MAINTENANCE** (<u>id_maintenance</u>, date_debut, date_fin, type_maintenance, description, chef_equipe, #immatriculation, #code_oaci_aeroport)
- **VOL** (<u>id_vol</u>, ref_commerciale, date_heure_depart_prevue, date_heure_arrivee_prevue, date_heure_depart_reelle, date_heure_arrivee_reelle, #immatriculation, #code_oaci_depart, #code_oaci_arrivee_prevue, #code_oaci_arrivee_reelle)
- **VOYAGE** (<u>id_voyage</u>, #code_oaci_depart, #code_oaci_arrivee)
- **VOYAGE_VOL** (<u>#id_voyage</u>, <u>#id_vol</u>, ordre_vol)


