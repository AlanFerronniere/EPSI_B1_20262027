# Guide d'utilisation — Serveur de Développement PHP

Bienvenue sur votre serveur de développement pour l'année B1. Ce serveur vous permet de développer vos projets PHP / MySQL, de tester votre code en conditions réelles sur un serveur Linux et de le rendre accessible sur le Web.

---

## 1. Vos URLs et Espaces de Travail

Chaque étudiant et chaque groupe de projet dispose d'une URL publique dédiée :

* **Format de l'URL** : `https://<votre_login>.b1.latetedanslephp.fr`
* **Exemple individuel** : `https://alexandre.b1.latetedanslephp.fr`
* **Exemple projet** : `https://groupe-ifrocean-1.b1.latetedanslephp.fr` *(en HTTPS, utiliser les tirets `-` plutôt que les underscores `_`)*

> [!NOTE]
> Vos identifiants individuels (login, mot de passe SSH, mot de passe BDD) vous ont été transmis par votre formateur. Vous les retrouverez également à tout moment dans votre dossier personnel sur le serveur, dans le fichier `~/MES_ACCES.txt`.

---

## 2. Connexion et Environnement de Développement

Le serveur est accessible depuis l'adresse dédiée :
```
serveur.b1.latetedanslephp.fr
```

---

### Méthode 1 : Avec PhpStorm — *(Recommandé)*

PhpStorm propose deux excellentes manières de travailler avec le serveur :

#### Option A : Déploiement SFTP automatique *(La méthode la plus fluide)*
Vous travaillez sur vos fichiers en local sur votre PC et PhpStorm synchronise automatiquement votre code sur le serveur à chaque sauvegarde (`Ctrl+S`) :

1. Dans PhpStorm, ouvrez votre projet local (ou créez un nouveau projet).
2. Rendez-vous dans **Tools** $\rightarrow$ **Deployment** $\rightarrow$ **Configuration...** (ou `Settings` $\rightarrow$ `Build, Execution, Deployment` $\rightarrow$ `Deployment`).
3. Cliquez sur le **`+`** en haut à gauche et choisissez **SFTP**.
4. Donnez un nom (ex: `Serveur Dev`) puis configurez la connexion :
   * **SSH configuration** : cliquez sur les `...` pour créer une configuration SSH :
     * **Host** : `serveur.b1.latetedanslephp.fr`
     * **Port** : `22`
     * **User name** : `<votre_login>`
     * **Authentication type** : `Password` (saisissez votre mot de passe SSH)
     * Testez la connexion avec le bouton **Test Connection**.
   * **Root path** : `/home/<votre_login>/public_html`
   * **Web server URL** : `https://<votre_login>.b1.latetedanslephp.fr`
5. Dans l'onglet **Mappings** :
   * **Local path** : dossier de votre projet sur votre PC
   * **Deployment path** : `/`
6. Activez la synchronisation automatique : **Tools** $\rightarrow$ **Deployment** $\rightarrow$ cochez **Automatic Upload (always)**.
7. Dès que vous enregistrez un fichier, il est immédiatement envoyé sur le serveur et visible sur votre URL web !

#### Option B : Développement à distance (Remote Development via SSH)
Pour exécuter PhpStorm directement sur le serveur :
1. Sur l'écran d'accueil de PhpStorm (ou `File` $\rightarrow$ `Remote Development...`), sélectionnez **SSH**.
2. Cliquez sur **New Connection** :
   * **Host** : `serveur.b1.latetedanslephp.fr`
   * **Port** : `22`
   * **User** : `<votre_login>`
3. Entrez votre mot de passe SSH.
4. Choisissez le répertoire de travail distant : `/home/<votre_login>/public_html`.
5. PhpStorm prépare l'environnement distant et vous ouvre votre projet directement sur le serveur.

---

### Méthode 2 : Avec Visual Studio Code (Remote - SSH)

1. Installez l'extension officielle **Remote - SSH** (par Microsoft) dans VS Code.
2. Ouvrez votre fichier de configuration SSH local :
   * Appuyez sur `F1` (ou `Ctrl+Shift+P`) $\rightarrow$ tapez `Remote-SSH: Open SSH Configuration File...` $\rightarrow$ choisissez votre fichier utilisateur (généralement `~/.ssh/config` ou `C:\Users\<vous>\.ssh\config`).
3. Ajoutez le bloc suivant :
   ```ssh-config
   Host toht-dev
       HostName serveur.b1.latetedanslephp.fr
       User <votre_login>
   ```
4. Appuyez sur `F1` $\rightarrow$ tapez `Remote-SSH: Connect to Host...` $\rightarrow$ sélectionnez `toht-dev`.
5. Entrez votre mot de passe lorsque demandé.
6. Une fois connecté, faites `Fichier` $\rightarrow$ `Ouvrir le dossier...` $\rightarrow$ sélectionnez `/home/<votre_login>/public_html`.

---

### Méthode 3 : En ligne de commande (Terminal / PowerShell / Git Bash)

Pour exécuter des commandes Linux, lancer des scripts CLI ou installer des dépendances :
```bash
ssh <votre_login>@serveur.b1.latetedanslephp.fr
```
Entrez votre mot de passe lorsque le serveur vous le demande (les caractères ne s'affichent pas, c'est normal).

---

## 3. Déposer et tester son code Web

Le répertoire web racine est :
```bash
~/public_html
```

* **Dossier de publication** : Déposez tous vos fichiers sources (`.php`, `.html`, `.css`, `.js`, images, etc.) dans ce dossier.
* **Point d'entrée** : Le fichier d'accueil par défaut doit s'appeler `index.php` (ou `index.html`).
* **Visualisation** : Dès qu'un fichier est enregistré dans `~/public_html`, il est instantanément accessible et exécuté en visitant votre URL :
  ```
  https://<votre_login>.b1.latetedanslephp.fr
  ```

---

## 4. Gestion de la Base de Données (MariaDB / MySQL)

Chaque compte dispose d'un accès dédié à MariaDB :

* **Hôte BDD** : `localhost` (ou `127.0.0.1`)
* **Utilisateur BDD** : `<votre_login>`
* **Mot de passe BDD** : *(votre mot de passe BDD transmis)*
* **Base principale** : `<votre_login>` *(avec un underscore `_` si votre login contient un tiret)*
* **Bases supplémentaires** : Vous pouvez créer librement de nouvelles bases de données dans MariaDB ou phpMyAdmin, à condition de préfixer leur nom par `<votre_login>_` (par exemple : `<votre_login>_blog`, `<votre_login>_ecommerce`, etc.).

### Interface Web phpMyAdmin

Pour administrer visuellement vos tables et données :
1. Rendez-vous sur :
   ```
   https://<votre_login>.b1.latetedanslephp.fr/phpmyadmin
   ```
2. Connectez-vous avec votre utilisateur MariaDB et votre mot de passe BDD.
3. Seules vos bases de données apparaîtront dans le panneau de gauche.

---

## 5. Exemple de connexion en PHP (PDO)

Voici le code standard recommandé pour vous connecter à votre base de données dans vos scripts PHP :

```php
<?php
// Configuration des accès
$host    = 'localhost';
$db      = 'VOTRE_BASE';        // Ex: 'maxime' ou 'groupe_ifrocean_1'
$user    = 'VOTRE_UTILISATEUR'; // Ex: 'maxime'
$pass    = 'VOTRE_MOT_DE_PASSE';
$charset = 'utf8mb4';

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";
$options = [
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_EMULATE_PREPARES   => false,
];

try {
    $pdo = new PDO($dsn, $user, $pass, $options);
    // echo "Connexion à la base de données réussie !";
} catch (\PDOException $e) {
    die("Erreur de connexion : " . $e->getMessage());
}
```

