# Guide pour les élèves sur Windows : Installation de XAMPP & Xdebug

Ce guide détaille l'installation complète depuis zéro de **XAMPP** (Apache, PHP, MySQL/phpMyAdmin) sous Windows, ainsi que l'ajout et la configuration de l'extension **Xdebug**.

---

## Part 1 : Téléchargement et installation de XAMPP

### 1. Télécharger l'installateur
1. Rendez-vous sur le site officiel : [https://www.apachefriends.org/fr/index.html](https://www.apachefriends.org/fr/index.html).
2. Cliquez sur **XAMPP pour Windows** (choisissez la version la plus récente avec PHP 8.2 ou 8.3).

---

### 2. Pièges à éviter lors de l'installation

Lancez le fichier d'installation téléchargé (`xampp-windows-x64-...-installer.exe`).

#### Avertissement UAC (User Account Control)
Un message d'avertissement peut s'afficher concernant l'UAC de Windows :
- Cliquez sur **OK**. Cet avertissement rappelle simplement qu'il ne faut pas installer XAMPP dans le dossier `C:\Program Files` (car Windows y bloque les droits d'écriture).

#### Choix des composants
Dans l'écran **Select Components** :
- **Laissez cochés :** `Apache`, `MySQL`, `PHP`, `phpMyAdmin`.
- *(Optionnel)* Vous pouvez **décocher** les services inutiles pour vos cours : `FileZilla FTP Server`, `Mercury Mail Server`, `Tomcat`, `Perl`, `Fake Sendmail`.

#### Dossier d'installation (Très important !)
- Laissez le chemin par défaut : **`C:\xampp`**.
- Ne changez pas pour `C:\Program Files\xampp`.

#### Fin de l'installation & Pare-feu
1. Cliquez sur **Next** jusqu'à la fin de l'installation.
2. Lorsque Windows Defender / le pare-feu vous demande l'autorisation pour Apache et MySQL :
   - Cochez **Réseaux privés** (domicile ou travail).
   - Cliquez sur **Autoriser l'accès**.

---

## Part 2 : Premier démarrage et tests

1. Cochez la case pour ouvrir le **XAMPP Control Panel** à la fin de l'installation (ou cherchez `XAMPP Control Panel` dans le menu Démarrer).
2. Sur la ligne **Apache**, cliquez sur **Start** (le fond devient vert).
3. Sur la ligne **MySQL**, cliquez sur **Start** (le fond devient vert).
4. Ouvrez votre navigateur internet :
   - Tapez `http://localhost` ➔ La page d'accueil de XAMPP s'affiche.
   - Tapez `http://localhost/phpmyadmin` ➔ L'interface de gestion de base de données MySQL s'affiche.

> [!TIP]
> **En cas d'erreur de port (Apache ne démarre pas) :**  
> Si le port `80` ou `443` est déjà utilisé (souvent par IIS ou Skype) :
> - Dans le Control Panel, cliquez sur **Config** en face d'Apache ➔ **Apache (httpd.conf)**.
> - Remplacez `Listen 80` par `Listen 8080`.
> - Accédez ensuite à vos projets via `http://localhost:8080`.

---

## Part 3 : Où ranger vos projets ?

Tous vos fichiers de code PHP doivent être placés dans le dossier :
```text
C:\xampp\htdocs\
```
Par exemple, créez un sous-dossier :
```text
C:\xampp\htdocs\tp1\index.php
```
Et vous y accéderez dans votre navigateur via :
```text
http://localhost/tp1/index.php
```

---

## Part 4 : Installation de Xdebug

Pour pouvoir déboguer votre code avec des points d'arrêt dans VS Code ou PhpStorm :

### 1. Télécharger la bonne DLL Xdebug
1. Dans votre navigateur, ouvrez la page : [http://localhost/dashboard/phpinfo.php](http://localhost/dashboard/phpinfo.php).
2. Faites `Ctrl + A` puis `Ctrl + C` pour copier toute la page.
3. Allez sur **[xdebug.org/wizard](https://xdebug.org/wizard)**, collez le texte et cliquez sur **Analyse my phpinfo() output**.
4. L'outil vous propose un lien direct de téléchargement d'un fichier `.dll` (il s'agit de la version **TS - Thread Safe x64** correspondant à votre PHP XAMPP).
5. Téléchargez ce fichier.

### 2. Déplacer la DLL dans XAMPP
1. Renommez le fichier téléchargé en : **`php_xdebug.dll`**.
2. Déplacez-le dans le dossier des extensions de XAMPP :
   ```text
   C:\xampp\php\ext\
   ```

### 3. Activer Xdebug dans `php.ini`
1. Dans **XAMPP Control Panel**, sur la ligne **Apache**, cliquez sur **Config** ➔ **PHP (php.ini)**.
2. Le fichier s'ouvre dans le Bloc-notes.
3. Descendez **tout en bas** du fichier et collez ces lignes :

```ini
[xdebug]
zend_extension = "C:\xampp\php\ext\php_xdebug.dll"
xdebug.mode = debug,develop
xdebug.start_with_request = yes
xdebug.client_host = localhost
xdebug.client_port = 9003
```

4. Sauvegardez le fichier (`Ctrl + S`) et fermez le Bloc-notes.

### 4. Redémarrer Apache
1. Dans XAMPP Control Panel, cliquez sur **Stop** en face d'Apache, puis sur **Start**.
2. Retournez sur [http://localhost/dashboard/phpinfo.php](http://localhost/dashboard/phpinfo.php) et recherchez (`Ctrl + F`) le mot **xdebug**.
3. Si un bloc Xdebug s'affiche, c'est réussi !

---

## Part 5 : Déboguer avec votre éditeur de code

### Avec Visual Studio Code
1. Installez l'extension **PHP Debug** (par Felix Becker / Xdebug).
2. Ouvrez votre dossier de projet (ex: `C:\xampp\htdocs\tp1`) dans VS Code.
3. Allez dans l'onglet Débogage (`Ctrl + Shift + D`) ➔ cliquez sur **create a launch.json file** ➔ sélectionnez **PHP**.
4. Le fichier créé écoute sur le port `9003` par défaut.
5. Placez un point d'arrêt (rond rouge dans la marge) sur une ligne de votre code.
6. Appuyez sur **F5** pour lancer l'écoute du débogueur.
7. Chargez votre page dans le navigateur (`http://localhost/tp1/index.php`) : VS Code s'arrête automatiquement sur votre point d'arrêt !

### Avec PhpStorm
1. Allez dans **File** ➔ **Settings** (`Ctrl + Alt + S`) ➔ **PHP**.
2. Dans **CLI Interpreter**, cliquez sur `...` et ajoutez le chemin :
   ```text
   C:\xampp\php\php.exe
   ```
   PhpStorm affichera la version de PHP et confirmera la détection de Xdebug.
3. Cliquez sur l'icône de combiné téléphonique en haut à droite (*"Start Listening for PHP Debug Connections"*).
4. Actualisez votre page dans le navigateur.
