# App deployment on kubernetes cluster , SonarQube analysis and jenkins pipeline creation

Aim of project :  SonarQube to perform Code Quality Analysis.  integrated Jenkins with Maven, SonarQube, and Docker, where the application will be accessed while running inside a container.


1. Launch Ubuntu VM with instance type as t2.large, AMI: 24.04, Storage: 25 GB, No. of instances: 1

2. jdk install

   sudo apt install openjdk-17-jre-headless -y

3. make ececutable file to jenkins.sh

     sudo chmod +x jenkins.sh

4.test jenkins on port 8080 in ec2 ipv4 address. 

5.SonarQube Setup using docker 

 sudo apt install docker.io

6.give permissions to run docker

sudo chmod 666 /var/run/docker.sock

7. docker run -d --name sonarqube -p 9000:9000 sonarqube:lts-community  ( installing sonarqube image )

   ![image](https://github.com/user-attachments/assets/a6cd5966-86cc-4b4e-8706-0d0bdc0e0a43)

8.test sonarqube on port 9000 

9.
