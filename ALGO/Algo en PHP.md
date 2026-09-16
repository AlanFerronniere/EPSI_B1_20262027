
# Code du cours


# Syntaxe de base

## Variables et types de données

Les variables en PHP sont déclarées avec le symbole `$` suivi du nom de la variable. PHP est un langage faiblement typé, ce qui signifie que vous n'avez pas besoin de déclarer explicitement le type de données d'une variable.

```php
<?php
$entier = 42; // entier

$flottant = 3.14; // flottant

$chaine = "Bonjour, monde!"; // chaîne de caractères

$booleen = true; // booléen

$tableau = array(1, 2, 3); // tableau
//ou
$tableau = [1, 2, 3]; // tableau (syntax plus récente)

$
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
$tableau = array("pomme", "banane", "cerise");
foreach ($tableau as $fruit) {
		echo $fruit;
}
?>
```
## Fonctions
Les fonctions sont définies avec le mot-clé `function`.

```php
<?php
function addition($a, $b) {
		return $a + $b;
}
$resultat = addition(5, 3);
echo $resultat; // Affiche 8
?>
```

