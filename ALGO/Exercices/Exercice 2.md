# Exercice 2 (PHP) : Nombre triangulaire et boucles imbriquées

## Énoncé

Un **nombre triangulaire** est un nombre que l'on peut représenter sous la forme d'un triangle équilatéral ou rectangle formé de points.  
Le nombre triangulaire de rang $n$ correspond à la somme de tous les entiers de 1 jusqu'à $n$ :
- Rang 1 : 1 point
- Rang 2 : 1 + 2 = 3 points
- Rang 3 : 1 + 2 + 3 = 6 points
- Rang 4 : 1 + 2 + 3 + 4 = 10 points

**Consigne :**  
Demander à l'utilisateur de saisir un rang $n$, puis :
1. Dessiner le triangle d'étoiles `*` correspondant.
2. Calculer et afficher la valeur numérique du nombre triangulaire ($T_n$).

**Exemple d'exécution :**
```text
Quel rang ? 4

*
**
***
****

Le nombre triangulaire de rang 4 vaut : 10
```

---

## 1. Code initial (vu en cours)

```php
<?php
// Dessiner le nombre triangulaire d'un rang  
echo "Quel rang ? ";  
$rang = readline();  
  
for ($i = 1; $i <= $rang; $i++) {  
    for ($j = 1; $j <= $i; $j++) {  
        echo "*";  
    }  
    echo "\n";  
}
```

### Analyse du code :
- **Boucle externe (`$i`) :** gère le numéro de ligne (de la ligne 1 à la ligne `$rang`).
- **Boucle interne (`$j`) :** gère le nombre d'étoiles affichées sur la ligne courante. À la ligne `$i`, elle affiche exactement `$i` étoiles.
- **Le saut de ligne :** `echo "\n";` (ou `PHP_EOL`) s'exécute à la fin de chaque ligne, une fois que la boucle interne a terminé d'afficher ses étoiles.

---

## 2. Étape 1 : Calcul de la valeur numérique du nombre triangulaire

Pour enrichir l'exercice, on calcule le total de points/étoiles :
- **Par cumul itératif :** on additionne `$i` à chaque passage dans la boucle.
- **Par la formule mathématique :** $T_n = \frac{n \times (n + 1)}{2}$.

### Code PHP complet

```php
<?php
$rang = (int) readline("Quel rang ? ");
$totalEtoiles = 0;

echo PHP_EOL;

// Dessin du triangle et comptage
for ($i = 1; $i <= $rang; $i++) {  
    for ($j = 1; $j <= $i; $j++) {  
        echo "*";  
    }  
    echo PHP_EOL;
    $totalEtoiles += $i; // Cumul du nombre d'étoiles
}

echo PHP_EOL;
echo "Le nombre triangulaire de rang " . $rang . " vaut : " . $totalEtoiles . PHP_EOL;

// Vérification avec la formule mathématique : n * (n + 1) / 2
$formule = ($rang * ($rang + 1)) / 2;
echo "(Vérification par formule : " . $formule . ")" . PHP_EOL;
```

---

## 3. Étape 2 : Sécurisation de la saisie avec `filter_var()`

Si l'utilisateur saisit du texte ou un nombre négatif, on filtre la saisie avec `filter_var()` et `FILTER_VALIDATE_INT`, puis on redemande tant que la valeur n'est pas un entier strictement supérieur à 0 :

```php
<?php
do {
    $saisie = readline("Quel rang (entier > 0) ? ");
    $rang = filter_var($saisie, FILTER_VALIDATE_INT);

    if ($rang === false || $rang <= 0) {
        echo "Erreur : veuillez entrer un entier strictement positif." . PHP_EOL;
    }
} while ($rang === false || $rang <= 0);

echo PHP_EOL;

for ($i = 1; $i <= $rang; $i++) {  
    for ($j = 1; $j <= $i; $j++) {  
        echo "*";  
    }  
    echo PHP_EOL;  
}

$valeur = ($rang * ($rang + 1)) / 2;
echo PHP_EOL . "Nombre triangulaire T(" . $rang . ") = " . $valeur . PHP_EOL;
```

---

## 4. Variantes algorithmiques

### Variante 1 : Utilisation de la fonction native `str_repeat()`
En PHP, il existe une fonction intégrée pour répéter une chaîne sans avoir à coder la boucle interne manuellement :

```php
<?php
$rang = (int) readline("Quel rang ? ");

echo PHP_EOL;
for ($i = 1; $i <= $rang; $i++) {
    echo str_repeat("*", $i) . PHP_EOL;
}
```

---

### Variante 2 : Triangle inversé (décroissant)
On peut parcourir la boucle à rebours (de `$rang` jusqu'à 1) :

```php
<?php
$rang = (int) readline("Quel rang ? ");

echo PHP_EOL;
for ($i = $rang; $i >= 1; $i--) {
    echo str_repeat("*", $i) . PHP_EOL;
}
```

**Exemple pour un rang 4 :**
```text
****
***
**
*
```

---

### Variante 3 : Pyramide centrée (Aller plus loin)
Pour centrer les étoiles et former une pyramide symétrique, on ajoute des espaces devant chaque ligne :

```php
<?php
$rang = (int) readline("Hauteur de la pyramide ? ");

echo PHP_EOL;
for ($i = 1; $i <= $rang; $i++) {
    $espaces = str_repeat(" ", $rang - $i);
    $etoiles = str_repeat("*", (2 * $i) - 1);
    echo $espaces . $etoiles . PHP_EOL;
}
```

**Exemple pour une hauteur 4 :**
```text
   *
  ***
 *****
*******
```