# Freestyle JOB
#### How to create Freestyle JOB
```
Jenkins Home ==> New Iteam ==> Enter "JOB Name" ==> Select Freestyle JOB
``` 
## LAB-1
### How to Run the Command or Shell scrit using Jenkins Freestyle
```
JOB => configure ==> Build step ==> Execute Shell ==> HERE we mention our Shell script
```
```
#!/bin/bash
age=30
if test $age -ge 18
then
echo "You are eligible for vote"
else
echo "You are not eligible for vote"
fi
```
### Execute these shell script Every Day at 1 AM
### I want to Execute these shell script Every Day at 1 AM

```
JOB => configure => Built Trigger => Build periodically ==> Mention cron "0 13 * * *" => click on "save"
```
## LAB-2
### What are the Manditory option we need to selecct for a Jenkins JOB

#### 1. Delete existing workspace before build start

These will delete the Existing Workspace Before it start the New Build
```
job ==> Build Trigger ==> Delete Existing workspace before build start
```
#### 2. Delete the old builds

These will Delete the out Builds, we need to mention the threshld then it will delete accordingly 
```
job ==> General ==> Discard old builds
```

#### 3. Add Timestamp to your Builds

These will add the Timestamp to our Buils, when we see console output then it will show Timestamp
```
job ==> Build Trigger ==> Add Timestamp to Console Output
```

## LAB-3
### GIT Webhook Integration

If we use Webhooks Job will be Trigger Immediately whenever developer push the Code. 
    Webooks Works under push based Mechanism, If you use webhook Job Triggered for Every Commit

##### Step:1 
```
Go to JOB ==> Build Triggers ==> Select GitHub hook trigger for GITScm Polling
```
![image](https://github.com/user-attachments/assets/5f1110df-5a7d-4c75-b1dc-b9f16bf3453c)

##### Step:2 
```
Step:2  ===> Copy your Jenkins JOB URL
```
![image](https://github.com/user-attachments/assets/81f1660b-6b81-4e7e-a60b-926e16e0b6c8)

##### Step:3
```
Step:3  ===> go to our GitHub Project  Repository ==> Settings ==> webhooks ===> Click on Add Webhook
```
Mention your Jenkins URL like below format
```
http://<Jenkins-URL>/github-webhook
```
![image](https://github.com/user-attachments/assets/10841439-a3e8-4a39-979e-b9525d523686)


## LAB-4
### Build a JAVA Project using Maven
We need to Follow these steps
```
            Step:1 ===> Install Maven Tool in Jenkins
            Step:2 ===> Maven Integration to your JOB
```
#### Step:1 ===> Install Maven Tool in Jenkins
```
Manage Jenkins ===> Global Tool Configuration ===> Scroll down to "Maven"
```
![image](https://github.com/user-attachments/assets/f8b7f6a4-ff32-4d58-8543-aba2d57dc399)

![image](https://github.com/user-attachments/assets/2bd46ea3-38c5-4e60-86e1-46bb8cd7f0b2)


## LAB-5
### Deploy our AddressBook App in Tomcat using Freestle JOB

```
Follow These in Tomcat-Deploy Folder
```
