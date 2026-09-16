# Guide d'installation de PHP et Xdebug sur Windows

Ce guide présente les étapes pour installer **PHP** et l'extension **Xdebug** sous Windows. Deux méthodes d'installation de PHP sont décrites : la méthode rapide recommandée via **winget**, et la méthode **manuelle** par archive zip.

---

## Méthode 1 : Installation rapide avec `winget` (Recommandée)

Windows intègre désormais le gestionnaire officiel `winget`, qui télécharge, extrait et configure automatiquement les variables d'environnement.

### 1. Installer PHP via le terminal
Ouvrez un terminal (PowerShell) et lancez :
```powershell
winget install PHP.PHP.8.5
```
*(ou une version spécifique comme `PHP.PHP.8.4` selon vos besoins).*

### 2. Prise en compte du PATH
Fermez et rouvrez votre terminal pour recharger les variables d'environnement, puis vérifiez :
```powershell
php -v
```

L'installation se trouve généralement dans :
```text
%LOCALAPPDATA%\Microsoft\WinGet\Packages\PHP.PHP.8.x...
```

---

## Méthode 2 : Installation manuelle classique (Zip)

Si vous préférez installer PHP sans gestionnaire de paquets :

### 1. Prérequis : Visual C++ Redistributable
Téléchargez et installez le runtime officiel Microsoft :
- Lien direct (x64) : [vc_redist.x64.exe](https://aka.ms/vs/17/release/vc_redist.x64.exe)

### 2. Téléchargement et extraction
1. Rendez-vous sur [windows.php.net/download](https://windows.php.net/download).
2. Choisissez la variante :
   - **Architecture :** `x64`.
   - **Thread Safety :**
     - **Non-Thread Safe (NTS)** : Recommandé pour CLI seul, Nginx, FastCGI.
     - **Thread Safe (TS)** : Recommandé avec Apache (`mod_php`).
3. Extrayez l'archive Zip dans un dossier fixe, par exemple `C:\php`.

### 3. Ajout au PATH Windows
1. Appuyez sur `Win + R` -> tapez `sysdm.cpl` -> onglet **Paramètres système avancés** -> **Variables d'environnement**.
2. Modifiez la variable `Path` utilisateur ou système et ajoutez `C:\php`.
3. Validez et ouvrez un nouveau terminal pour vérifier avec `php -v`.

---

## Initialisation du fichier `php.ini`

Que vous ayez utilisé `winget` ou l'installation manuelle, un fichier `php.ini` doit être créé s'il n'existe pas encore :

1. Repérez le dossier d'installation de PHP :
   ```powershell
   (Get-Command php).Source
   ```
2. Dans ce dossier, copiez `php.ini-development` vers `php.ini` :
   ```powershell
   # Exemple dans le dossier d'installation :
   Copy-Item "php.ini-development" "php.ini"
   ```
3. Ouvrez `php.ini` et activez le répertoire des extensions en décommentant la ligne :
   ```ini
   ; On windows:
   extension_dir = "ext"
   ```

---

## Installation et configuration de Xdebug

Puisque winget ne fournit pas d'extension PECL préconfigurée sous Windows, Xdebug s'ajoute simplement en plaçant sa DLL.

### 1. Identifier votre version exacte de PHP
Dans un terminal, lancez :
```powershell
php -i | Select-String -Pattern "PHP Version|Thread Safety|Architecture|Compiler"
```
Relevez :
- **Version PHP** (ex : `8.5`)
- **Thread Safety** (`enabled` = **TS**, `disabled` = **NTS**)
- **Compilateur** (ex : `VS17`)
- **Architecture** (`x64`)

> [!TIP]
> Si vous utilisez PHP installé par winget, il s'agit généralement de la version **TS (Thread Safe) VS17 x64**.

### 2. Télécharger la DLL Xdebug
1. Rendez-vous sur [xdebug.org/download](https://xdebug.org/download) *(ou utilisez l'assistant [xdebug.org/wizard](https://xdebug.org/wizard))*.
2. Téléchargez le fichier DLL correspondant exactement à vos caractéristiques (ex : `php_xdebug-3.x.x-8.5-ts-vs17-x86_64.dll`).
3. Renommez-le en `php_xdebug.dll` et déplacez-le dans le dossier `ext` de votre PHP.

### 3. Activer Xdebug dans `php.ini`
Ajoutez à la fin de votre fichier `php.ini` :

```ini
[xdebug]
; Chargement de l'extension
zend_extension = xdebug

; Modes activés (debug pas-à-pas + aides au développement)
xdebug.mode = debug,develop

; Lancement de la session de debug à chaque requête
xdebug.start_with_request = yes

; Port de communication standard avec l'IDE
xdebug.client_host = localhost
xdebug.client_port = 9003
```

> [!WARNING]
> Toujours utiliser `zend_extension = xdebug` et jamais `extension = xdebug`.

---

## Vérification finale

Vérifiez que Xdebug est bien chargé par PHP :
```powershell
php -v
```
La sortie doit inclure la mention Xdebug :
```text
PHP 8.5.10 (cli) ...
    with Xdebug v3.5.3, Copyright (c) 2002-2026, by Derick Rethans
    with Zend OPcache v8.5.10, Copyright (c), by Zend Technologies
```

Et pour inspecter les directives détaillées :
```powershell
php --ri xdebug
```

---

## Configuration de l'IDE

- **PhpStorm** : Allez dans **Settings** (`Ctrl + Alt + S`) -> **PHP** -> configurez le CLI Interpreter sur l'exécutable `php.exe`. Dans **Debug**, confirmez le port `9003`, puis activez le bouton d'écoute (*"Start Listening for PHP Debug Connections"*).
- **VS Code** : Installez l'extension **PHP Debug**, créez un profil d'écoute sur le port `9003` dans `.vscode/launch.json`, puis lancez le débogueur (`F5`).
