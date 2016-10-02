# PHP-login-system
3. semester, Modul 2, opgave 2.

<?php
session_start();
if( isset($_SESSION['user_id']) ){
	header("Location: /");
}

require 'database.php';
$message = '';
// if(!empty...) = hvis feltet er tomt...
// && betyder både og, altså at alle felter skal være udfyldt
if(!empty($_POST['user']) && !empty($_POST['email']) && !empty($_POST['password'])):
	
	// Den nye bruger lægges ind i databasen
	$sql = "INSERT INTO cphlogin_users (user, email, password) VALUES (:user, :email, :password)";
	$stmt = $conn->prepare($sql);
	// Brugernavn
	$stmt->bind_param(':user', $_POST['user']);
	// E-mail
	$stmt->bind_param(':email', $_POST['email']);
	// Kodeord - kodeordet bliver krypteret
	$stmt->bind_param(':password', password_hash($_POST['password'], PASSWORD_BCRYPT));
	if( $stmt->execute() ):
		$message = 'Din bruger er oprettet, du kan nu logge ind og opdage min hemmelighed.';
	else:
		$message = 'Beklager, men der opstod et problem under oprettelsen af ny bruger.';
	endif;
endif;
?>

<!DOCTYPE html>
<html>
<head>
	<title>Opret bruger</title>
</head>
<body>

	<a href="index.php">Tilbage til forsiden</a>

	<?php if(!empty($message)): ?>
		<p><?= $message ?></p>
	<?php endif; ?>

	<form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>" method="POST">
		<fieldset>
        	<legend>Opret bruger</legend>
            <input type="text" placeholder="Brugernavn" name="user"><br>
            <input type="text" placeholder="E-mail" name="email"><br>
            <input type="password" placeholder="Kodeord" name="password"><br>
            <input type="password" placeholder="Gentag kodeord" name="confirm_password"><br>
            <input type="submit">
		</fieldset>
	</form>
    
	<span>Gå til <a href="login.php">Log ind</a></span>

</body>
</html>
