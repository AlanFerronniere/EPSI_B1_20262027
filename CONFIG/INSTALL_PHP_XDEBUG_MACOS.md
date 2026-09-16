# Guide d'installation de PHP et Xdebug sur macOS

Ce guide présente les étapes pour installer et configurer **PHP** et l'extension **Xdebug** sous macOS (compatible processeurs Apple Silicon M1/M2/M3/M4 et processeurs Intel).

---

## Méthode 1 : Installation recommandée avec Homebrew (La plus simple)

Sous macOS, **Homebrew** est l'équivalent standard de `winget` sous Windows. C'est la méthode de référence pour gérer les versions de PHP et leurs extensions.

### 1. Prérequis : Xcode Command Line Tools et Homebrew

1. Installez les outils de compilation Apple si ce n'est pas déjà fait :
   ```bash
   xcode-select --install
   ```
2. Installez Homebrew (si vous ne l'avez pas déjà) :
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

### 2. Installer PHP via Homebrew

- **Pour installer la dernière version stable de PHP :**
  ```bash
  brew install php
  ```
- **Ou pour installer une version spécifique (ex: PHP 8.3 ou 8.4) :**
  ```bash
  brew install php@8.3
  brew link --force --overwrite php@8.3
  ```

Vérifiez ensuite la version active :
```bash
php -v
```

> [!NOTE]
> Sur Apple Silicon (M1/M2/M3/M4), Homebrew installe les fichiers dans `/opt/homebrew/`.  
> Sur les processeurs Intel, ils sont installés dans `/usr/local/`.

---

### 3. Installer Xdebug

Il existe deux manières simples d'installer Xdebug avec Homebrew :

#### Option A : Via PECL (Méthode officielle standard)
PECL est fourni directement avec le paquet PHP de Homebrew :
```bash
pecl install xdebug
```
*Cette commande compile automatiquement le module `xdebug.so` adapté à votre architecture (ARM64 ou x86_64).*

#### Option B : Via le tap Homebrew Shivam Mathur (Pratique pour versions spécifiques)
```bash
brew tap shivammathur/extensions
brew install shivammathur/extensions/xdebug@8.3  # remplacez par votre version PHP
```

---

## Configuration de `php.ini` sous macOS

### 1. Localiser le fichier `php.ini`
Pour trouver le chemin exact du fichier de configuration actif :
```bash
php --ini
```
La sortie indiquera l'emplacement du fichier principal, par exemple :
- Apple Silicon : `/opt/homebrew/etc/php/8.x/php.ini`
- Intel : `/usr/local/etc/php/8.x/php.ini`

### 2. Configurer Xdebug
Ouvrez le fichier `php.ini` (ou le fichier dédié `ext-xdebug.ini` dans le dossier `conf.d` s'il existe) :
```bash
nano $(php -r "echo php_ini_loaded_file();")
```

Ajoutez ou vérifiez la présence du bloc suivant à la fin du fichier :

```ini
[xdebug]
; Sur macOS, PECL ajoute souvent automatiquement la ligne zend_extension="xdebug.so".
; Si ce n'est pas le cas, ajoutez-la :
zend_extension = "xdebug.so"

; Modes activés : pas à pas et outils de développement
xdebug.mode = debug,develop

; Démarrer automatiquement le débogueur à chaque requête
xdebug.start_with_request = yes

; Hôte et port standard de communication avec l'IDE
xdebug.client_host = localhost
xdebug.client_port = 9003

; Journal de debug (optionnel, utile en cas d'erreur de connexion)
; xdebug.log = "/tmp/xdebug.log"
```

> [!WARNING]
> Sous macOS/Linux, l'extension est un fichier `.so` (`xdebug.so`), et non une `.dll` Windows.  
> Veillez à toujours utiliser la directive **`zend_extension`** et non `extension`.

---

## Méthode 2 : Compilation manuelle depuis les sources (Alternative sans Homebrew)

Si vous ne souhaitez pas utiliser de gestionnaire de paquets pour Xdebug :

1. Téléchargez le code source de Xdebug depuis [xdebug.org/download](https://xdebug.org/download) :
   ```bash
   curl -O https://xdebug.org/files/xdebug-3.x.x.tgz
   tar -xvzf xdebug-3.x.x.tgz
   cd xdebug-3.x.x
   ```
2. Préparez et compilez l'extension avec votre environnement PHP local :
   ```bash
   phpize
   ./configure
   make
   sudo make install
   ```
3. La commande `make install` vous indiquera le dossier d'installation de `xdebug.so` (par exemple `/usr/lib/php/extensions/...`).
4. Ajoutez la ligne `zend_extension="chemin_complet/xdebug.so"` dans votre `php.ini` ainsi que le bloc `[xdebug]`.

---

## Vérification de l'installation

1. Vérifiez que PHP charge bien Xdebug dans le terminal :
   ```bash
   php -v
   ```
   La réponse doit mentionner :
   ```text
   with Xdebug v3.x.x, Copyright (c) 2002-2026, by Derick Rethans
   ```

2. Inspectez les variables actives de Xdebug :
   ```bash
   php --ri xdebug
   ```

---

## Configuration de l'IDE sur macOS

### PhpStorm
1. Ouvrez les préférences : `Cmd + ,` -> **PHP**.
2. Dans **CLI Interpreter**, sélectionnez l'exécutable PHP :
   - `/opt/homebrew/bin/php` (sur Mac Apple Silicon)
   - `/usr/local/bin/php` (sur Mac Intel)
   PhpStorm détecte automatiquement la version et Xdebug.
3. Dans **PHP** -> **Debug**, vérifiez que le port Xdebug est configuré sur `9003`.
4. Cliquez sur l'icône de combiné téléphonique / écoute de debug en haut à droite (*"Start Listening for PHP Debug Connections"*).

### Visual Studio Code
1. Installez l'extension **PHP Debug** (par Xdebug / Felix Becker).
2. Dans le menu Débogage (`Cmd + Shift + D`), ajoutez la configuration standard dans `.vscode/launch.json` :
   ```json
   {
       "name": "Listen for Xdebug",
       "type": "php",
       "request": "launch",
       "port": 9003
   }
   ```
3. Placez un point d'arrêt dans votre script PHP et appuyez sur `F5`.
