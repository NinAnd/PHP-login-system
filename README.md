# PHP-login-system
3. semester, Modul 2, opgave 2.

<?php
const DB_HOST = 'localhost';
const DB_USER = '';
const DB_PASS = '';
const DB_NAME = 'mademois_nin';

$conn = new mysqli(DB_HOST, DB_USER, DB_PASS, DB_NAME);
if ($conn->connect_error) { 
   die('Connect Error ('.$conn->connect_errno.') '.$connlink->connect_error);
}
$conn->set_charset('utf8'); 
?>
