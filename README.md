# PHP-login-system
3. semester, Modul 2, opgave 2.

<?php
session_start();
if( isset($_SESSION['user_id']) ){
	header("Location: /");
}
require 'database.php';
if(!empty($_POST['user']) &&  !empty($_POST['password'])):
	
	$records = $conn->prepare('SELECT id,user,email,password FROM cphlogin_users WHERE name = :name');
	$records->bind_param(':user', $_POST['user']);
	$records->execute();
	$results = $records->fetch(PDO::FETCH_ASSOC);
	$message = '';
	if(count($results) > 0 && password_verify($_POST['password'], $results['password']) ){
		$_SESSION['user_id'] = $results['id'];
		header("Location: /");
	} else {
		$message = 'Beklager, men kodeordene er ikke ens.';
	}
endif;
?>

<!DOCTYPE html>
<html>
<head>
	<title>Log ind</title>
</head>
<body>

	<a href="index.php">Tilbage til forsiden</a>

	<?php if(!empty($message)): ?>
		<p><?= $message ?></p>
	<?php endif; ?>

	<form action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>" method="POST">
		<fieldset>
        	<legend>Log ind</legend>
            <input type="text" placeholder="Brugernavn" name="name"><br>
            <input type="password" placeholder="Kodeord" name="password"><br>
			<input type="submit">
		</fieldset>
	</form>

	<span>Gå til <a href="registerform.php">Opret bruger</a></span>
</body>
</html>
