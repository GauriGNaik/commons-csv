# devops-project
The milestone one project contains the following: 
* Apache Mavens project 'Commons-Csv' containing post-commit file 
* Readme
* Screencast
* Jenkins config file 

### Build section
## Setup

* Used Apache Java Mavens project titled 'commons-csv'. 

##Tasks
1.   
2.   
3.   
4.   
5.  For this task, we have configured cobertura to fail the build if the coverage falls below some specified criteria. So, on commit to the repository, the build will fail if the coverage decreases. Once, the build fails, we are checking in post-commit, the status of the Jenkins Build. On Build Failure, the last commit is reverted and repository goes back to previous state.
```
#!/bin/bash
prevStatus=`curl -silent http://localhost:8080/job/DevOpsMilestone2/lastBuild/api/json | grep -iEo 'result":"\w*'`
prevStatus=${prevStatus/result\"\:\"/}
if [[ "$prevStatus" == "FAILURE" ]]; then
    echo BUILD FAILURE, Reverting last Commit
    git reset --hard HEAD^1
    echo git state back to normal
    exit 1
fi
```
6.   

### Screencast
![screencast m1](https://cloud.githubusercontent.com/assets/11006675/10261150/a0c5d94a-6957-11e5-89cb-c514f2911627.gif)

Team: 
Gauri Naik (gnaik2), 
Arvind Telharkar(adtelhar), 
Ravneet Kaur(ravnee)
All worked on it together. 












