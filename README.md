# Guide d'installation, de désinstallation et d'utilisation de Tomcat 9
## Table de matiere
- [Ubuntu](#ubuntu)
    - [Installation](#installation-sous-ubuntu)
    - [Désinstallation](#désinstallation-sous-ubuntu)
- [Windows 11](#windows-11)
    - [Installation](#installation)
    - [Désinstallation](#désinstallation)
- [Utilisation](#utilisation)
## Ubuntu
### Installation sous ubuntu

- Installer Java :
Tomcat nécessite Java pour fonctionner. 

- Installez OpenJDK :
```bash
    sudo apt update
    sudo apt install openjdk-17-jdk
```

- Télécharger Tomcat :
Téléchargez la dernière version de Tomcat 9 :
```bash
    wget https://downloads.apache.org/tomcat/tomcat-9/v9.0.65/bin/apache-tomcat-9.0.65.tar.gz
```

- Extraire l'archive :
```bash
    tar xzf apache-tomcat-9.0.65.tar.gz
```

- Déplacer Tomcat vers le répertoire `/Documents` :
```bash
    sudo mv apache-tomcat-9.0.65 /Documents/
```

- Définir les permissions :
```bash
    chmod +x /Documetns/apache-tomcat-9.0.65/bin/*.sh
```

- Créer un fichier de service Systemd :
```bash
    sudo nano ~/.bashrc
    ource ~/.bashrc
```

- Ajoutez le contenu suivant :
```ini
    export CATALINA_HOME=~/Documents/apache-tomcat-9.0.65
    export PATH=$PATH:$CATALINA_HOME/bin
```

- Recharger Systemd et démarrer Tomcat :
```bash
    startup.sh
```

- Vérifier l'installation :
Ouvrez votre navigateur et allez sur http://localhost:8080.

### Désinstallation sous ubuntu
- Arrêter le service Tomcat :
```bash
    shutdown.sh
```
- Supprimer les fichiers Tomcat :
```bash
    sudo rm -rf /Documetns/apache-tomcat-9.0.65/
```

## Windows 11
### Installation
- Installer Java :
Téléchargez et installez Java depuis le site Oracle.

- Télécharger Tomcat :
Téléchargez la dernière distribution binaire de Tomcat 9 depuis le site Apache Tomcat.

- Extraire l'archive :
Extrayez le fichier ZIP téléchargé dans un répertoire souhaité (par exemple, `C:\Tomcat`).

- Définir les variables d'environnement :
    - Ouvrez le Menu Démarrer et cherchez `Variables d'environnement`.
    - Cliquez sur `Modifier`.
    - Dans la fenêtre Propriétés Système, cliquez sur `Variables d'environnement`.
    - Sous `Variables système`, cliquez sur `Nouveau` et créez une nouvelle variable `CATALINA_HOME` avec la valeur définie sur le répertoire Tomcat (par exemple, `C:\Tomcat`).
    - De même, créez ou mettez à jour la variable `JAVA_HOME` pour pointer vers le répertoire d'installation de Java (par exemple, `C:\Program Files\Java\jdk-17.0.10`).

- Démarrer Tomcat :
    - Accédez au répertoire `C:\Tomcat\bin`.
    - Double-cliquez sur `startup.bat`.

- Vérifier l'installation :
    - Ouvrez votre navigateur et allez sur http://localhost:8080.

### Désinstallation

- Arrêter Tomcat :
    - Accédez au répertoire `C:\Tomcat\bin`.
    - Double-cliquez sur `shutdown.bat`.

- Supprimer le répertoire Tomcat :
    - Supprimez le répertoire `C:\Tomcat`.

- Supprimer les variables d'environnement :
    - Ouvrez le Menu Démarrer et cherchez `Variables d'environnement`.
    - Cliquez sur `Modifier`.
    - Dans la fenêtre Propriétés Système, cliquez sur `Variables d'environnement`.
    - Sous `Variables système`, trouvez et supprimez la variable `CATALINA_HOME`.
    - Optionnellement, si elle n'est pas utilisée par d'autres programmes, supprimez la variable `JAVA_HOME`.

## Utilisation

- Déployer une application web :
    - Copiez le fichier `WAR` de votre application dans le répertoire webapps de votre répertoire d'installation Tomcat.
    - Tomcat déploiera automatiquement l'application.

- Accéder au gestionnaire de Tomcat :
    - Ouvrez votre navigateur et allez sur http://localhost:8080/manager/html.
    - Connectez-vous en utilisant les identifiants par défaut (généralement définis dans le fichier `tomcat-users.xml`situé dans le répertoire conf).

- Surveiller et gérer les applications :
    - Utilisez le gestionnaire Tomcat pour démarrer, arrêter et gérer les applications déployées.