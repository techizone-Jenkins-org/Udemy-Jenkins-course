# Deploy to Tomcat using Jenkins Freestyle
## Infra Setup
We need to crewate 2 servers 
```
        1. Launch Ec2 Instance with Redhat AMI for Jenkins server {open port 8080}
        2. Launch Ec2 Instance with Redhat AMI for Tomcat server {open port 8080}
```
### Jenkins Server Setup
#### Install Java
```
sudo dnf upgrade
sudo dnf install fontconfig java-17-openjdk
java -version
```
#### Install Jenkins
```
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo dnf upgrade
sudo dnf install jenkins
sudo systemctl daemon-reload
```
### Tomcat Server Setup
#### Install Java
```
sudo dnf upgrade
sudo dnf install fontconfig java-17-openjdk
java -version
```
#### Install Tomcat
```
sudo wget  https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.60/bin/apache-tomcat-9.0.60.tar.gz

			tar -zxpvf apache-tomcat-9.0.60.tar.gz   -C   /opt/
		cd /opt/
				mv   apache-tomcat-9.0.60.tar.gz    tomcat
```
#### Setup Tomcat
##### Start Tomcat
```
useradd -r  tomcat 
chown -R tomcat:tomcat   /opt/tomcat

sudo visudo 

# Add No password permissions for Tomcat user. 

Add the below line and Save. 

tomcat ALL=(ALL)       NOPASSWD: ALL 
```
#### Running Tomcat as a Service
Open the File and add the Tomcat Service
```
vim /etc/systemd/system/tomcat.service 
```
```
[Unit] 
Description=Apache Tomcat Server 
After=syslog.target network.target 
[Service] 
Type=forking 
User=tomcat 
Group=tomcat  
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid 
Environment=CATALINA_HOME=/opt/tomcat 
Environment=CATALINA_BASE=/opt/tomcat 
ExecStart=/opt/tomcat/bin/catalina.sh start 
ExecStop=/opt/tomcat/bin/catalina.sh stop 
RestartSec=10 
Restart=always 
[Install] 
WantedBy=multi-user.target 
```
#### Enable the Tomcat Services and Start the Tomcat
```
systemctl daemon-reload 
systemctl enable tomcat.service 
systemctl status tomcat.service 
```
# We can Deploy the Aplication in 2 ways 
```
    Method:1 ==> Deploy using "Publish over SSH"
    Method:2 ==> Deploy using "Deploy to container"
```
## Method:1 ==> Deploy using "Publish over SSH"
