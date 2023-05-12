
<br/>
<p align="center">
  <h3 align="center">Send mail notification to GitHub last committer email using Jenkins.</h3>

  <p align="center">
    <a href="https://github.com/ShaanCoding/ReadME-Generator/issues">Report Bug</a>
    .
    <a href="https://github.com/ShaanCoding/ReadME-Generator/issues">Request Feature</a>
  </p>
</p>

![Contributors](https://img.shields.io/github/contributors/ShaanCoding/ReadME-Generator?color=dark-green) ![Stargazers](https://img.shields.io/github/stars/ShaanCoding/ReadME-Generator?style=social) ![Issues](https://img.shields.io/github/issues/ShaanCoding/ReadME-Generator) 

## Table Of Contents

* [About the Project](#about-the-project)
* [Built With](#built-with)
* [Getting Started](#getting-started)
* [Results](#results)


## About The Project

Jenkins is a self-contained, open source automation server which can be used to automate all sorts of tasks related to building, testing, and delivering or deploying software.

In this project, we will integrated Github repository with Jenkins and send mail automatically to Github committer if build failed.

## Built With

To do it we need to install Jenkins in our local Machine.

## Getting Started

First we need to go the Dashboard of Jenkins and click New Item option:

![DashBoard](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/94acc698-315f-4bea-855d-5c9a9cc19286)

Then gave the name of the project, select FreeStyle project and hit Ok.

![FreeStyleProject](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/1a84d7ad-f485-4868-83ee-36c1a1ac3771)

Then navigate through Configure -> Source Code Management and select Git.
Give the Repository URL(if needed give credential also. As it is a public project so no credential is needed).

![SourceCodeManagement](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/7f5ce0c7-4883-4b18-9428-214b46f6d602)

After that, under Build Triggers options select Poll SCM and in Schedule box write * * * * * which is an expression that specifies the schedule for the job run. 
The five fields in the expression represent, in order, the minutes (0-59), hours (0-23), days of the month (1-31), months (1-12), and days of the week (0-7, where both 0 and 7 represent Sunday).

So, * * * * * means every minute, every hour, every day of the month, every month, and every day of the week.

![BuildTriggers](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/9d3a0817-6004-4398-9a01-a21ffeba4150)

Then under Build Steps option select Execute Windows batch command
from drop down options and run the following Script:
```
for /f "usebackq delims=" %%a in (`git log -1 "--pretty=format:%%ae"`) do set COMMITTER_EMAIL=%%a
echo The committer email is %COMMITTER_EMAIL%
setx MAIL_RECIPIENT "%COMMITTER_EMAIL%"
```

this runs a for loop to extract the email address of the last committer using the git log command and setx command makes the variable available to other processes

![BuildSteps](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/c3265f4e-afa2-4f54-9c6d-f00eb1be4a67)

Then Post-build Actions select Editable Email Notification from dropdown. Under Project Recipient List write $MAIL_RECIPIENT which store the email address. Under Default Subject and Default Content options set required data to be mailed.
![ProjectReciepientList](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/02cd0727-8082-48a0-af65-6bb4a726c8c0)
![DefaultSubjectAndContent](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/e9738bd8-5afe-4ac1-82fe-5189fed97b95)

Then from Advance settings option go to Triggers and select Always if you want to send mail always or select Failure-Any if you want to send failure mail only and in send To option select Recipient List and hit save.
![AdvanceSettingsTriggers](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/b613d790-52ff-49e3-8696-6f5a2b818b23)




## Results
After that press build now option, this will try to build your source code. 

![buildNow](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/ce4fb006-ede2-49a1-9a6e-697241c82681)

You can see if the build is succeed or failed from console output. if the build is failed the committer will get an email to notify him/her.

![ConsoleOutput](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/310b8ff2-baed-4346-9650-d99241435e85)

The committer will get a notification email of failure like below one!

![mailInbox](https://github.com/Mirazul62/Jenkins-GitHub-Integration-Send-Mail-Notification-to-Last-Committer-Email/assets/39739233/71c7fe7e-b344-49da-8f83-ab8bad7c5f43)


