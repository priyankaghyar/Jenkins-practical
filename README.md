A simple Jenkins pipeline to verify if the docker slave configuration is working as expected.
Steps as below:
1.	Installation of ec2 instance
•	Go to the aws console
•	Create and launch the ec2 instance
 
![image](https://github.com/user-attachments/assets/a76f2752-8588-4e18-8de5-4bdf83aeb3b8)

2.	Connect the ec2 instance on mobaXterm
   
 ![image](https://github.com/user-attachments/assets/d58ab2dd-5315-4ab1-9a64-5c4d104a7e8e)


3.	Install Jenkins

Pre-Requisites:
•	Java (JDK)
Run the below commands to install Java and Jenkins
Install Java

        sudo apt update
        sudo apt install openjdk-17-jre


Verify Java is Installed

        java -version

 ![image](https://github.com/user-attachments/assets/c79b4f5d-cc09-46c6-a7fa-a35636da990d)


•	Proceed to install Jenkins

          curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee
          /usr/share/keyrings/jenkins-keyring.asc > /dev/null echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]
          https://pkg.jenkins.io/debian binary/ | sudo tee
         /etc/apt/sources.list.d/jenkins.list > /dev/null 
         sudo apt-get update 
         sudo apt-get install jenkins


 ![image](https://github.com/user-attachments/assets/91e0ccfa-a62b-4e67-8629-c936fca389d7)


• Jenkins is installed but it will not allow inbound traffic to the external due to restriction of aws. So, we need to allow the traffic
•	Go to the running ec2 instance
•	Go to the below tab security group -> click on that group name -> add the inbound traffic rules.


 ![image](https://github.com/user-attachments/assets/4c0ed4ef-9f2f-43b4-aff5-5a9e70ac6f4f)


4.	Login the Jenkins using the below URL:
•	http://<ec2-ip>:8080 
•	After you login to Jenkins, - Run command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword – 
•	Enter the Administrator password

 ![image](https://github.com/user-attachments/assets/fb0990d9-5001-47c6-9298-c25ef2e6bfc4)


5.	You will get the Jenkins window
 
http://54.81.177.130:8080/

 ![image](https://github.com/user-attachments/assets/64b5f2fa-fcfd-4483-aca4-0dab75509939)

![image](https://github.com/user-attachments/assets/5fa4e55f-62ce-4690-9a71-3f9433d4518a)

 ![image](https://github.com/user-attachments/assets/0ad36e8e-ab02-4c83-9fe6-23e6039eab7e)

6.	Install the docker pipeline plugin in Jenkins
•	Log in to Jenkins.
•	Go to Manage Jenkins > Manage Plugins.
•	In the Available tab, search for "Docker Pipeline".
•	Select the plugin and click the Install button.
•	Restart Jenkins after the plugin is installed.

 ![image](https://github.com/user-attachments/assets/9201361c-72d2-4e66-955a-523f4eaef428)


7.	Docker Slave Configuration
   Run the below command to Install Docker
  	
              sudo apt update
             sudo apt install docker.io

Note: Here we are using docker as agent

8.	Grant the Jenkins user and ubuntu user permission to docker daemon

            sudo su - 
            usermod -aG docker jenkins
            usermod -aG docker ubuntu
            systemctl restart docker


Now Jenkins is able to create the container tried hello-world

 ![image](https://github.com/user-attachments/assets/0568ad53-5694-499b-91de-c5c9c4f23249)


9.	Restart the Jenkins.

http://<ec2-instance-public-ip>:8080/restart

![image](https://github.com/user-attachments/assets/59cb010c-5b32-4e1d-b50b-bab1619edd8e)

10.	Configure the pipeline
    
 ![image](https://github.com/user-attachments/assets/f0c320c6-41eb-42b8-9932-c9e21d17344c)


11.	Pipeline is running and checkout the console output
    
![image](https://github.com/user-attachments/assets/bc4b53d4-42be-414c-ac46-e02700a50ea5)

 ![image](https://github.com/user-attachments/assets/41a35a38-b74b-4a6c-957f-398a8e2833f9)


 

	Multi-stage-multi-agent example pipeline as below:
Set up a multi stage jenkins pipeline where each stage is run on a unique agent. This is a very useful approach when you have multi language application or application that has conflicting dependencies.
1.	Two stages are used: Front end and backend
2.	configure and run the pipeline
   
 ![image](https://github.com/user-attachments/assets/67f3377a-fdd5-4be2-bcb0-332da26099fe)
 
![image](https://github.com/user-attachments/assets/b51a5f3a-b09a-451b-be63-e8499294c52b)

![image](https://github.com/user-attachments/assets/03c7a7de-ee86-4f10-866f-2b348d2794db)

 The docker configuration and pipeline now successful.

 

