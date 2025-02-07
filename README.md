# WordPressServer
Dockerized Wordpress server deployed on EC2 with RDS/EFS background

#To be inserted into wp-config.php file for SSL routing
#if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
     $_SERVER['HTTPS'] = 'on';
