# PHP-login-system
3. semester, Modul 2, opgave 2.

use mademois_nin;

CREATE TABLE cphlogin_users (
	id INT PRIMARY KEY auto_increment,
    user varchar(45) not null,
    email varchar(255) not null,
    password varchar(20) not null
)
