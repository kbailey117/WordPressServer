# WordPressServer
Dockerized Wordpress server deployed on EC2 with RDS/EFS background

# VPC Setup
# Security Groups (EC2, Bastion, RDS, EFS, ALB)
# EC2 Bastion 
# Webserver (public hosted)
     #!/bin/bash
     sudo apt-get update -y
     sudo apt install docker.io -y
     sudo systemctl start docker
     sudo systemctl enable docker
     sudo apt install docker-compose -y
     sudo usermod -aG docker $USER
     
# SSH Setup through Bastion to Webserver
# Verification of Docker & Docker-Compose Installation
# Installation of Git and setup of SSH Keygen for GitHub repository pull
# Mount location of EFS
# EFS Setup
# RDS Setup
# ALB Setup
# Route 53 DNS Setup 


# To be inserted into wp-config.php file for SSL routing

if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
     $_SERVER['HTTPS'] = 'on';
}

