# Jenkins-docker
Install Jenkins and install docker to demostrate use of docker agents for builds instead of traditional Jenkins slave machines.

## Install Jenkins
Pre-Requisites:
 - Java (JDK)

### Run the below commands to install Java and Jenkins

Install Java

```
sudo apt update
sudo apt install openjdk-11-jre
```

Verify Java is Installed

```
java -version
```

Now, install Jenkins

```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
In the security group of the EC2 instance open port 8080 in the inbound traffic rules

### Login to Jenkins:

In your browser enter http://<ec2-instance-public-ip-address>:8080 
  
You see the Jenkins page, 
      - From your command line run - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
      - Enter the Administrator password
      - Install suggested plugins
      
## Install the Docker Pipeline plugin in Jenkins:

   - Log in to Jenkins.
   - Go to Manage Jenkins > Manage Plugins.
   - In the Available tab, search for "Docker Pipeline".
   - Select the plugin and click the Install button.
   - Restart Jenkins after the plugin is installed.
     
## Configuration Docker

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```
 
### Grant Jenkins user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
systemctl restart docker
```

Restart Jenkins

```
http://<ec2-instance-public-ip>:8080/restart
```

The docker agent configuration is now successful.
