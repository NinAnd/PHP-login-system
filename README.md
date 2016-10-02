# PHP-login-system
3. semester, Modul 2, opgave 2.

<?php
session_start();
require 'database.php';
if( isset($_SESSION['user_id']) ){
	$records = $conn->prepare('SELECT id, user, email,password FROM cphlogin_users WHERE id = :id');
	$records->bindParam(':id', $_SESSION['user_id']);
	$records->execute();
	$results = $records->fetch(PDO::FETCH_ASSOC);
	$user = NULL;
	if( count($results) > 0){
		$user = $results;
	}
}
?>

<!DOCTYPE html>
<html>
<head>
	<title>Ninettes hemmelighed</title>
</head>
<body>


	<?php if( !empty($user) ): ?>

		<br />Velkommen <?= $user['user']; ?> 
		<br /><br />Du er nu logget ind. Her er min hemmelighed... Jeg har meget svært ved at fosrtå PHP.
		<br /><br />
		<a href="logout.php">Logout?</a>

	<?php else: ?>

		<h1>Log ind og opdag min hemmelighed</h1>
		<a href="login.php">Log ind</a> eller
		<a href="registerform.php">Opret bruger</a>

	<?php endif; ?>

</body>
</html>
