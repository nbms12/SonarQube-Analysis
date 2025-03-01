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

9. install neccessary pluggins

    a) SonarQube Scanner
   
    b) Eclipse Temurin installer
   
    c) Pipeline Stage View

11. under tools of jenkins
      add jdk  > Name: jdk17  > Check' install automatically, Select 'Install from adoptium.net' from dropdown, Version: select jdk-17.0.11+9
      Add SonarQube Scanner  > Name: sonar-scanner, 'Check' install automatically, Select 'Install from Maven Central', Version: SonarQube Scanner 5.0.1.3006
      add maven > Name:  maven3,  'Check' install automatically, Select 'Install from Apache' from dropdown, Version: 3.9.7

    save and apply .


12. configure sonarqube server

      SonarQube console --- Click on 'Administration' --- Click on 'Security' --- Select 'Users' --- You can see 'Tokens' --- Click on 3 dashes icon --- A New dialogue --- Name: token, Expires in: 90days --- Generate and copy it.


13. adding credentials to sonarqube and dockerhub

     a) for sonarqube >  Manage Jenkins --- Security --- Credentials --- Click on 'global' --- Click on 'Add Credentials' --- Kind: Secret text, Scope: Global, Secret: <Paste the token copied from SonarQube console>, ID: sonar-token, Description: sonar-token --- Create

    b) for dockerhub > configure dockerhub credentials with id as "dockerhub-credentials" with kind as "username with password" ( my dockerhub username and pwd )


14. configure sonarqube server into jenkins

    Manage Jenkins --- System --- Scroll down to 'SonarQube servers' --- Click on 'Add SonarQube' --- Name: sonar-server --- ServerURL: <PublicIPofSQinstalledVM>:9000 --- Server Authentication Token: select 'sonar-token' --- Apply --- Save


15. create an  pipeline job and start build. 

    add jenkins file code as it and  convert github url from pipeline syntax .
    
     ex : https://github.com/nbms12/SonarQube-Analysis.git  >  git branch: 'main', url: 'https://github.com/nbms12/SonarQube-Analysis.git'


16.once build is succesfull , we can see docker image is pushed into dockerhub.

17 . sonarqube project is created and we can see in port 

![image](https://github.com/user-attachments/assets/10430a3d-2717-47a4-88f2-3224b789501f)


18. test application in 5555 port no

    ![image](https://github.com/user-attachments/assets/65f29647-25e8-4964-a5ba-f09587f7edb4)






    
