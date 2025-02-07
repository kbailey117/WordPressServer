# WordPressServer
Dockerized Wordpress server deployed on EC2 with RDS/EFS background

# VPC Setup
# Security Groups (EC2, Bastion, RDS, EFS, ALB)
SSH -> Bastion
Bastion -> EC2 Server
HTTP -> ALB
EC2 Server -> ALB
RDS -> EC2 Server
EFS -> EC2 Server

# EC2 Bastion 
# EC2 Webserver (public hosted to avoid NAT Gateway costs)
     #!/bin/bash
     sudo apt-get update -y
     sudo apt install docker.io -y
     sudo systemctl start docker
     sudo systemctl enable docker
     sudo apt install docker-compose -y
     sudo usermod -aG docker $USER
     sudo mkdir -p /mnt/efs/wordpress
     sudo mkdir /mnt/efs/wordpress_data
     
# SSH Setup through Bastion to Webserver
     sudo scp -i "bastionkey.pem" "ec2privatekey.pem" user@bastion-private-ipv4dns:~/
# Verification of Docker & Docker-Compose Installation
     docker --version
     docker-compose --version
# SSH Keygen for GitHub repository pull
     ssh-keygen -t rsa -b 4096 -C "your_email_here@example.com"
     eval "$(ssh-agent -s)"
     ssh-add ~/.ssh/id_rsa
     cat ~/.ssh/id_rsa.pub | clip
     
# Clone repository
     cat /mnt/efs/wordpress
     git clone git@github.com:username/repository.git /mnt/efs/wordpress

# Mount location of EFS verification
     cat /mnt/efs/wordpress_data
     
# EFS Setup
     sudo apt install nfs-common -y
     sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport efs-name.efs.your-region-here.amazonaws.com:/ ~/mnt/efs/wordpress_data
     dh -f

     sudo nano /etc/fstab
     fs-04e6a6e06503c054a.efs.eu-central-1.amazonaws.com:/ /home/ubuntu/mnt/efs/wordpress_data nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport,_netdev 0 0
     
# RDS Setup
Create a MySQL RDS database and make sure the unique name is put into the .env file you cloned from repository.
# ALB Setup
Create target group for HTTP initially
# Route 53 DNS Setup 
Under your hosted zone, create a record and enable "Alias" option. Choose your endpoint, Region, and ensure you've selected your ALB.

# To be inserted into wp-config.php file for SSL routing
     if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') {
          $_SERVER['HTTPS'] = 'on';
     }

# SSL setup using ACM
Request a public certificate and use your domain name -- Ensure you create the CNAME records in Route53 -- Alter your ALB listening protocol to HTTPS using the previous target group -- Also set up an HTTP redirect protocol to HTTPS
