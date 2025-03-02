# Symfony Project

Bienvenue dans le projet Symfony ! Ce fichier `README.md` fournit toutes les informations nécessaires pour configurer et démarrer l'application.

## Prérequis

Avant de commencer, assurez-vous que vous avez les éléments suivants installés sur votre machine :

- **PHP** (version 8.0 ou supérieure)
- **Composer** (pour gérer les dépendances PHP)
- **MySQL** ou tout autre serveur de base de données compatible
- **Symfony CLI** (facultatif mais recommandé)
- **Docker** et **Docker Compose** (pour la gestion des conteneurs)

## Installation

### 1. Cloner le projet

Clonez le dépôt Git du projet sur votre machine :

```bash
git clone git@github.com:loicosternaud/symfony-project.git
cd symfony-project
```

### 2. Installer les dépendances

Une fois le projet cloné, utilisez Composer pour installer toutes les dépendances nécessaires :

```bash
composer install
```

### 3. Configurer l'environnement

Vous devez maintenant personnaliser la configuration de votre environnement local.

- Ouvrez le fichier `.env` et ajoutez les lignes suivantes :

  - **Base de données** : Ajoutez la ligne suivante pour configurer l'URL de votre base de données :

    ```env
    DATABASE_URL="mysql://db_user:password@127.0.0.1:3306/my_project_db"
    ```

    **Explication :**
    - `db_user` : nom d'utilisateur pour accéder à la base de données (par exemple, `root`).
    - `password` : mot de passe de l'utilisateur de la base de données.
    - `my_project_db` : nom de la base de données à utiliser.

  - **Clé secrète** (`APP_SECRET`) : Ajoutez la ligne suivante pour définir une clé secrète (cela est requis pour des fonctionnalités de sécurité, comme la gestion des sessions et des cookies) :

    ```env
    APP_SECRET=your_secret_key_here
    ```

### 4. Configurer Docker

Si vous souhaitez utiliser Docker pour exécuter l'application, voici les étapes à suivre.

- **Modifier le fichier** `docker-compose.yml`

   Le fichier `docker-compose.yml` contient la configuration pour le service de base de données MySQL. Avant de démarrer Docker, vous devez modifier les valeurs suivantes dans ce fichier pour correspondre à vos informations de connexion :

    - `MYSQL_ROOT_PASSWORD` : mot de passe pour le super utilisateur root de la base de données.
    - `MYSQL_DATABASE` : nom de la base de données à créer.
    - `MYSQL_USER` : nom d'utilisateur pour se connecter à la base de données.
    - `MYSQL_PASSWORD` : mot de passe de l'utilisateur `MYSQL_USER`.

- **Lancer Docker**

Une fois que vous avez mis à jour le fichier `docker-compose.yml`, vous pouvez démarrer le service avec Docker en utilisant la commande suivante :

```bash
docker-compose up
```

Cela démarrera le conteneur MySQL dans un environnement Docker.

### 5. Créer la base de données

Une fois que vous avez configuré `.env`, vous pouvez créer la base de données avec la commande suivante :

```bash
php bin/console doctrine:database:create
```

### 6. Effectuer les migrations

Si des migrations doivent être appliquées pour créer ou mettre à jour les tables de la base de données, utilisez les commandes suivantes :

- Générer une migration :

  ```bash
  php bin/console make:migration
  ```

- Appliquer les migrations :

  ```bash
  php bin/console doctrine:migrations:migrate
  ```

### 7. Lancer le serveur Symfony

Si vous avez installé Symfony CLI, vous pouvez démarrer le serveur de développement avec :

```bash
symfony serve
```

Sinon, vous pouvez démarrer le serveur PHP intégré avec :

```bash
php -S 127.0.0.1:8000 -t public
```

Ensuite, ouvrez votre navigateur et accédez à `http://127.0.0.1:8000` pour voir l'application en fonctionnement.
