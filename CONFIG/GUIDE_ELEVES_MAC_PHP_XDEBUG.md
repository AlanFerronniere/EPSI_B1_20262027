# Guide pour les élèves sur Mac : Environnement PHP & Xdebug

Ce guide est spécialement conçu pour les élèves travaillant sous **macOS** (MacBook Air / Pro avec puces Apple Silicon M1/M2/M3/M4 ou processeurs Intel).

---

## ⚠️ Pourquoi éviter XAMPP sur Mac ?

Sous Windows, XAMPP s'installe directement sur le système. Mais sous macOS :
- XAMPP tourne souvent dans une **machine virtuelle émulée** (XAMPP-VM).
- Cela crée une adresse IP virtuelle séparée (`192.168.64.2`), rendant la communication entre Xdebug (dans la VM) et votre éditeur de code (sur votre Mac) complexe et instable.
- Le partage de fichiers entre le Mac et la VM ralentit l'affichage.

👉 **La solution recommandée et professionnelle sous macOS :** installer PHP nativement via **Homebrew**. C'est léger, rapide et cela fonctionne parfaitement avec VS Code et PhpStorm.

---

## Étape 1 : Installer Homebrew (le gestionnaire de paquets de macOS)

1. Ouvrez l'application **Terminal** sur votre Mac (via Spotlight : `Cmd + Espace` -> tapez `Terminal`).
2. Copiez-collez la commande suivante et appuyez sur Entrée :
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```
3. Suivez les instructions à l'écran (votre mot de passe Mac vous sera demandé, il ne s'affiche pas pendant la frappe, c'est normal).
4. *Important pour les Mac récents (Apple Silicon) :* À la fin de l'installation, le terminal affiche 2 ou 3 commandes à copier pour ajouter Homebrew à votre chemin. Copiez-les et exécutez-les.

---

## Étape 2 : Installer PHP

Dans le terminal, lancez simplement :
```bash
brew install php
```

Une fois terminé, vérifiez que PHP est bien accessible :
```bash
php -v
```
Vous devez voir la version de PHP installée (ex : `PHP 8.3.x` ou `PHP 8.4.x`).

---

## Étape 3 : Installer Xdebug en une commande

Homebrew inclut l'utilitaire `pecl`. Pour installer Xdebug, tapez :
```bash
pecl install xdebug
```

Le Mac va compiler automatiquement la version exacte de Xdebug adaptée à la puce de votre machine.

---

## Étape 4 : Activer et configurer Xdebug

### 1. Trouver le fichier `php.ini`
Tapez la commande :
```bash
php --ini
```
Repérez la ligne `Loaded Configuration File`. Le chemin ressemble généralement à :
- `/opt/homebrew/etc/php/8.x/php.ini` (Mac Apple Silicon M1/M2/M3/M4)
- `/usr/local/etc/php/8.x/php.ini` (Mac Intel)

### 2. Ouvrir le fichier
Ouvrez-le dans l'éditeur de votre choix ou avec TextEdit :
```bash
open -e $(php -r "echo php_ini_loaded_file();")
```

### 3. Ajouter la configuration Xdebug
Allez à la toute fin du fichier et ajoutez les lignes suivantes :

```ini
[xdebug]
; Active le débogage pas-à-pas et l'affichage des erreurs détaillé
xdebug.mode = debug,develop

; Démarre automatiquement la session de débogage
xdebug.start_with_request = yes

; Port standard de communication avec l'IDE
xdebug.client_host = localhost
xdebug.client_port = 9003
```

> [!NOTE]
> La commande `pecl install xdebug` a déjà inséré automatiquement la ligne `zend_extension="xdebug.so"` au tout début de votre fichier `php.ini`. Il suffit donc d'ajouter le bloc ci-dessus.

Enregistrez (`Cmd + S`) et fermez le fichier.

---

## Étape 5 : Vérifier que Xdebug fonctionne

Dans votre terminal, relancez :
```bash
php -v
```
Vous devez voir la ligne Xdebug :
```text
with Xdebug v3.x.x, Copyright (c) 2002-2026, by Derick Rethans
```

---

## Étape 6 : Travailler sur vos projets (Serveur local)

Sous Mac, pas besoin d'Apache pour tester vos TP ! PHP possède un serveur web intégré ultra-léger.

Dans le terminal, déplacez-vous dans le dossier de votre projet :
```bash
cd ~/Documents/mon_projet_php
php -S localhost:8000
```
Ouvrez votre navigateur sur : [http://localhost:8000](http://localhost:8000). Votre code s'exécute instantanément.

---

## Étape 7 : Configurer l'IDE

### Avec Visual Studio Code
1. Installez l'extension **PHP Debug** (par Xdebug / Felix Becker).
2. Dans le panneau de débogage (`Cmd + Shift + D`), cliquez sur **create a launch.json file** et choisissez **PHP**.
3. Le fichier créé écoute par défaut sur le port `9003`.
4. Placez un point d'arrêt (clic rouge dans la marge) dans votre fichier `.php`.
5. Appuyez sur **F5** (démarrer l'écoute), puis actualisez votre page sur `http://localhost:8000`. VS Code intercepte l'exécution !

### Avec PhpStorm
1. Allez dans **Settings** (`Cmd + ,`) -> **PHP**.
2. Dans **CLI Interpreter**, cliquez sur `...` et sélectionnez :
   - `/opt/homebrew/bin/php` (sur Apple Silicon)
   - `/usr/local/bin/php` (sur Intel)
3. Cliquez sur l'icône de combiné téléphonique en haut à droite (*Start Listening for PHP Debug Connections*).
4. Actualisez votre page dans le navigateur.
