# Jenkins Task-2 – GitHub Webhook Auto-Trigger with Email Notification

## Task Description

Create a simple script file and push it to a GitHub repository.
Create a Jenkins project connected to the GitHub repository.
When a commit is made to the repository, the Jenkins build should trigger automatically and the output should be shared via email.

---

## Technologies Used

* AWS EC2 (Ubuntu)
* Jenkins
* GitHub
* Shell Scripting

---

## Step 1 – Jenkins Installation on AWS EC2

Jenkins was installed on an Ubuntu EC2 instance using the official Jenkins repository.

Main actions performed:

* Added Jenkins GPG key and repository
* Installed Jenkins using apt
* Started and enabled Jenkins service
* Accessed Jenkins web UI
* Unlocked Jenkins using initial admin password

Screenshot:
01-jenkins-installation-and-unlock.png

---

## Step 2 – Cloning GitHub Repository and Creating Script

The GitHub repository was cloned into the EC2 instance and a shell script was created.

Script file: `script.sh`

Contents of script:

```
#!/bin/bash
echo "Hello from Jenkins Task-2"
date
hostname
uname -a
```

The script was made executable using:

```
chmod +x script.sh
```

Screenshot:
02-github-repo-clone-and-script-creation.png

---

## Step 3 – Committing and Pushing Script to GitHub

The script file was committed and pushed to the GitHub repository.

Commands used:

```
git add script.sh
git commit -m "Added Jenkins Task-2 script"
git push origin main
```

Screenshot:
03-git-commit-and-push-script.png

---

## Step 4 – Creating and Configuring Jenkins Job

A Jenkins Freestyle job named `jenkins-task2-job` was created.

Configuration details:

Source Code Management:

* Git selected
* Repository URL: [https://github.com/Padmesh010/jenkins-task2.git](https://github.com/Padmesh010/jenkins-task2.git)
* Branch: */main

Build Steps (Execute shell):

```
chmod +x script.sh
./script.sh > output.txt
cat output.txt
```

Build Triggers:

* GitHub hook trigger for GITScm polling enabled

Screenshot:
04-jenkins-job-creation-and-configuration.png

---

## Step 5 – Installing Required Jenkins Plugins

Required plugins were installed from Manage Jenkins → Plugins.

Important plugins:

* Git
* GitHub API plugins
* Email Extension
* Mailer

Screenshot:
05-jenkins-plugins-installation.png

---

## Step 6 – Configuring Email Notifications

SMTP configuration was done in Manage Jenkins → System.

Settings used:

* SMTP server: smtp.gmail.com
* SMTP authentication enabled
* TLS enabled
* Port: 587
* Sender email configured

Post-build Email Notification was configured in the Jenkins job:

* Recipient email address added
* Subject and content template configured
* Trigger set to Success

Screenshot:
06-jenkins-email-configuration-and-job-status.png

---

## Step 7 – Configuring GitHub Webhook

A webhook was added in the GitHub repository.

Webhook URL:

```
http://<EC2_PUBLIC_IP>:8080/github-webhook/
```

Settings:

* Content type: application/x-www-form-urlencoded
* Event: Just the push event

Webhook status showed successful delivery.

Screenshot:
07-github-webhook-configuration.png

---

## Step 8 – Modifying Script and Pushing Commit to Test Auto-Trigger

The script was modified to change the output message.

Updated first line:

```
echo "Hello from Jenkins Task-2 Auto-Trigger Test"
```

Commands used:

```
git add script.sh
git commit -m "Testing Jenkins auto trigger"
git push origin main
```

Screenshot:
08-script-change-and-git-push-for-auto-trigger.png

---

## Step 9 – Jenkins Auto-Triggered Build

After pushing the commit, Jenkins automatically triggered a new build.

Build details:

* Trigger source: Started by GitHub push
* Commit message: Testing Jenkins auto trigger
* Build executed successfully

Screenshot:
09-jenkins-auto-triggered-build.png

---

## Final Result

* Jenkins successfully pulled code from GitHub
* Jenkins automatically triggered builds on every commit
* Script executed successfully during the build
* Build output was generated
* Email notification logic was executed on build success

---

## GitHub Repository URL

[https://github.com/Padmesh010/jenkins-task2](https://github.com/Padmesh010/jenkins-task2)

---

## Jenkins Job URL

http://<EC2_PUBLIC_IP>:8080/job/jenkins-task2-job/

---

## Conclusion

This task demonstrates a complete CI workflow using Jenkins and GitHub:

* Source code management using GitHub
* Jenkins job configuration
* Webhook-based auto-trigger
* Script execution during build
* Email notification setup

All task requirements were successfully implemented and verified.

---
