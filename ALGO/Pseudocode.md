# Les bases en pseudocode

Ce document résume le cours d'algorithmique en utilisant le pseudocode. Il couvre les concepts fondamentaux, les structures de contrôle, les tableaux, les fonctions, et présente des exercices pratiques pour renforcer la compréhension.
## 1. Introduction à l'Algorithmique en pseudocode

Le pseudo-code est un langage de description d'algorithmes. Il se situe entre le langage humain (comme le français) et un langage de programmation. Il n'a pas de syntaxe stricte, son objectif principal est d'être **clair et compréhensible** par n'importe qui.

## 2. Les Concepts Fondamentaux

### Les Variables

Une **variable** est un conteneur qui stocke une information. Elle est identifiée par un nom et possède un type qui définit la nature de la donnée qu'elle peut contenir.

**Types de données courants :**

- **Entier :** Nombres entiers (ex: `1`, `-42`, `1337`).
- **Réel :** Nombres à virgule (ex: `3.14`, `-25.5`).
- **Chaîne de caractères :** Texte (ex: `"Bonjour le monde !"`).
- **Booléen :** Représente une valeur de vérité, soit **Vrai**, soit **Faux**.

#### Déclaration et Affectation :

En pseudo-code, on déclare une variable puis on lui affecte une valeur avec le symbole <-.

```
// Déclare une variable 'age' de type Entier
Variable age : Entier

// Affecte la valeur 25 à la variable 'age'
age <- 25

// On peut aussi faire les deux en une seule ligne
Variable nom_utilisateur : Chaîne <- "Alice"
```

### Les Opérations

Les algorithmes manipulent les variables à l'aide d'opérateurs.

- **Arithmétiques :** `+` (addition), `-` (soustraction), `*` (multiplication), `/` (division), `%` (modulo), `^` (puissance)
- **De comparaison :** `==` (égal), `!=` (différent), `>` (supérieur), `<` (inférieur), `>=` (supérieur ou égal), `<=` (inférieur ou égal).
- **Logiques :** `ET`, `OU`, `NON`.

### Lire et Écrire

Ce sont les instructions de base pour interagir avec l'utilisateur.

- **`Écrire`** : Affiche un message ou le contenu d'une variable à l'écran.
- **`Lire`** : Attend que l'utilisateur saisisse une donnée et la stocke dans une variable.

**Exemple :**

```
Variable nom : Chaîne
Écrire "Quel est votre nom ?"
Lire nom
Écrire "Bonjour, " + nom
```

---

## 3. Les Structures de Contrôle

Ces structures permettent de contrôler le déroulement de l'algorithme.

### Les Conditions (Si... Alors... Sinon)

Elles permettent d'exécuter des blocs d'instructions différents selon qu'une condition est vraie ou fausse (**donc un booléen !**).

**Syntaxe :**

```
Si (condition) Alors
    // Bloc d'instructions si la condition est Vraie
Sinon
    // Bloc d'instructions si la condition est Fausse
Fin Si
```

**Exemple : Vérifier la majorité d'une personne.**

```
Variable age : Entier
Écrire "Quel est votre âge ?"
Lire age

Si (age >= 18) Alors
    Écrire "Vous êtes majeur."
Sinon
    Écrire "Vous êtes mineur."
Fin Si
```

### Les Boucles

Les boucles permettent de répéter un bloc d'instructions plusieurs fois.

#### La boucle `Tant Que`

Répète un bloc tant qu'une condition reste vraie. La condition est vérifiée **avant** chaque itération.

**Syntaxe :**

```
Tant Que (condition) Faire
    // Instructions à répéter
Fin Tant Que
```

**Exemple : Compter de 1 à 5.**

```
Variable compteur : Entier <- 1
Tant Que (compteur <= 5) Faire
    Écrire compteur
    compteur <- compteur + 1
Fin Tant Que
```

#### La boucle `Pour`

Idéale lorsque l'on connaît à l'avance le nombre de répétitions.

**Syntaxe :**

```
Pour variable allant de valeur_début à valeur_fin Faire
    // Instructions à répéter
Fin Pour
```

**Exemple : Afficher 3 fois "Bonjour".**

```
Variable i : Entier
Pour i allant de 1 à 3 Faire
    Écrire "Bonjour"
Fin Pour
```

## 4. Les Tableaux

Un **tableau** est une structure de données permettant de stocker une collection d'éléments **souvent du même type**. Chaque élément est accessible via un **indice**, qui commence souvent à 0.

**Déclaration :**

```
// Déclare un tableau nommé 'notes' pouvant contenir 4 entiers (indices 0, 1, 2, 3)
Variable notes : Tableau[4] d'Entiers
```

**Utilisation :**

```
// Stocker la valeur 15 dans la première case (indice 0)
notes[0] <- 15

// Afficher la valeur de la troisième case (indice 2)
Écrire notes[2]
```

#### Parcourir un tableau :

On utilise très souvent une boucle Pour pour parcourir tous les éléments d'un tableau.

```
Variable notes : Tableau[3] d'Entiers
notes[0] <- 12
notes[1] <- 17
notes[2] <- 8

Pour i allant de 0 à 2 Faire
    Écrire "Note à l'indice " + i + " : " + notes[i]
Fin Pour
```

On ajoute souvent une fonction pour la taille du tableau afin de rendre le code plus flexible.
`Taille(nom_du_tableau)` retourne le nombre d'éléments dans le tableau.

```
Variable notes : Tableau[3] d'Entiers
notes[0] <- 12
notes[1] <- 17
notes[2] <- 8
Pour i allant de 0 à Taille(notes) - 1 Faire
		Écrire "Note à l'indice " + i + " : " + notes[i]
Fin Pour
```

On utilise aussi une **boucle spécifique** `Pour Chaque` pour parcourir les éléments d'un tableau sans se soucier des indices.

```
Variable notes : Tableau[3] d'Entiers
notes[0] <- 12
notes[1] <- 17
notes[2] <- 8
Pour Chaque note dans notes Faire
	Écrire "Note : " + note
Fin Pour
```


## 5. Les Fonctions

Une **fonction** est un bloc d'instructions réutilisable qui accomplit une tâche spécifique. Elle peut accepter des données en entrée (les **paramètres**) et retourner un résultat en sortie. L'usage de fonctions rend le code plus modulaire, lisible et facile à maintenir.

**Syntaxe :**

```
Fonction NomDeLaFonction(parametre1: Type, parametre2: Type) : TypeDeRetour
    // Déclaration de variables locales à la fonction
    Début
        // Instructions de la fonction
        Retourner resultat
    Fin
```

**Exemple : Une fonction pour calculer la somme de deux nombres.**

```
// Définition de la fonction
Fonction CalculerSomme(a : Entier, b : Entier) : Entier
    Variable somme_locale : Entier
	somme_locale <- a + b
	Retourner somme_locale
Fin Fonction

// --- Algorithme principal qui utilise la fonction ---
Début
    Variable resultat_final : Entier
    // Appel de la fonction avec les valeurs 5 et 10
    resultat_final <- CalculerSomme(5, 10)
    Écrire "Le résultat est : " + resultat_final // Affichera 15
Fin
```

### La récursivité

La récursivité est une technique où une fonction s'appelle elle-même pour résoudre un problème. C'est particulièrement utile pour les problèmes qui peuvent être divisés en sous-problèmes similaires.
**Exemple : Calcul de la factorielle d'un nombre.**

```
// Définition de la fonction récursive
Fonction Factorielle(n : Entier) : Entier
	Début
		// Condition d'arrêt
		Si (n == 0) Alors
				Retourner 1
		Sinon
				// Appel récursif
				Retourner n * Factorielle(n - 1)
		Fin Si
	Fin
// --- Algorithme principal ---
Début
		Variable nombre, resultat_factorielle : Entier
		Écrire "Entrez un nombre pour calculer sa factorielle :"
		Lire nombre
		resultat_factorielle <- Factorielle(nombre)
		Écrire "La factorielle de " + nombre + " est " + resultat_factorielle
Fin
```

## 6. Exercices Pratiques

### Exercice 1 : Conversion de Température

Écrire un algorithme qui demande à l'utilisateur une température en degrés Celsius et la convertit en degrés Fahrenheit.

Rappel de la formule : F=(C×59​)+32.

```
Variable celsius, fahrenheit : Réel

Début
    Écrire "Veuillez entrer une température en degrés Celsius :"
    Lire celsius

    fahrenheit <- (celsius * 9/5) + 32

    Écrire celsius + "°C équivaut à " + fahrenheit + "°F."
Fin
```


### Exercice 2 : Pair ou Impair ?

Écrire un algorithme qui demande un nombre entier à l'utilisateur et affiche s'il est pair ou impair.

Indice : Utilisez l'opérateur modulo (% ou MOD), qui donne le reste d'une division. Un nombre est pair si le reste de sa division par 2 est 0.

```
Variable nombre : Entier

Début
    Écrire "Veuillez entrer un nombre entier :"
    Lire nombre

    Si (nombre MOD 2 == 0) Alors
        Écrire "Le nombre est pair."
    Sinon
        Écrire "Le nombre est impair."
    Fin Si
Fin
```

### Exercice 3 : Recherche dans un Tableau

Écrire un algorithme qui recherche une valeur donnée dans un tableau d'entiers et affiche si elle a été trouvée ou non.

```
Variables monTableau : Tableau[5] d'Entiers
Variable valeurRecherchee, i : Entier
Variable trouve : Booléen <- Faux

Début
    // Initialisation du tableau pour l'exemple
    monTableau[0] <- 10
    monTableau[1] <- 25
    monTableau[2] <- 5
    monTableau[3] <- 42
    monTableau[4] <- 18

    Écrire "Quelle valeur souhaitez-vous rechercher ?"
    Lire valeurRecherchee

    // Parcours du tableau
    Pour i allant de 0 à 4 Faire
        Si (monTableau[i] == valeurRecherchee) Alors
            trouve <- Vrai
        Fin Si
    Fin Pour

    Si (trouve == Vrai) Alors
        Écrire "La valeur a été trouvée dans le tableau."
    Sinon
        Écrire "La valeur n'a pas été trouvée."
    Fin Si
Fin
```

### Exercice 4 : Calcul de Puissance avec une Fonction

Créer une fonction `CalculerPuissance` qui prend deux entiers en paramètres (`nombre` et `exposant`) et retourne `nombre` élevé à la puissance `exposant`. Ensuite, écrire un algorithme principal qui utilise cette fonction.


```
// Définition de la fonction
Fonction CalculerPuissance(nombre : Entier, exposant : Entier) : Entier
    Variable resultat : Entier <- 1
    Variable i : Entier
    Début
        Si (exposant < 0) Alors
            // Cas simple : on ne gère pas les exposants négatifs
            Retourner -1 
        Sinon
            Pour i allant de 1 à exposant Faire
                resultat <- resultat * nombre
            Fin Pour
            Retourner resultat
        Fin Si
    Fin

// --- Algorithme principal ---
Début
    Variable n, e, resultat_puissance : Entier

    Écrire "Entrez le nombre :"
    Lire n
    Écrire "Entrez l'exposant :"
    Lire e

    resultat_puissance <- CalculerPuissance(n, e)

    Si (resultat_puissance == -1) Alors
        Écrire "L'exposant doit être positif."
    Sinon
        Écrire n + " à la puissance " + e + " = " + resultat_puissance
    Fin Si
Fin
```

## Exercices d'Algorithmique : Niveau Intermédiaire

Ces exercices vous demanderont de manipuler des tableaux de manière plus complexe et de structurer votre logique avec plus de rigueur.

### Exercice 5 : Tri à Bulles (Bubble Sort)

Le **tri à bulles** est un algorithme de tri simple. Il parcourt le tableau plusieurs fois et compare à chaque fois les éléments adjacents pour les échanger s'ils ne sont pas dans le bon ordre. Le processus est répété jusqu'à ce que plus aucun échange ne soit nécessaire, signifiant que le tableau est trié.

**Énoncé :** Écrire un algorithme qui trie un tableau d'entiers en ordre croissant en utilisant la méthode du tri à bulles.

```
Variables monTableau : Tableau[5] d'Entiers
Variable i, j, temp : Entier

Début
    // Initialisation du tableau pour l'exemple
    monTableau[0] <- 42
    monTableau[1] <- 18
    monTableau[2] <- 5
    monTableau[3] <- 25
    monTableau[4] <- 10

    Écrire "Tableau avant le tri : 42, 18, 5, 25, 10"

    // Boucle externe pour parcourir tout le tableau
    Pour i allant de 0 à 3 Faire
        // Boucle interne pour comparer les paires
        Pour j allant de 0 à 3 Faire
            // Si l'élément actuel est plus grand que le suivant
            Si (monTableau[j] > monTableau[j+1]) Alors
                // On les échange
                temp <- monTableau[j]
                monTableau[j] <- monTableau[j+1]
                monTableau[j+1] <- temp
            Fin Si
        Fin Pour
    Fin Pour

    Écrire "Tableau après le tri :"
    Pour i allant de 0 à 4 Faire
        Écrire monTableau[i]
    Fin Pour
Fin
```

### Exercice 6 : Inversion d'un Tableau

**Énoncé :** Écrire un algorithme qui inverse l'ordre des éléments d'un tableau sans utiliser de deuxième tableau. Par exemple, un tableau `[10, 20, 30]` deviendrait `[30, 20, 10]`.

_Indice :_ Vous aurez besoin de parcourir seulement la moitié du tableau et d'échanger l'élément `i` avec l'élément à la position symétrique.

```
Variables monTableau : Tableau[5] d'Entiers
Variable i, temp, taille : Entier

Début
    taille <- 5
    // Initialisation du tableau
    monTableau[0] <- 10
    monTableau[1] <- 20
    monTableau[2] <- 30
    monTableau[3] <- 40
    monTableau[4] <- 50

    Écrire "Tableau original : 10, 20, 30, 40, 50"

    // On parcourt la première moitié du tableau
    Pour i allant de 0 à (taille / 2) - 1 Faire
        // Échange de l'élément i avec son symétrique
        temp <- monTableau[i]
        monTableau[i] <- monTableau[taille - 1 - i]
        monTableau[taille - 1 - i] <- temp
    Fin Pour

    Écrire "Tableau inversé :"
    Pour i allant de 0 à taille - 1 Faire
        Écrire monTableau[i]
    Fin Pour
Fin
```

### Exercice 7 : Le Nombre d'Or (Suite de Fibonacci)

La suite de Fibonacci est une suite de nombres où chaque terme est la somme des deux termes qui le précèdent. Elle commence généralement par 0 et 1.

F_0=0,F_1=1,F_n=F_n−1+F_n−2

(Séquence : 0, 1, 1, 2, 3, 5, 8, 13, 21, ...)

**Énoncé :** Écrire une fonction **récursive** `Fibonacci(n)` qui calcule le n-ième terme de la suite. Ensuite, écrire un algorithme qui demande un nombre `n` à l'utilisateur et affiche les `n` premiers termes de la suite.

Une fonction **récursive** est une fonction qui s'appelle elle-même. 🔄

```
// Définition de la fonction récursive
Fonction Fibonacci(n : Entier) : Entier
    Début
        // Condition d'arrêt
        Si (n <= 1) Alors
            Retourner n
        // Appel récursif
        Sinon
            Retourner Fibonacci(n-1) + Fibonacci(n-2)
        Fin Si
    Fin

// --- Algorithme principal ---
Début
    Variable nombreTermes, i : Entier

    Écrire "Combien de termes de la suite de Fibonacci souhaitez-vous afficher ?"
    Lire nombreTermes

    Pour i allant de 0 à nombreTermes - 1 Faire
        Écrire Fibonacci(i)
    Fin Pour
Fin
```

### Exercice 8 : Recherche par Dichotomie

La recherche dichotomique est un algorithme très efficace pour trouver un élément dans un tableau **trié**. Le principe est de comparer l'élément recherché avec la valeur au milieu du tableau. Si les valeurs sont égales, on a trouvé. Sinon, on recommence la recherche soit dans la moitié inférieure, soit dans la moitié supérieure du tableau.

**Énoncé :** Écrire une fonction `RechercheDichotomique` qui prend en paramètres un tableau d'entiers **trié**, sa taille, et la valeur recherchée. La fonction doit retourner l'indice de la valeur si elle est trouvée, et -1 sinon.

```
Fonction RechercheDichotomique(t : Tableau d'Entiers, taille : Entier, valeur: Entier) : Entier
    Variable debut, fin, milieu : Entier
    Début
        debut <- 0
        fin <- taille - 1

        Tant Que (debut <= fin) Faire
            milieu <- (debut + fin) / 2 // Division entière

            Si (t[milieu] == valeur) Alors
                // On a trouvé la valeur !
                Retourner milieu
            Sinon Si (t[milieu] < valeur) Alors
                // La valeur est dans la moitié droite
                debut <- milieu + 1
            Sinon
                // La valeur est dans la moitié gauche
                fin <- milieu - 1
            Fin Si
        Fin Tant Que

        // La valeur n'a pas été trouvée
        Retourner -1
    Fin

// --- Algorithme principal pour tester la fonction ---
Début
    Variable monTableau : Tableau[7] d'Entiers
    Variable valeurCherchee, indexResultat : Entier

    // Le tableau DOIT être trié
    monTableau[0] <- 5
    monTableau[1] <- 10
    monTableau[2] <- 18
    monTableau[3] <- 25
    monTableau[4] <- 42
    monTableau[5] <- 51
    monTableau[6] <- 60

    Écrire "Quelle valeur cherchez-vous ?"
    Lire valeurCherchee

    indexResultat <- RechercheDichotomique(monTableau, 7, valeurCherchee)

    Si (indexResultat != -1) Alors
        Écrire "La valeur " + valeurCherchee + " a été trouvée à l'indice " + indexResultat
    Sinon
        Écrire "La valeur " + valeurCherchee + " n'est pas dans le tableau."
    Fin Si
Fin
```