# WordPressServer
Dockerized Wordpress server deployed on EC2 with RDS/EFS background

# VPC Setup
# Security Groups (EC2, Bastion, RDS, EFS, ALB)
# EC2 Bastion 
# EC2 Webserver (public hosted)
     #!/bin/bash
     sudo apt-get update -y
     sudo apt install docker.io -y
     sudo systemctl start docker
     sudo systemctl enable docker
     sudo apt install docker-compose -y
     sudo usermod -aG docker $USER
     
# SSH Setup through Bastion to Webserver
# Verification of Docker & Docker-Compose Installation
# Verify Git Installation and setup of SSH Keygen for GitHub repository pull
# Mount location of EFS
     mkdir mnt/efs/wordpress_data
     cat mnt/efs/wordpress_data
     
# EFS Setup
     sudo apt install nfs-common -y
     sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport efs-name.efs.your-region-here.amazonaws.com:/ ~/mnt/efs/wordpress_data
# RDS Setup
# ALB Setup
# Route 53 DNS Setup 


# To be inserted into wp-config.php file for SSL routing

if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
     $_SERVER['HTTPS'] = 'on';
}

