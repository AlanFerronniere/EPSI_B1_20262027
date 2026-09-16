
# Code du cours


# Syntaxe de base

## Variables et types de données

Les variables en PHP sont déclarées avec le symbole `$` suivi du nom de la variable. 

Bien que les variables locales en PHP déduisent automatiquement leur type à l'affectation, **PHP 8** met l'accent sur un typage fort et explicite (typage des paramètres, retours de fonctions, propriétés de classes, types d'union `int|float`, et mode strict).

```php
<?php
// Typage implicite lors de l'affectation :
$entier = 42;                    // int (entier)
$flottant = 3.14;                // float (flottant / nombre à virgule)
$chaine = "Bonjour, monde !";    // string (chaîne de caractères)
$booleen = true;                 // bool (booléen : true ou false)
$tableau = [1, 2, 3];            // array (tableau)

// En PHP 8, on peut inspecter le type d'une variable :
var_dump($entier);   // Affiche : int(42)
echo gettype($chaine); // Affiche : string
?>
```

## Structures de contrôle
Les structures de contrôle permettent de diriger le flux d'exécution du programme.

### Conditionnelles
```php
<?php
$age = 20;
if ($age < 18) {
		echo "Mineur";
} elseif ($age >= 18 && $age < 65) {
		echo "Adulte";
} else {
		echo "Senior";
}
?>
```
### Boucles

#### for

```php
<?php
for ($i = 0; $i < 10; $i++) {
		echo $i;
}
?>
```
#### while

```php
<?php
$i = 0;
while ($i < 10) {
		echo $i;
		$i++;
}
?>
```

#### foreach (pour les tableaux)

```php
<?php
$tableau = ["pomme", "banane", "cerise"];
foreach ($tableau as $fruit) {
		echo $fruit;
}
?>
```
## Fonctions

Les fonctions sont définies avec le mot-clé `function`.

Depuis **PHP 8**, il est fortement recommandé de déclarer explicitement le type des paramètres et le type de retour, ainsi que d'activer le mode strict avec `declare(strict_types=1);`.

### Exemple de base avec typage

```php
<?php
declare(strict_types=1); // Active la vérification stricte des types

function addition(int $a, int $b): int {
		return $a + $b;
}

$resultat = addition(5, 3);
echo $resultat; // Affiche 8
?>
```

### Typage avancé en PHP 8 (Union types & void)

PHP 8 permet également de combiner plusieurs types possibles (**types d'union**) ou d'indiquer qu'une fonction ne retourne rien (`void`) :

```php
<?php
declare(strict_types=1);

// Union types (int ou float)
function multiplier(int|float $a, int|float $b): int|float {
		return $a * $b;
}

// Fonction sans valeur de retour (void)
function afficherMessage(string $message): void {
		echo $message . PHP_EOL;
}

echo multiplier(2.5, 4); // Affiche 10
afficherMessage("Bonjour !");
?>
```

