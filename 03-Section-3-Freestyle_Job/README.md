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
##### Step:2 
```
Go to JOB ==> Build Triggers ==> Select GitHub hook trigger for GITScm Polling
```
##### Step:3
```
Go to JOB ==> Build Triggers ==> Select GitHub hook trigger for GITScm Polling
```
## LAB-4
### Build a JAVA Project using Maven
```
Steps
```
## LAB-5
### Deploy our AddressBook App in Tomcat using Freestle JOB

```
Steps
```
