# Exercice 2 (PHP) : Table de multiplication personnalisée

## Énoncé

Demander à l'utilisateur quelle table de multiplication il souhaite (par exemple `7`) et jusqu'à combien il veut la calculer (par exemple `5`), puis afficher le résultat ligne par ligne :

```text
7 x 1 = 7
7 x 2 = 14
7 x 3 = 21
7 x 4 = 28
7 x 5 = 35
```

---

## Étape 1 : Solution simple avec une boucle `for`

On récupère les deux informations via `readline()`, puis on utilise une boucle `for` pour itérer de 1 jusqu'à la limite demandée.

### Code PHP

```php
<?php
// 1. Saisie des paramètres
$table = (int) readline("Quelle table voulez-vous ? ");
$limite = (int) readline("Jusqu'à combien ? ");

echo PHP_EOL . "--- Table de " . $table . " (jusqu'à " . $limite . ") ---" . PHP_EOL;

// 2. Boucle de calcul et d'affichage
for ($i = 1; $i <= $limite; $i++) {
    $resultat = $table * $i;
    echo $table . " x " . $i . " = " . $resultat . PHP_EOL;
}
```

---

## Étape 2 : Sécurisation et validation des entrées

Pour éviter les erreurs si l'utilisateur saisit du texte ou un nombre négatif, on filtre la saisie avec `filter_var()` et `FILTER_VALIDATE_INT`.  
On utilise une boucle `do...while` pour redemander la valeur tant qu'elle n'est pas valide (entier supérieur à 0).

### Code PHP avec validation

```php
<?php
// Saisie sécurisée de la table (entier positif)
do {
    $saisie = readline("Quelle table voulez-vous (entier > 0) ? ");
    $table = filter_var($saisie, FILTER_VALIDATE_INT);

    if ($table === false || $table <= 0) {
        echo "Erreur : veuillez entrer un entier strictement positif." . PHP_EOL;
    }
} while ($table === false || $table <= 0);

// Saisie sécurisée de la limite (entier positif)
do {
    $saisie = readline("Jusqu'à combien voulez-vous aller (entier > 0) ? ");
    $limite = filter_var($saisie, FILTER_VALIDATE_INT);

    if ($limite === false || $limite <= 0) {
        echo "Erreur : veuillez entrer un entier strictement positif." . PHP_EOL;
    }
} while ($limite === false || $limite <= 0);

// Affichage
echo PHP_EOL . "--- Table de " . $table . " jusqu'à " . $limite . " ---" . PHP_EOL;

for ($i = 1; $i <= $limite; $i++) {
    $resultat = $table * $i;
    echo $table . " x " . $i . " = " . $resultat . PHP_EOL;
}
```

---

## Étape 3 : Variante avec proposition de recommencer

On peut englober le programme dans une boucle principale pour proposer à l'utilisateur de calculer une autre table sans relancer le script manuellement.

### Code PHP interactif

```php
<?php
do {
    // 1. Saisie des valeurs
    $table = (int) readline("Quelle table voulez-vous ? ");
    $limite = (int) readline("Jusqu'à combien ? ");

    // 2. Affichage
    echo PHP_EOL . "--- Table de " . $table . " jusqu'à " . $limite . " ---" . PHP_EOL;
    for ($i = 1; $i <= $limite; $i++) {
        echo $table . " x " . $i . " = " . ($table * $i) . PHP_EOL;
    }

    // 3. Demander si on continue
    echo PHP_EOL;
    $recommencer = readline("Voulez-vous afficher une autre table ? (o/n) : ");
    echo PHP_EOL;

} while (strtolower(trim($recommencer)) === 'o');

echo "Programme terminé. À bientôt !" . PHP_EOL;
```

---
