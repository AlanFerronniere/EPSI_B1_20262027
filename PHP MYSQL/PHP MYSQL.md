# PHP & MySQL

## Objectifs du cours

Ce module fait le pont entre les précédents apprentissages :
- **HTML / CSS** : structurer et styliser les pages web.
- **Algorithmique** : variables, conditions, boucles, fonctions et logique de traitement.

L'objectif est d'utiliser **PHP** pour dynamiser vos pages web côté serveur, puis **MySQL** pour stocker et manipuler des données de manière persistante (en s'appuyant sur la modélisation de bases de données).

---

## Configuration de départ

Il vous faut sur votre machine :
- L'IDE **PhpStorm** : [Télécharger PhpStorm](https://www.jetbrains.com/fr-fr/phpstorm/download/)
- L'environnement PHP / serveur local :
  - Sur Windows : [[GUIDE_ELEVES_WINDOWS_XAMPP_XDEBUG]]
  - Sur macOS : [[GUIDE_ELEVES_MAC_PHP_XDEBUG]]

---

## Code du cours

Le dépôt GitHub officiel contenant le code des séances et les projets pratiques est disponible ici :
👉 **[AlanFerronniere/PHP_MYSQL_20262027](https://github.com/AlanFerronniere/PHP_MYSQL_20262027)**

---

## Introduction & Historique de PHP

### Qu'est-ce que PHP ?
PHP est un langage de script open source exécuté **côté serveur** (*backend*). Contrairement au HTML et au CSS interprétés directement par le navigateur client, le code PHP est exécuté sur le serveur web : il produit du HTML qui est ensuite envoyé au navigateur.

Site officiel : [php.net](https://www.php.net/) (et [documentation officielle en français](https://www.php.net/manual/fr/)).

### Bref historique
- **1994 - Création par Rasmus Lerdorf** : à l'origine, Rasmus Lerdorf crée un ensemble de scripts en langage C pour suivre les visiteurs sur son CV en ligne. Le projet est alors baptisé **PHP** pour *« Personal Home Page Tools »*.
- **1997 - PHP 3 et le moteur Zend** : Andi Gutmans et Zeev Suraski réécrivent le moteur d'exécution, donnant naissance à la base du moteur **Zend Engine**. Le sigle devient un acronyme récursif : **PHP: Hypertext Preprocessor**.
- **Années 2000 - PHP 4 et PHP 5** : PHP s'impose comme le langage roi du web dynamique grâce à sa simplicité d'intégration au HTML, le support étendu de MySQL et l'arrivée d'un modèle objet complet (avec PHP 5 en 2004).
- **2015 - PHP 7** : refonte majeure du moteur (*PHPNG*), doublement des performances et réduction de la consommation mémoire.
- **2020+ - PHP 8.x (version actuelle)** : introduction du compilateur JIT (*Just-In-Time*), du typage strict et moderne (types d'union, attributs, constructeurs promus), renforçant la robustesse et la rapidité du langage.

Aujourd'hui, PHP propulse près de 75% des sites web mondiaux (notamment via des CMS comme WordPress ou des frameworks professionnels comme Symfony et Laravel).

---

## Fonctionnement de base

### 1. Intégration de PHP dans une page web
Le code PHP s'insère directement dans un document à l'aide des balises `<?php ... ?>`.

```php
<!doctype html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Mon premier script PHP</title>
</head>
<body>
    <h1>Bonjour</h1>
    <p>Nous sommes le : <?php echo date('d/m/Y H:i:s'); ?></p>
</body>
</html>
```

### 2. Modularité : découper ses pages
Pour éviter de dupliquer les en-têtes et les pieds de page, PHP propose les instructions `include` et `require` :

```php
<?php
$title = "Accueil de la photothèque";
include("header.php");
?>

<main>
    <h1>Contenu principal</h1>
</main>

<?php
include("footer.php");
?>
```

### 3. Premiers projets pratiques
- **Exemples simples** : manipulation des dates, conditions (`if`, `elseif`, `else`) et affichage dynamique.
- **Projet Photothèque** : exploration de répertoires avec `scandir()`, vérification avec `is_dir()` et génération dynamique de liens de navigation avec passage de paramètres d'URL (`dossier.php?dossier=...`).
