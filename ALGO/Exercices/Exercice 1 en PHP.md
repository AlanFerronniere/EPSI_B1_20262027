# Exercice 1 en PHP : Gestion de notes et calcul de moyenne

Ce document reprend pas à pas l'algorithme de **[[Exercice 1 pseudo-code]]** et sa traduction en langage **PHP** pour une exécution en ligne de commande (CLI).

---

## Rappel : Saisie utilisateur en PHP CLI

En ligne de commande PHP, on utilise la fonction `readline()` pour inviter l'utilisateur à saisir une valeur.  
Comme `readline()` renvoie toujours une chaîne (`string`), on convertit la saisie en nombre à virgule avec `(float)` :

```php
$note = (float) readline("Entrez une note : ");
```

---

## Étape 1 : Saisie de 10 notes stockées dans un tableau

> **Consigne :** Demander à l'utilisateur de saisir 10 notes et les stocker dans un tableau.

### Rappel du pseudo-code
```text
Variable notes : tableau[] Reel
Pour i de 0 à 9 Faire
    Ecrire "Note " + (i + 1)
    Lire note[]
Fin Pour
```

### Traduction en PHP
En PHP, les tableaux sont naturellement dynamiques. L'opérateur `$notes[] = ...` permet d'ajouter un élément à la fin du tableau sans avoir à spécifier l'indice :

```php
<?php
$notes = []; // Déclaration d'un tableau vide

for ($i = 0; $i < 10; $i++) {
    $numero = $i + 1;
    $notes[] = (float) readline("Note N°" . $numero . " : ");
}

// Vérification du contenu du tableau
print_r($notes);
```

---

## Étape 2 : Calcul de la moyenne du tableau

> **Consigne :** Calculer et afficher la moyenne des 10 notes saisies.

### Rappel du pseudo-code
```text
Variable notes : tableau[] Reel
Variable somme : Reel <- 0
Variable moyenne : Reel

Pour i de 0 à 9 Faire
    Ecrire "Note " + (i + 1)
    Lire note[]
Fin Pour

Pour i de 0 à 9 Faire
    somme <- somme + notes[i]
Fin Pour

moyenne <- somme / 10
Ecrire "La moyenne est : " + moyenne
```

### Traduction en PHP
```php
<?php
$notes = [];

// 1. Saisie des 10 notes
for ($i = 0; $i < 10; $i++) {
    $notes[] = (float) readline("Note N°" . ($i + 1) . " : ");
}

// 2. Calcul de la somme
$somme = 0.0;
for ($i = 0; $i < 10; $i++) {
    $somme += $notes[$i];
}

// 3. Calcul et affichage de la moyenne
$moyenne = $somme / 10;
echo "La moyenne est : " . round($moyenne, 2) . " / 20" . PHP_EOL;
```

> **Astuce PHP (fonctions natives) :**  
> En PHP, on peut aussi calculer la somme et la taille directement avec `array_sum()` et `count()` :  
> `$moyenne = array_sum($notes) / count($notes);`

---

## Étape 3 : Saisie libre (arrêt sur entrée vide)

> **Consigne :** Permettre à l'utilisateur de saisir autant de notes qu'il le souhaite. La saisie s'arrête lorsqu'il appuie sur Entrée sans rien taper.

### Rappel du pseudo-code
```text
Variable notes : tableau[] Reel
Variable saisie : Chaine
Variable somme : Reel <- 0
Variable moyenne : Reel

Ecrire "Entrez une note (laisser vide pour terminer) :"
Lire saisie

Tant Que saisie != "" Faire
    notes[] <- saisie
    Ecrire "Entrez une note (laisser vide pour terminer) :"
    Lire saisie
Fin Tant Que

Si Taille(notes) > 0 Alors
    Pour i de 0 à Taille(notes) - 1 Faire
        somme <- somme + notes[i]
    Fin Pour

    moyenne <- somme / Taille(notes)
    Ecrire "La moyenne est : " + moyenne
Sinon
    Ecrire "Aucune note n'a été saisie."
Fin Si
```

### Traduction en PHP
```php
<?php
$notes = [];

echo "Entrez une note (laisser vide pour terminer) :" . PHP_EOL;
$saisie = readline("> ");

while ($saisie !== "") {
    $notes[] = (float) $saisie;

    echo "Entrez une note (laisser vide pour terminer) :" . PHP_EOL;
    $saisie = readline("> ");
}

// On vérifie qu'au moins une note a été saisie pour éviter une division par zéro
if (count($notes) > 0) {
    $somme = 0.0;
    $totalNotes = count($notes);

    for ($i = 0; $i < $totalNotes; $i++) {
        $somme += $notes[$i];
    }

    $moyenne = $somme / $totalNotes;
    echo "Nombre de notes : " . $totalNotes . PHP_EOL;
    echo "La moyenne est : " . round($moyenne, 2) . " / 20" . PHP_EOL;
} else {
    echo "Aucune note n'a été saisie." . PHP_EOL;
}
```

---

## Variante 1 : Parcours avec `foreach`

En pseudo-code, on peut utiliser la structure `Pour Chaque note dans notes`.  
En PHP, c'est la boucle `foreach` qui s'utilise directement sur le tableau :

```php
<?php
// Remplacement de la boucle 'for' par un 'foreach' :
$somme = 0.0;

foreach ($notes as $note) {
    $somme += $note;
}

$moyenne = $somme / count($notes);
echo "La moyenne est : " . round($moyenne, 2) . PHP_EOL;
```

---

## Variante 2 : Cumul direct en une seule boucle (sans tableau et avec filtrage)

Si l'objectif est uniquement de calculer la moyenne globale, il n'est pas nécessaire de conserver l'ensemble des notes en mémoire dans un tableau. On peut cumuler la somme au fur et à mesure et utiliser un simple compteur pour dénombrer les notes valides.

En PHP, la fonction `filter_var()` avec le filtre `FILTER_VALIDATE_INT` permet de valider proprement et directement que la saisie est un entier valide :

### Traduction en PHP
```php
<?php
$somme = 0;
$nbNotes = 0;

echo "Entrez une note entre 0 et 20 (laisser vide pour terminer) :" . PHP_EOL;
$saisie = readline("> ");

while ($saisie !== "") {
    $note = filter_var($saisie, FILTER_VALIDATE_INT);

    if ($note !== false && $note >= 0 && $note <= 20) {
        $somme += $note; // Cumul direct
        $nbNotes++;      // Comptage des notes valides
    } else {
        echo "Erreur : veuillez entrer un nombre entier compris entre 0 et 20." . PHP_EOL;
    }

    echo "Entrez une note entre 0 et 20 (laisser vide pour terminer) :" . PHP_EOL;
    $saisie = readline("> ");
}

if ($nbNotes > 0) {
    $moyenne = $somme / $nbNotes;
    echo PHP_EOL . "--- Bilan ---" . PHP_EOL;
    echo "Nombre de notes valides : " . $nbNotes . PHP_EOL;
    echo "La moyenne est          : " . round($moyenne, 2) . " / 20" . PHP_EOL;
} else {
    echo "Aucune note valide n'a été saisie." . PHP_EOL;
}
```

> **Astuce :** Pour accepter également les notes décimales (ex: `14.5`), on peut remplacer `FILTER_VALIDATE_INT` par `FILTER_VALIDATE_FLOAT`.

