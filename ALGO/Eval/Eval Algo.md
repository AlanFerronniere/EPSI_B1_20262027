> Durée : le temps qu'il faudra à chacun dans la limite de 3h

#### Vous pouvez tester vos résultats ici : 
#### https://www.latetedanslephp.fr/chatons

Rendu ici : https://forms.gle/nX11yspbzBoUuVvs5

# Le Distributeur Automatique de Lait pour Chatons

À la grande chatterie, le distributeur automatique de lait tiède a été automatisé pour nourrir la portée. Pour que chaque chaton puisse obtenir sa dose de lait dans sa coupelle, il doit présenter son **collier d'identification**, sur lequel est gravée une chaîne de caractères complexe.

Pour déverrouiller la machine et servir les chatons, vous devez calculer la **Ration de Lait** de chaque chaton à partir de son collier.

**Règle (Partie 1) :** 
La Ration de Lait d'un chaton (en ml) est calculée en multipliant le **nombre de chiffres** présents dans la chaîne de son collier par la **somme de tous ces chiffres** :

$$\text{Ration} = (\text{Nombre de chiffres}) \times (\text{Somme des chiffres})$$

* S'il n'y a aucun chiffre dans la chaîne du collier, la ration est de **0 ml**.

Votre mission est, pour chaque ligne de votre fichier d'entrée, de **calculer la Ration de Lait**. Ensuite, vous devez trouver la **somme de _toutes_ ces rations** pour obtenir la valeur de déverrouillage finale de la fontaine.

## Exemples

Voici quelques exemples de chaînes de colliers de chatons et le calcul de leur ration :

```
Garfield-7b-3
Moustic22-Patte4-1
Flocon-005
Minou-Gris
```

Et le tableau récapitulatif des calculs :

| Collier de Chaton (Input) | Chiffres Présents | Nb de Chiffres | Somme des Chiffres | Ration de Lait (Calcul) |
| ------------------------- | ----------------- | -------------- | ------------------ | ----------------------- |
| `Garfield-7b-3`           | 7, 3              | 2              | 7+3 = 10           | 2 &times; 10 = **20**   |
| `Moustic22-Patte4-1`      | 2, 2, 4, 1        | 4              | 2+2+4+1 = 9        | 4 &times; 9 = **36**    |
| `Flocon-005`              | 0, 0, 5           | 3              | 0+0+5 = 5          | 3 &times; 5 = **15**    |
| `Minou-Gris`              | _(Aucun chiffre)_ | 0              | 0                  | **0**                   |


Si votre fichier d'entrée ne contenait que ces quatre lignes, la **valeur de déverrouillage finale** serait la somme des rations :

20 + 36 + 15 + 0 = **71**

## Fichier à analyser

```
Moustic15-Patte3-8
Flocon-006
Garfield-8b-2
Minou-Gris
Choupette-4x-7
Tigrou-9y-5
Peluche-2z-1
Noisette-3a-6
Caline-1b-8
Simba-6c-9
03-Minette-8
Felix-5d-4
Luna-1e-8
Whiskers-3f-5
Shadow-6g-2
Mittens-4h-1
Salem-7i-5
Oliver-3j-5-8-arbre
Bella-2k-6-89
Nala-8l-1-34
Tiger-5m-4-67-vert
Snowball-8n-9-91-jaune
Lucky-4o-3-22-bleu
2-Fluffy-7p-5-44-rouge
Coco-1q-8-33-dore
Midnight-4r-8-55-noir
Ziggy-7s-2-66-blanc
Patches-3t-6-77-gris
Misty-5u-1-88-marron
Socks-8v-4-99-argente
33Boots-2w-7-88
12-Simba-6x-3-24
Furball-8y-9-45
Tigerlily-4z-5-67-sauvage
Shadowfax-7a-1-89-91
Bouboule22-des-94
Whiskers-3b-6-32
Cuddles-9c-2-54
15-Tabby-Red
Mittens-Zen
Roger-Chat-5d
67-7d8-Henry-98
Fluffy-4e-3-78
Snowflake-8f-1-56
Midnight-6g-9-34
Salem-2h-5-23
Marcel-8i-7-45
Pixel-8x-2
Caramel-3b-9-doux
Sushi-8m-5-12
09-Gribouille-6r
Reglisse-4f-1-sombre
Orion-2k-7-alpha
Pompom-5g-3-88
34-Cookie-9h-8
Filou-1z-4-vif
Zephyr-7d-6-beta
25-Bounty-3j-8-blanc
Kiwi-8p-2-44-vert
Mochi-6t-1-62
Gizmo-4v-5-test-03
28-Merlin-8u-9-magie
Patoune-2a-7-RC4
Olympe-9y-4-91-gris
Ronron-v4-5q-6
Atlas-1w-8-35
72-Baghera-6c-3-nuit
Nougat-4z-2-56
Virus-9b-8-debug
Octet-3m-1-1010
Chipie-7n-5-patch
88-Oreo-2s-8-double
Pacha-8k-4-v2.3
Spip-5l-6-87
Java-1e-9-script
Calypso-8r-3-bleu
44-Pixel-6g-2-RGB
Kilo-3h-5-mega
Muffin-9t-1-77
Watson-4d-7-elem
23-Mango-8f-8-jaune
Nebula-2v-6-astro
Zadig-7w-4-99
Vodka-5y-1-pur
88-Ziggy-1p-3-star
Cortex-8x-9-fast
Bounty-3a-5-v3
29-Simba-6z-2-roi
Linux-4c-8-kernel
Pepite-9j-7-or
Moka-2m-3-cafe
58-Sputnik-7q-8
Tofu-1r-5-bloc
Ramses-8u-6-sphinx
Wifi-3n-9-connect
06-Twix-8s-4-gauche
Zelda-5k-2-link
Dobby-7b-4-ronron
Plume-3p-9-dodo
Gatsby-9k-1-pelage
```

## Partie 2

Le code de la première partie était trop facile à percer. L'équipe vétérinaire a mis à jour l'algorithme du distributeur pour équilibrer les apports selon le profil des chatons :

* Pour les chatons dont le nom commence par une **lettre**, on ne prend en compte que les **chiffres pairs** (0, 2, 4, 6, 8) présents dans la chaîne :
  $$\text{Ration} = (\text{Nombre de chiffres pairs}) \times (\text{Somme des chiffres pairs})$$
* Pour les chatons dont le nom commence par un **chiffre**, on ne prend en compte que les **chiffres impairs** (1, 3, 5, 7, 9) présents dans la chaîne :
  $$\text{Ration} = (\text{Nombre de chiffres impairs}) \times (\text{Somme des chiffres impairs})$$
* S'il n'y a aucun chiffre correspondant dans la chaîne, la ration est de **0 ml**.

Par exemple :

| Collier de Chaton (Input) | Chiffres Filtrés (Pairs / Impairs) | Nb Chiffres | Somme | Nouvelle Ration (Calcul) |
| ------------------------- | ---------------------------------- | ----------- | ----- | ------------------------ |
| `Garfield-7b-3`           | _(commence par 'G' &rarr; pairs : aucun)_ | 0           | 0     | **0**                    |
| `Moustic22-Patte4-1`      | _(commence par 'M' &rarr; pairs : 2, 2, 4)_ | 3           | 2+2+4 = 8 | 3 &times; 8 = **24**     |
| `Flocon-005`              | _(commence par 'F' &rarr; pairs : 0, 0)_ | 2           | 0+0 = 0 | 2 &times; 0 = **0**      |
| `1-Minou-Gris`            | _(commence par '1' &rarr; impairs : 1)_ | 1           | 1     | 1 &times; 1 = **1**      |
| `02-Minette-7`            | _(commence par '0' &rarr; impairs : 7)_ | 1           | 7     | 1 &times; 7 = **7**      |


Calculez la nouvelle **valeur de déverrouillage finale** en utilisant cette nouvelle règle pour chaque ligne du fichier d'entrée.

## Un indice
Parce que je suis gentil : https://www.php.net/manual/fr/function.ctype-digit.php


![[ALGO/Eval/chaton_fontaine_lait.png]]

![[ALGO/Eval/chatons_fete_lait.png]]
