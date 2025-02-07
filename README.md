# WordPressServer
Dockerized Wordpress server deployed on EC2 with RDS/EFS background

# VPC Setup
# Security Groups (EC2, Bastion, RDS, EFS, ALB)
# EC2 Bastion and Webserver (public hosted)
# SSH Setup through Bastion to Webserver
# Installation of Docker
# Installation of Git and setup of SSH Keygen for GitHub repository pull
# Mount location of EFS
# EFS Setup
# RDS Setup
# ALB Setup
# Route 53 DNS Setup 


# To be inserted into wp-config.php file for SSL routing

if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
     $_SERVER['HTTPS'] = 'on';
