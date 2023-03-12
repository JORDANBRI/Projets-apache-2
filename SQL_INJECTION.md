Qu'est-ce qu'une attaque par injection SQL ?
==
Une attaque par injection SQL (SQLi) est une technique d'attaque informatique qui consiste à exploiter une vulnérabilité de sécurité dans une application web pour injecter des instructions SQL malveillantes dans une base de données. Les attaquants peuvent utiliser cette technique pour accéder et modifier des données sensibles dans la base de données, voler des informations d'identification, exécuter des commandes à distance sur le serveur ou même prendre le contrôle complet de l'application web.

En général, les attaques par injection SQL sont possibles lorsque les entrées utilisateur ne sont pas correctement validées ou nettoyées avant d'être envoyées à la base de données. Les développeurs d'applications web peuvent prévenir les attaques par injection SQL en utilisant des techniques telles que la préparation de requêtes SQL, la validation des entrées utilisateur, l'utilisation de pare-feu d'applications web et la mise à jour régulière de leurs systèmes.

Exemple d'attaque de type injection SQL
Supposons que nous disposons d'un serveur LAN Apache 2 avec une configuration par défaut d'une base de données MariaDB et d'un formulaire écrit en HTML pour la partie statique et en PHP pour la partie dynamique (sans protection particulière).

Voici un extrait du code PHP pour insérer les données du formulaire dans la base de données :

php
```

// Récupérer les informations saisies dans le formulaire
$nom = $_POST['nom'];
$prenom = $_POST['prenom'];
$email = $_POST['email'];

// Préparer la requête SQL pour insérer les données dans la table 'information'
$sql = "INSERT INTO information (nom, prenom, email) VALUES ('$nom', '$prenom', '$email')";

```

On peut constater que les informations entrées par l'utilisateur ne subissent aucune vérification ou modification.


Supposons que l'utilisateur entre à la place de prénom la commande suivante : ``` '; DROP TABLE information';--  ```

Si un utilisateur entre la commande suivante en tant que prénom: ``` '; DROP TABLE information';--, ``` cela entraînerait l'exécution d'une injection SQL. La commande résultante serait:

```
Copy code
INSERT INTO information (nom, prenom, email) VALUES ('', ''; DROP TABLE information;--', '')

```
Le double tiret (--) indique que le reste de la requête SQL doit être ignoré. Cette commande supprimerait la table "information" de la base de données.

Comment se protéger contre les attaques par injection SQL ?
==
Voici quelques mesures de sécurité de base que vous pouvez mettre en place pour protéger votre application contre les attaques par injection SQL :

- Utilisez des requêtes préparées ou des paramètres de requête pour empêcher les entrées utilisateur d'être interprétées comme des instructions SQL. Les requêtes préparées sont des requêtes SQL qui sont précompilées et stockées dans la mémoire du serveur. Les paramètres de requête sont des valeurs qui sont passées à la requête SQL à l'aide d'une API de base de données.
- Échappez les caractères spéciaux dans les entrées utilisateur avant de les utiliser dans des instructions SQL. Vous pouvez utiliser des fonctions d'échappement telles que mysqli_real_escape_string() en PHP.




Mesures de sécurité supplémentaires
==
En plus des mesures de sécurité de base, il existe plusieurs autres mesures que vous pouvez prendre pour renforcer la sécurité de votre application contre les attaques par injection SQL :

- Limitez l'accès à la base de données : Limitez l'accès à la base de données uniquement aux utilisateurs qui en ont besoin pour effectuer leur travail. En outre, assurez-vous que les utilisateurs ont les privilèges les plus faibles nécessaires pour effectuer leurs tâches.

- Mise à jour régulière de votre application et des composants tiers : Les mises à jour régulières de votre application et de ses composants tiers (comme les bibliothèques) peuvent résoudre les vulnérabilités connues et améliorer la sécurité globale de votre application.

- Utilisez un pare-feu d'application Web (WAF) : Les pare-feu d'application Web peuvent détecter et bloquer les attaques par injection SQL avant qu'elles n'atteignent votre application. Les WAF peuvent être configurés pour filtrer les entrées utilisateur malveillantes, pour bloquer les adresses IP suspectes et pour empêcher les attaques par déni de service.

- Effectuez une analyse de vulnérabilité régulière : Effectuez régulièrement des analyses de vulnérabilité pour détecter les vulnérabilités de sécurité dans votre application et prendre les mesures nécessaires pour les corriger.

- Restreindre les permissions du serveur : Réduire les permissions du serveur sur lequel est installé votre application web peut réduire l'impact des attaques par injection SQL. Cela peut être fait en utilisant des utilisateurs et des groupes d'utilisateurs distincts avec des permissions limitées sur le serveur.

Conclusion
==
Les attaques par injection SQL sont une menace pour les applications web qui utilisent des bases de données pour stocker des données. Les développeurs d'applications web peuvent prévenir les attaques par injection SQL en utilisant des techniques telles que la préparation de requêtes SQL, la validation des entrées utilisateur, l'utilisation de pare-feu d'applications web et la mise à jour régulière de leurs systèmes. En outre, les utilisateurs peuvent protéger leurs données en ne fournissant pas d'informations personnelles sensibles à des applications web non fiables et en utilisant des mots de passe forts et différents pour chaque application.
