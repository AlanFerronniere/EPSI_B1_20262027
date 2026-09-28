# Exercice 3 : Table de multiplication en PHP

## Énoncé

Créer un programme en ligne de commande qui demande à l'utilisateur :
1. Quelle table de multiplication il souhaite afficher (ex: `7`).
2. Jusqu'à quel multiplicateur il souhaite aller (ex: `5`).

Puis affiche le résultat sous la forme :
```text
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
```

---

## 1. Code initial

```php
<?php
$tableDe = readline("Table de quoi ? ");  
$jusquA = readline("Jusqu'à combien ? ");  
  
for ($i = 1; $i <= $jusquA; $i++) {  
    // echo $tableDe . " x " . $i . " = ";  
    echo "$tableDe x $i = ";  
    echo $tableDe * $i;  
    echo PHP_EOL;  
}
```

### Analyse du code initial :
- `readline()` permet de récupérer la saisie de l'utilisateur dans le terminal.
- La boucle `for` fait varier le compteur `$i` de 1 jusqu'à la valeur limite `$jusquA`.
- PHP effectue une conversion implicite de type (le texte retourné par `readline()` est automatiquement converti en nombre lors de la multiplication `*` et de la comparaison `<=`).

---

## 2. Étape 1 : Optimisation et nettoyage de l'affichage

On peut regrouper les trois instructions `echo` en une seule ligne grâce à la concaténation `.`, en plaçant l'opération arithmétique entre parenthèses :

```php
<?php
$tableDe = (int) readline("Table de quoi ? ");  
$jusquA = (int) readline("Jusqu'à combien ? ");  

echo PHP_EOL . "--- Table de $tableDe jusqu'à $jusquA ---" . PHP_EOL;

for ($i = 1; $i <= $jusquA; $i++) {  
    echo "$tableDe x $i = " . ($tableDe * $i) . PHP_EOL;  
}
```

---

## 3. Étape 2 : Sécurisation des entrées avec `filter_var()`

Si l'utilisateur entre du texte (ex: `"abc"`) ou un nombre négatif, le programme risque d'avoir un comportement inattendu.  
On valide les entrées avec `filter_var(..., FILTER_VALIDATE_INT)` :

```php
<?php
$saisieTable = readline("Table de quoi ? ");
$tableDe = filter_var($saisieTable, FILTER_VALIDATE_INT);

$saisieLimite = readline("Jusqu'à combien ? ");
$jusquA = filter_var($saisieLimite, FILTER_VALIDATE_INT);

// Vérification de la validité des deux valeurs
if ($tableDe === false || $jusquA === false || $jusquA <= 0) {
    echo "Erreur : veuillez renseigner des nombres entiers valides (limite > 0)." . PHP_EOL;
} else {
    echo PHP_EOL . "--- Table de $tableDe jusqu'à $jusquA ---" . PHP_EOL;
    for ($i = 1; $i <= $jusquA; $i++) {  
        echo "$tableDe x $i = " . ($tableDe * $i) . PHP_EOL;  
    }
}
```

---

## 4. Étape 3 : Saisie robuste avec redemande (`do...while`)

Pour rendre le script ergonomique, on redemande la saisie tant qu'elle n'est pas correcte :

```php
<?php
// 1. Saisie sécurisée de la table
do {
    $saisie = readline("Table de quoi ? ");
    $tableDe = filter_var($saisie, FILTER_VALIDATE_INT);

    if ($tableDe === false) {
        echo "Erreur : entrez un entier valide." . PHP_EOL;
    }
} while ($tableDe === false);

// 2. Saisie sécurisée de la limite (> 0)
do {
    $saisie = readline("Jusqu'à combien ? ");
    $jusquA = filter_var($saisie, FILTER_VALIDATE_INT);

    if ($jusquA === false || $jusquA <= 0) {
        echo "Erreur : la limite doit être un entier supérieur à 0." . PHP_EOL;
    }
} while ($jusquA === false || $jusquA <= 0);

// 3. Affichage du résultat
echo PHP_EOL . "--- Table de $tableDe jusqu'à $jusquA ---" . PHP_EOL;
for ($i = 1; $i <= $jusquA; $i++) {  
    echo "$tableDe x $i = " . ($tableDe * $i) . PHP_EOL;  
}
```

---

## 5. Pour aller plus loin : La table de Pythagore (Boucles imbriquées)

Pour s'entraîner aux boucles imbriquées (une boucle dans une boucle), on peut afficher toutes les tables de multiplication de 1 jusqu'à `N` :

```php
<?php
$taille = (int) readline("Taille de la table de Pythagore : ");

echo PHP_EOL;
for ($ligne = 1; $ligne <= $taille; $ligne++) {
    for ($col = 1; $col <= $taille; $col++) {
        // str_pad permet d'aligner proprement les colonnes
        echo str_pad((string)($ligne * $col), 5, " ", STR_PAD_LEFT);
    }
    echo PHP_EOL;
}
```
