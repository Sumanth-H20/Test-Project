# Test-Project
this repo is for practice purpose

#intializing git repositories
git clone $url$
git init          ---------------- initialize git repo
git add .         ----------------- to add the file to stagging area (all files)
git commit -m "commit message"  -------to commit the changes to repo
git push -u $branch name$     -------------to push the changes to remote repo

optional
git remote add origin <remote_repository_url>    ---------------to add the remote repo
git remote -v          ------------------------ to check the remote repo



#Jenkins Installation
ref: https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

#!/bin/bash
sudo apt update
sudo apt install fontconfig openjdk-17-jre -y
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y


sh jenkins.sh


To verify the jenkins status
systemctl enable jenkins
systemctl start jenkins
systemctl status jenkins
<img width="1641" height="313" alt="image" src="https://github.com/user-attachments/assets/b97cb1ab-ab59-4d50-92bc-f23904905023" />


#Docker Installation

#!/bin/bash
# Script to install Docker on an EC2 instance and configure permissions

# Update the package list
sudo apt-get update -y

# Install Docker
sudo apt-get install docker.io -y

# Add the 'ubuntu' and 'jenkins' users to the 'docker' group to allow running Docker without sudo
sudo usermod -aG docker ubuntu 
sudo usermod -aG docker jenkins 

# Apply the new group settings immediately
newgrp docker

# Set correct permissions for the Docker socket to allow 'docker' group members to access it
sudo chmod 660 /var/run/docker.sock
sudo chown root:docker /var/run/docker.sock

# Restart Docker service to apply changes
sudo systemctl restart docker


#to check the status of Docker
sudo systemctl status docker

<img width="1087" height="278" alt="image" src="https://github.com/user-attachments/assets/1bc7caa7-d649-4dcc-88a3-4eaf5af16665" />

login to jenkins with intial password

<img width="1632" height="868" alt="image" src="https://github.com/user-attachments/assets/3489efae-c503-4c30-bc14-20a5ef05cde6" />


configuring the pipeline as from SCM option and providing the url and branch name and also provide the jenkins file name & path
<img width="1832" height="928" alt="image" src="https://github.com/user-attachments/assets/fb07bd8a-f876-49ab-b887-37fb6f929812" />

installed below plugins as first requirement
<img width="1918" height="528" alt="image" src="https://github.com/user-attachments/assets/6b9955a8-80c1-4062-bca4-16a131a0c735" />


After this step add the webhook

under repo settings -webhook --add webhook
<img width="1150" height="873" alt="image" src="https://github.com/user-attachments/assets/c3324166-1963-4855-8ead-3a6c0defdfad" />

you should see below message if the connection is success.
<img width="1216" height="460" alt="image" src="https://github.com/user-attachments/assets/5da995ef-f30f-438e-9771-6b29028607b4" />

now we need to add the tools.
for java
<img width="1312" height="546" alt="image" src="https://github.com/user-attachments/assets/6e10996d-9063-4a35-bd84-ed63e3e92bd0" />

for maven
<img width="1255" height="497" alt="image" src="https://github.com/user-attachments/assets/56c89903-20d2-4e47-bcdf-d2410cc0acb0" />

apply-save.


Now try to build the from Jenkins pipeline.
<img width="1757" height="540" alt="image" src="https://github.com/user-attachments/assets/160e44db-e8e3-4991-8241-3c8f23e0ddc2" />

till above screenshot the build is successful.

now installing sonarqube using docker. with below command
docker run -d --name sonarqube -e SONAR_ES_BOOTSTRAP_CHECKS_DISABLE=true -p 9000:9000 sonarqube:8.9.1-community

check for running container 
docker ps
the default password and username will be admin
you should below page
<img width="1746" height="745" alt="image" src="https://github.com/user-attachments/assets/0267864b-b4ae-42f3-9419-bd5b68ac45be" />
adding the project manually.
<img width="1057" height="552" alt="image" src="https://github.com/user-attachments/assets/2e66addd-52e8-45fa-a471-01fcaf444f2a" />
it will ask for toen generation, provide the name -> generate -> continue
<img width="1267" height="511" alt="image" src="https://github.com/user-attachments/assets/ce17f812-b279-44bf-b925-61c0c187ee0e" />

now select maven as build
<img width="1638" height="732" alt="image" src="https://github.com/user-attachments/assets/fe393b50-cb05-4bda-bf78-02eacc53f721" />

get those commands and add them in the pipeline stage.
you should get passed message in sonarqube console
<img width="1658" height="651" alt="image" src="https://github.com/user-attachments/assets/9d57b59e-ac85-4843-88be-59fb8dbd09f9" />

now we are trying to introduce quality gates
for that we need to add sonarqube webhook so if the quality gate is not passed then the pipeline should fail.
for the creation of webhook
under projects -->project settings --> webhooks ->craete -->
<img width="592" height="742" alt="image" src="https://github.com/user-attachments/assets/37cb075d-0514-41c4-8344-9f888b57b99c" />

after that install sonarqube plugin in Jenkins
<img width="1432" height="290" alt="image" src="https://github.com/user-attachments/assets/cd747fd7-efaa-41d3-a125-c7098ec96006" />

now for the connection between sonar and jenkins 
navigate to manage jenkins - systems -- add
<img width="1740" height="645" alt="image" src="https://github.com/user-attachments/assets/3352cbf1-568d-4e30-93a6-fd4f2990d929" />
for the secrete form sonarqube navigate to myaccount - security - provide secrete name - generate
<img width="1312" height="851" alt="image" src="https://github.com/user-attachments/assets/c71e7a22-c940-431b-925f-bf304c81501b" />













