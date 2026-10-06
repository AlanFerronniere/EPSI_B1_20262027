# Exercice 4 (PHP) : Jeu du "Plus ou Moins" (Devine le nombre)

## Énoncé

L'ordinateur choisit un nombre aléatoire entre 1 et 1000.  
Le joueur doit deviner ce nombre en faisant des propositions successives :
- Si la proposition est trop grande, le programme affiche `"Trop grand"`.
- Si la proposition est trop petite, le programme affiche `"Trop petit"`.
- Dès que le nombre est trouvé, le programme félicite le joueur, affiche le nombre d'essais nécessaires, et lui propose de recommencer une partie.

---

## 1. Code initial (vu en cours)

```php
<?php  
$jouer = "O";  
while ($jouer == "O") {  
    $nombreADeviner = rand(1, 1000);  
    $nombrePropose = readline("Devinez un nombre entre 1 et 1000." . PHP_EOL . "Nombre proposé ? ");  
    $essais = 1;  
  
    while ($nombrePropose != $nombreADeviner) {  
        if ($nombrePropose > $nombreADeviner) {  
            echo "Trop grand" . PHP_EOL;  
        } elseif ($nombrePropose < $nombreADeviner) {  
            echo "Trop petit" . PHP_EOL;  
        }  
  
        $nombrePropose = readline("Nombre proposé ? ");  
        $essais++;  
    }  
  
//si j'arrive là c'est que je suis sorti du while  
    echo "Gagné ! ($essais essais)" . PHP_EOL;  
  
    $jouer = readline("Voulez vous rejouer ? (O/N)");  
}
```

### Analyse du code initial

1. **La double boucle :**
   - **Boucle externe (`while ($jouer == "O")`) :** gère la rejouabilité d'une partie.
   - **Boucle interne (`while ($nombrePropose != $nombreADeviner)`) :** gère les tentatives jusqu'à trouver le nombre secret.
2. **Le comptage des essais :**
   - L'initialisation à `$essais = 1;` permet de comptabiliser la première proposition effectuée avant la boucle.
   - À chaque nouvelle tentative saisie dans la boucle, `$essais++` incrémente le compteur. Le compte total est donc parfaitement exact (y compris si l'on trouve dès le 1er coup).
3. **Piste d'amélioration (duplication de saisie) :**
   - L'instruction `readline("Nombre proposé ? ")` est écrite deux fois : une première fois avant d'entrer dans le `while`, puis à nouveau à l'intérieur de la boucle.

---

## 2. Étape 1 : Simplification de la structure avec `do...while`

Une boucle `do...while` est particulièrement adaptée ici car le joueur effectue **toujours au moins une tentative**.  
Elle permet de regrouper la saisie et l'incrémentation en un seul endroit, évitant ainsi d'avoir à dupliquer l'appel à `readline()` :

```php
<?php
$jouer = "O";

while (strtoupper(trim($jouer)) === "O") {
    $nombreADeviner = rand(1, 1000);
    $essais = 0;

    echo PHP_EOL . "--- Nouvelle partie : Devinez le nombre entre 1 et 1000 ---" . PHP_EOL;

    do {
        $nombrePropose = (int) readline("Nombre proposé ? ");
        $essais++;

        if ($nombrePropose > $nombreADeviner) {
            echo "Trop grand !" . PHP_EOL;
        } elseif ($nombrePropose < $nombreADeviner) {
            echo "Trop petit !" . PHP_EOL;
        }
    } while ($nombrePropose !== $nombreADeviner);

    echo "Bravo, vous avez trouvé en $essais essai(s) !" . PHP_EOL;

    $jouer = readline("Voulez-vous rejouer ? (O/N) : ");
}

echo "Merci d'avoir joué. À bientôt !" . PHP_EOL;
```

---

## 3. Étape 2 : Sécurisation et validation des entrées avec `filter_var()`

Si le joueur entre une chaîne de texte (ex: `"abc"`) ou un nombre hors de l'intervalle `[1, 1000]`, on peut lui signaler l'erreur sans pénaliser son compteur d'essais :

```php
<?php
$jouer = "O";

while (strtoupper(trim($jouer)) === "O") {
    $nombreADeviner = rand(1, 1000);
    $essais = 0;

    echo PHP_EOL . "--- Devinez un nombre entre 1 et 1000 ---" . PHP_EOL;

    do {
        $saisie = readline("Nombre proposé ? ");
        $nombrePropose = filter_var($saisie, FILTER_VALIDATE_INT);

        // Validation de la saisie
        if ($nombrePropose === false || $nombrePropose < 1 || $nombrePropose > 1000) {
            echo "Attention : veuillez entrer un nombre entier valide entre 1 et 1000." . PHP_EOL;
            continue; // On redemande sans compter d'essai
        }

        $essais++;

        if ($nombrePropose > $nombreADeviner) {
            echo "Trop grand !" . PHP_EOL;
        } elseif ($nombrePropose < $nombreADeviner) {
            echo "Trop petit !" . PHP_EOL;
        }
    } while ($nombrePropose !== $nombreADeviner);

    echo "Gagné ! Le nombre était bien $nombreADeviner (trouvé en $essais essai(s))." . PHP_EOL;

    $jouer = readline("Voulez-vous rejouer ? (O/N) : ");
}

echo "Au revoir !" . PHP_EOL;
```

---

## 4. Étape 3 : Nombre d'essais limité et lien avec la recherche dichotomique

On peut limiter le joueur à un nombre maximal d'essais, par exemple **10 essais**.

> **Pourquoi 10 essais ? (Lien avec la complexité algorithmique)**  
> En utilisant la stratégie de la **recherche dichotomique** (en coupant l'intervalle en deux à chaque étape : 500, puis 750 ou 250, etc.), le nombre maximum d'étapes nécessaires pour trouver un nombre parmi $N$ est $\lceil \log_2(N) \rceil$.  
> Pour $N = 1000$ :  
> $2^{10} = 1024 > 1000 \implies$ **10 essais suffisent toujours mathématiquement pour gagner !**  
> Il s'agit d'un algorithme de complexité logarithmique $O(\log n)$.

### Code PHP avec limite d'essais

```php
<?php
const MAX_ESSAIS = 10;
$nombreADeviner = rand(1, 1000);
$essais = 0;
$trouve = false;

echo "--- Devinez le nombre entre 1 et 1000 (Vous avez " . MAX_ESSAIS . " essais) ---" . PHP_EOL;

while ($essais < MAX_ESSAIS && !$trouve) {
    $restants = MAX_ESSAIS - $essais;
    echo PHP_EOL . "Essai " . ($essais + 1) . " / " . MAX_ESSAIS . " (il vous reste $restants essai(s))" . PHP_EOL;

    $saisie = readline("Votre proposition : ");
    $nombrePropose = filter_var($saisie, FILTER_VALIDATE_INT);

    if ($nombrePropose === false || $nombrePropose < 1 || $nombrePropose > 1000) {
        echo "Saisie invalide, entrez un entier entre 1 et 1000." . PHP_EOL;
        continue;
    }

    $essais++;

    if ($nombrePropose > $nombreADeviner) {
        echo "C'est moins !" . PHP_EOL;
    } elseif ($nombrePropose < $nombreADeviner) {
        echo "C'est plus !" . PHP_EOL;
    } else {
        $trouve = true;
    }
}

echo PHP_EOL . "================ RESULTAT ================" . PHP_EOL;
if ($trouve) {
    echo "Félicitations ! Vous avez trouvé $nombreADeviner en $essais essai(s) !" . PHP_EOL;
} else {
    echo "Perdu ! Vous avez épuisé vos " . MAX_ESSAIS . " essais." . PHP_EOL;
    echo "Le nombre secret était : $nombreADeviner" . PHP_EOL;
}
```

---

## 5. Pour aller plus loin : Gestion du meilleur score (Record de session)

On peut conserver en mémoire le record du joueur (le nombre minimal d'essais pour gagner) au fil des parties successives :

```php
<?php
$jouer = "O";
$meilleurScore = null; // null au début car aucune victoire enregistrée

while (strtoupper(trim($jouer)) === "O") {
    $nombreADeviner = rand(1, 1000);
    $essais = 0;

    echo PHP_EOL . "=== NOUVELLE PARTIE ===" . PHP_EOL;
    if ($meilleurScore !== null) {
        echo "Record actuel à battre : $meilleurScore essai(s)" . PHP_EOL;
    }

    do {
        $proposition = (int) readline("Nombre proposé (1-1000) ? ");
        $essais++;

        if ($proposition > $nombreADeviner) {
            echo "Trop grand" . PHP_EOL;
        } elseif ($proposition < $nombreADeviner) {
            echo "Trop petit" . PHP_EOL;
        }
    } while ($proposition !== $nombreADeviner);

    echo "Gagné en $essais essai(s) !" . PHP_EOL;

    // Mise à jour du meilleur score
    if ($meilleurScore === null || $essais < $meilleurScore) {
        $meilleurScore = $essais;
        echo "Nouveau record de session établi : $meilleurScore essai(s) !" . PHP_EOL;
    }

    $jouer = readline("Voulez-vous rejouer ? (O/N) : ");
}

echo "Partie terminée. Meilleur score de la session : " . ($meilleurScore ?? "Aucun") . PHP_EOL;
```
