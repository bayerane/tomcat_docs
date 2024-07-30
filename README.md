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

- Déplacer Tomcat vers le répertoire `/opt` :
```bash
    sudo mv apache-tomcat-9.0.65 /opt/tomcat
```

- Définir les permissions :
```bash
    sudo chown -R $USER:$USER /opt/tomcat
    chmod +x /opt/tomcat/bin/*.sh
```

- Créer un fichier de service Systemd :
```bash
    sudo nano /etc/systemd/system/tomcat.service
```

- Ajoutez le contenu suivant :
```ini
    [Unit]
    Description=Apache Tomcat Web Application Container
    After=network.target

    [Service]
    Type=forking

    Environment=JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
    Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
    Environment=CATALINA_HOME=/opt/tomcat
    Environment=CATALINA_BASE=/opt/tomcat
    Environment='CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC'
    Environment='JAVA_OPTS=-Djava.awt.headless=true -Djava.security.egd=file:/dev/./urandom'

    ExecStart=/opt/tomcat/bin/startup.sh
    ExecStop=/opt/tomcat/bin/shutdown.sh

    User=tomcat
    Group=tomcat
    UMask=0007
    RestartSec=10
    Restart=always

    [Install]
    WantedBy=multi-user.target
```

- Recharger Systemd et démarrer Tomcat :
```bash
    sudo systemctl daemon-reload
    sudo systemctl start tomcat
    sudo systemctl enable tomcat
```

- Vérifier l'installation :
Ouvrez votre navigateur et allez sur http://localhost:8080.

### Désinstallation sous ubuntu
- Arrêter le service Tomcat :
```bash
    sudo systemctl stop tomcat
```

- Désactiver le service Tomcat :
```bash
    sudo systemctl disable tomcat
```

- Supprimer les fichiers Tomcat :
```bash
    sudo rm -rf /opt/tomcat
```

- Supprimer le fichier de service Systemd :
```bash
    sudo rm /etc/systemd/system/tomcat.service
```

- Recharger Systemd :
```bash
    sudo systemctl daemon-reload
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