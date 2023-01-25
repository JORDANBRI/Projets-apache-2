# Installer un serveur LAMP sur Debian 11  

LAMP est l'acronyme de Linux, Apache, MySQL et PHP. C'est un package d'applications très utilisé permettant de mettre en place des serveurs web simplement. Il existe également pour Windows (WAMP) et Mac OS (MAMP). Ici, nous allons vous montrer comment nous avons installés un serveur LAMP sur une machine équipée de Debian 11.  

## Prérequis  
- Avant de commencer, il est nécessaire de disposer des privilèges root sur votre machine Debian 11.  

## Installation d'Apache2 
- Tout d'abord, nous allons installer Apache2 en utilisant cette commande :   

``` apt install apache2  ```  

- Une fois que le paquet est installé, on doit configurer Apache2 afin qu'il démarre au démarrage de notre serveur : 

 ```  systemctl enable apache2  ```  

- Vous pouvez ensuite démarrer Apache2 :

 ```  systemctl start apache2  ```  

- Il est recommandé de vérifier qu'Apache2 est bien lancé et fonctionnel en exécutant la commande suivante :

  ```  systemctl status apache2  ```  

## Installation de MySQL  

- Ensuite, nous allons installer MariaDB en utilisant la commande suivante :  

```  apt install mariadb-server  ```  

- Afin de sécuriser un peu plus notre installation fraiche de MariaDB, j'ai exécuté le script suivant :

``` mariadb-secure-installation```

- Il permet d'effectuer simplement des taches importantes tel qu'empêcher un utilisateur anonyme de se connecter a la base de données, retirer la possibilité d'accéder au root à distance, etc.

- Il est recommandé de vérifier le bon fonctionnement de MariaDB en se connectant à l'instance a l'aide de cette commande :

  ```  mariadb -u root -p  ```  

## Installation de PHP

- Enfin, passons a l'installation de PHP. Lorsque l'on installe PHP avec la commande suivante  ``` apt install php  ```, Des paquets additionnels tels que ``` libapache2-mod-php7.4  ``` s'installent en même temps. C'est par exemple ce paquet qui permet l'intégration de PHP avec Apache2.

- Afin de vérifier la bonne installation de PHP, nous allons créer un fichier test a la racine de notre serveur Web ayant pour but de nous donner des informations sur la configuration de PHP. Le bon affichage de cette page dite **phpinfo** confirme la bonne installation de PHP.

Note : Il est important de préciser que j'ai suivi [ce](https://www.it-connect.fr/installer-un-serveur-lamp-linux-apache-mariadb-php-sous-debian-11/) tutoriel afin de mener à bien mon installation.
