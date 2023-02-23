## CRÉATION DU SITE

Pour créer un site web dynamique, nous aurons besoin d'un serveur web, d'un serveur de base de données et d'un langage de script côté serveur.

### Installation de Apache2

Apache2 est un serveur web populaire qui peut être utilisé pour héberger des sites web statiques et dynamiques. Voici comment l'installer sur Ubuntu :

```
sudo apt-get update
sudo apt-get install apache2
```

### Installation de MySQL

MySQL est un serveur de base de données relationnelle qui peut être utilisé pour stocker et récupérer des données. Voici comment l'installer sur Ubuntu :

```
sudo apt-get update
sudo apt-get install mysql-server
```

## CRÉATION DU FORMULAIRE EN HTML

Voici un exemple de formulaire d'enregistrement utilisateur en HTML :

```html
<!DOCTYPE html>
<html>
<head>
    <title>Formulaire d'enregistrement</title>
</head>
<body>
    <h2>Enregistrement utilisateur</h2>
    <form method="post" action="test.php">
        <label for="nom">Nom:</label>
        <input type="text" name="nom" required><br>

        <label for="prenom">Prénom:</label>
        <input type="text" name="prenom" required><br>

        <label for="email">Email:</label>
        <input type="email" name="email" required><br>

        <input type="submit" name="enregistrer" value="Enregistrer">
    </form>
</body>
</html>
```

Le formulaire utilise la méthode POST pour soumettre les données et l'action pointe vers un script PHP nommé "test.php".

### Ajout de pages web dans Apache2

Après avoir créé votre page web en HTML, vous pouvez l'ajouter au répertoire de votre site web. Par défaut, le répertoire pour les fichiers web est /var/www/html.

```bash
cd /var/www/html
sudo nano formulaire.html
```

Pour accéder à la page web à partir de votre navigateur, accédez à l'adresse IP de votre serveur ou à son nom de domaine. Par exemple, si l'adresse IP de votre serveur est 192.168.0.100, vous pouvez accéder à la page formulaire.html en entrant l'URL suivante dans votre navigateur :

```
http://192.168.0.100/formulaire.html
```

## CRÉATION DE LA PARTIE DYNAMIQUE DU SITE WEB EN PHP

Pour créer une partie dynamique de votre site web, vous pouvez utiliser PHP pour interagir avec une base de données et récupérer des données saisies dans le formulaire.

Voici un exemple de script PHP qui récupère les données saisies dans le formulaire d'enregistrement et les insère dans une table MySQL nommée "information".

```php
<?php
function connect() {
    // Les informations de connexion
    $host = "localhost";
    $username = "prodexamdb";
    $password = "Julolebro";
    $dbname = "blog";

    // La connexion à la base de données
    $conn = mysqli_connect($host, $username, $password, $dbname);

    // Vérifier si la connexion a réussi
    if (!$conn) {
        die("La connexion a échoué: " . mysqli_connect_error());
    }

    // Retourner l'objet de connexion
    return $conn;
}

// Connexion à la base de données
$conn = mysqli_connect("localhost", "prodexamdb", "Julolebro", "blog");

// Vérifier si la connexion a réussi
if (!$conn) {
    die("La connexion a échoué: " . mysqli_connect_error());
}

// Récupérer les informations saisies dans le formulaire
$nom = $_POST['nom'];
$prenom = $_POST['prenom'];
$email = $_POST['email'];

// Préparer la requête SQL pour insérer les données dans la table 'information'
$sql = "INSERT INTO information (nom, prenom, email) VALUES ('$nom', '$prenom', '$email')";

// Exécuter la requête SQL
if (mysqli_query($conn, $sql)) {
    echo "Enregistrement réussi";
} else {
    echo "Erreur: " . mysqli_error($conn);
}

// Fermer la connexion
mysqli_close($conn);
?>
```
N'oubliez pas de remplacer les informations de connexion par les vôtres dans la fonction connect().
