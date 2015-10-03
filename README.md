# devops-project
The milestone one project contains the following: 
* Apache Mavens project 'Commons-Csv' containing post-commit file 
* Readme
* Screencast
* Jenkins config file 

### Build section
## Setup

* Used Apache Java Mavens project titled 'commons-csv'. 

* Used Jenkins as the build server. To install Jenkins on Mac, we have used the following command:
```
brew install jenkins
```
* The following plugins were installed in Jenkins:
  GIT plugin, Email Extension plugin, Mail Watcher plugin, Multi-Branch Project plugin, Post-Build scripts plugin

* Added the Maven, JDK installation paths in the Jenkins System settings.

* Added the smtp server value as smtp.gmail.com

* Added the user email and password for smtp authentication using ssl protocol and smtp port 465. This email is used for sending the email.

* Added the default recipients for the email.

* To be able to send emails in Mac you need to start postfix using the following command:
```
sudo postfix start
```
* And in the gmail account used for sending the email, turn off safety. 

* Create Maven multi-branch project titled 'commons-csv' in Jenkins.

* In Source Code Management section in the configuration of the project do the following: 

* Blank the Sync Branches Schedule textbox in the configuration of the project. 

* Select the Git option and then enter the path of the local Git repository using:
  file://

* Specify the Git branches from the project to be included and excluded.

* Remove all the default build triggers.

* In the build step, specify the goals and options:
```
clean install
```
* Add the following post-build steps:
* Email Notification:
Add the always trigger, so that email is sent everytime build is triggered. Also add the recipients list. 

* Post-build scripts:
Add the following script in build steps:
```
#!/bin/bash
open http://localhost:8080/view/All/builds
```

* Aggregate downstream test results:
Generates a file containing all the test reports. 

##Capabilities

* Post-Commit Hook
* Create a post-commit file in .git/hooks and place the following script inside
```
#!/bin/bash
branch_name="$(git symbolic-ref --short HEAD 2>/dev/null)" ||
branch_name="(unnamed branch)"

url='http://localhost:8080/job/commons-csv/branch/'${branch_name}'/build'
curl $url
``` 

* In the build step in Jenkins, to do a clean build we have used:
```
clean install
```

* For post-build tasks, we send email and generate test reports as described above

* The branch on which commit is done, the corresponding job in jenkins is triggered. 

* Open the build history page in jenkins as a post build task.  

### Screencast
![screencast m1](https://cloud.githubusercontent.com/assets/11006675/10261150/a0c5d94a-6957-11e5-89cb-c514f2911627.gif)

Team: 
Gauri Naik (gnaik2), 
Arvind Telharkar(adtelhar), 
Ravneet Kaur(ravnee)













