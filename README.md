# devops-poc3

#Deploying a web application using Git, Jenkins, and Docker on an AWS EC2 Amazon Linux 2023 instance.

Prerequisites 

AWS EC2 instance (Amazon Linux 2023) 

Connecting to instance 

Internet connectivity

Installation Steps 

1. Update System Packages 

Sudo yum update –y 


2. Install Git 

sudo yum install git -y 
 

3. Install Docker 

sudo dnf install docker -y 
sudo systemctl start docker 
sudo systemctl enable docker 
sudo usermod -aG docker ec2-user 
 

Jenkins & Java Installation (Amazon Linux 2023) 

Step 1: Install OpenJDK 17 

sudo dnf install java-17-amazon-corretto -y 
java --version 
 

Step 2: Add Jenkins Repository & GPG Key 

sudo rpm --import https://pkg.jenkins.io/rpm-stable/jenkins.io-2026.key 

sudo tee /etc/yum.repos.d/jenkins.repo <<EOF 

[jenkins] 

name=Jenkins-stable 

baseurl=https://pkg.jenkins.io/redhat-stable/ 

enabled=1 

gpgcheck=1 

gpgkey=https://pkg.jenkins.io/rpm-stable/jenkins.io-2026.key 

EOF 
. 

Step 3: Install Jenkins 

sudo dnf install jenkins -y 

 

Step 4: Start & Enable Jenkins 

sudo systemctl start jenkins 
sudo systemctl enable jenkins 
 

Step 5: Docker Access for Jenkins 

sudo usermod -aG docker jenkins 
sudo systemctl restart jenkins 
sudo systemctl restart docker 

Docker ps 

Access Jenkins Web Interface 

Visit: 

http://<your-server-ip>:8080 

Retrieve initial admin password: 

sudo cat /var/lib/jenkins/secrets/initialAdminPassword 

Jenkins Setup for CI/CD 

Required Plugins: 

Pipeline Plugin – Enables Jenkinsfile execution. 

Git Plugin – For cloning repositories. 

Docker Pipeline Plugin – Supports docker.build() and docker.run(). 

Credentials Binding Plugin – For securely managing credentials. 
