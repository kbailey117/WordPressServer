# WordPressServer
Dockerized Wordpress server deployed on Ubuntu EC2 with RDS background

# VPC Setup
Setup VPC with a CIDR block limitation of /26 | no NAT Gateway due to cost incursions | no S3 endpoint required | Enable DNS hostnames & resolution 
# Security Groups (EC2, Bastion, RDS, EFS, ALB)
   # Bastion Host: SSH into Bastion from host IP address
   # EC2: SSH from Bastion Security Group; IP4 traffic for port 8080; MySQL traffic for port 3306 from database Security Group; All traffic from ALB Security Group
   # ALB: 

# EC2 Bastion 
# EC2 Webserver (public subnet with temporary inbound HTTP access for GitHub repository access)
   
     sudo apt-get update -y
     sudo apt install docker.io -y
     sudo systemctl start docker
     sudo systemctl enable docker
     sudo apt install docker-compose -y
     sudo usermod -aG docker $USER
     
# SSH Setup through Bastion to Webserver
     sudo scp -i "bastionkey.pem" "ec2privatekey.pem" ubuntu@bastion-private-ipv4dns:~/
# Verification of Docker & Docker-Compose Installation
     docker --version
     docker-compose --version
   
# RDS Setup
Create a MySQL RDS database and make sure the unique name is put into the .env file you cloned from repository along with 
MySQL | Free-tier | Disable Autoscaling of storage | Modify the DB to use dualstack communication with EC2

# SSH Keygen for GitHub repository pull
     ssh-keygen -t rsa -b 4096 -C "your_email_here@example.com"
     eval "$(ssh-agent -s)"
     ssh-add ~/.ssh/id_rsa
     cat ~/.ssh/id_rsa.pub
     git clone git@github.com:username/repository.git

# ALB Setup
Create target group for HTTP
Set up security groups between EC2 and the ALB
# Route 53 DNS Setup 
Under your hosted zone, create an "A" record and enable "Alias" option. Choose your endpoint, Region, and ensure you've selected your ALB.

# SSL setup using ACM
Request a public certificate and use your domain name -- Ensure you create the CNAME records in Route53 -- Alter your ALB listening protocol to HTTPS using the previous target group -- Also set up an HTTP redirect protocol to HTTPS
