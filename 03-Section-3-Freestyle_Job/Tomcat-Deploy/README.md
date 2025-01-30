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
    Method:1 ==> Deploy using "Deploy to container"
    Method:2 ==> Deploy using "Publish over SSH"
```
## Method:1 ==> Deploy using "Deploy to container"
### Step:1 ===> Install and Configure "Deploy to container" Plug-in
To deploy .war in Tomcat server using jenkins we need to install one plug-in "Deploy to container"
```
Manage Jenkins ==> Manage Plug-in ==> Available ==> search "Deploy to container" ==> Install without restart
```
Note ==> To deploy war to tomcat server from jenkins, you must assign this role "manage-script" to your tomcat user

### Step:2 ===> Create Jenkins "JOB" 
New item ==> JOB-Name "Deploy Container JOB" and select "Freestyle" job
1. Pull the Code
```
JOB ==> Under SCM ==> Select "GIT" ==> Paster your GIT URL and enter your Branch-Name
```
Note ==> HERE we use Public Repository, so we no need to enter Credentials

2. Remove the old Workspace before Build
```
JOB ==> Build Environment ==> Select "Deleter workspace before Build Start"
```
3. Build the Package
Install Maven Tool in Jenkins
```
Manage Jenkins ===> Global Tool Configuration ===> Scroll down to "Maven"
```
![image](https://github.com/user-attachments/assets/f8b7f6a4-ff32-4d58-8543-aba2d57dc399)

![image](https://github.com/user-attachments/assets/2bd46ea3-38c5-4e60-86e1-46bb8cd7f0b2)

Configure Maven in your JOB
```
JOB ==> Build steps ==> Select "Invoke Top level Maven" ==> Select the maven Version and Goal "compile package"
```
4. Deploy WAR file to Tomcat using "Deploy to Container"
```
Job configuration ==> post-build Action ==> Add post-build Action ==>  select "Deploy war/ear to container" 
```
![image](https://github.com/user-attachments/assets/56d6680e-0ce7-497e-b465-d70627ad35cf)

![image](https://github.com/user-attachments/assets/d14f9a77-d43b-4fbd-b150-5332138628ff)


## Method:2 ==> Deploy using "Publish over SSH"
### Step:1 ===> Install and Configure "publish over SSH" Plug-in
"publish over SSH" Plug-in Install
```
Manage Jenkins ==> Manage Plug-in ==> Available ==> search publish over SSH ==> Install without restart
```
"publish over SSH" Plug-in Configuration
If we want to do any SSH to Remote server we need these details
1. IP-Address or Hostname
2. Username
3. Password
```
manage Jenkins ==> Manage Credentials ==> create credentials ==> select "username with private key" 
	enter username "ec2-user" and private key paste your "PEM" file
```

### Step:2 ===> Create Jenkins "JOB" 
New item ==> JOB-Name "Deploy Container JOB" and select "Freestyle" job
1. Pull the Code
```
JOB ==> Under SCM ==> Select "GIT" ==> Paster your GIT URL and enter your Branch-Name
```
Note ==> HERE we use Public Repository, so we no need to enter Credentials

2. Remove the old Workspace before Build
```
JOB ==> Build Environment ==> Select "Deleter workspace before Build Start"
```
3. Build the Package
Install Maven Tool in Jenkins
```
Manage Jenkins ===> Global Tool Configuration ===> Scroll down to "Maven"
```
![image](https://github.com/user-attachments/assets/f8b7f6a4-ff32-4d58-8543-aba2d57dc399)

![image](https://github.com/user-attachments/assets/2bd46ea3-38c5-4e60-86e1-46bb8cd7f0b2)

Configure Maven in your JOB
```
JOB ==> Build steps ==> Select "Invoke Top level Maven" ==> Select the maven Version and Goal "compile package"
```
4. Deploy WAR file to Tomcat using "Publish over SSH"
```
Job configuration ==> post-build Action ==> Add post-build Action ==> select "Publish over SSH"
```
