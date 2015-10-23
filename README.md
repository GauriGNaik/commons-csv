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
    #edit jobpath
    jobpath="http://localhost:8080/job/DevOpsMilestone2/lastBuild/api/json"
    prevStatus=`curl -silent $jobpath | grep -iEo 'result":"\w*'`
    prevStatus=${prevStatus/result\"\:\"/}
    if [[ "$prevStatus" == "FAILURE" ]]; then
        echo BUILD FAILURE, Reverting last Commit
        git reset --hard HEAD^1
        echo git state back to normal
        exit 1
    fi
    ```

6. For Security tokens, we have checked the following three things:
    1.   pem files - 
        Checked the repository for .pem files, and rejected the commit if it's present.
    2.   ssh keys - 
        Checked the repository for ssh keys(id_rsa) in the whole repository and rejected the commit if it's present.
    3.   AWS Tokens - 
        Checked the Java source files for AWS Token Id's and Secret Keys. For AWS Token Id's, we have checked for              strings in Uppercase and having length greater than 20. Such strings are good contenders for Token Id's.
        Similarly for AWS Secret keys, we have checked for alphanumeric strings having length greater than 40. 
        
    All the above checks have been made in pre-commit hook.

  ```
#!/bin/bash

#check for count of pem files
PATH="/home/arvind/SampleMavenProject"
PEM_FILES_COUNT=$(find $PATH -type f -name "*.pem" | wc -l)
if [ $PEM_FILES_COUNT -ne 0 ]; then
   echo "There are .pem files in this commit.Rejecting the commit!"
   exit 1
fi

SSH_KEY_FILES_COUNT=$(find $PATH -type f -name "*id_rsa" | wc -l)
if [ $SSH_KEY_FILES_COUNT -ne 0 ]; then
   echo "There are ssh-key files in this commit.Rejecting the commit!"
   exit 1
fi

#Now scan all the source files to check for tokens or api access keys for AWS

SRC_PATH="/home/arvind/SampleMavenProject/src"
LIST_OF_FILES=$(find $SRC_PATH -type f -name "*.java")

#Get List of All .java files
for file in $LIST_OF_FILES
do
ALL_CAPITAL_TOKENS=$(grep -Eo [\"]?[A-Z]+[\"]? $file)
ALPHA_NUMERIC_TOKENS=$(grep -Eo [\"]?[0-9A-Za-z]+[\"]? $file)

# now scan all the capitalized tokens to check for possible AWS key IDs
 for token in $ALL_CAPITAL_TOKENS
  do
   l=${#token}
   if [ $l -ge 20 ];then
    echo "Seems like there are AWS Acccess key IDs in one or more source files.Please check again. Rejecting commit!"
    exit 1
   fi
  done

#now check the alphanumeric strings for length>=40
 for token in $ALPHA_NUMERIC_TOKENS
  do
   l=${#token}
   if [ $l -ge 40 ];then
    echo "Seems like there are AWS Secret Acccess keys in one or more source files.Please check again. Rejecting commit!"
    exit 1
   fi
  done
done
  
  ```




### Screencast


Team: 
Gauri Naik (gnaik2), 
Arvind Telharkar(adtelhar), 
Ravneet Kaur(ravnee)
All worked on it together. 












