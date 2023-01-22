# CONTINUOUS INTEGRATION WITH AWS DEVELOPER TOOLS


## AWS SERVICES USED


- AWS CodeCommit

- AWS CodeArtifact

- AWS CodeBuild

- AWS CodeDeploy

- AWS CodePipeline


Other Tools.......

- Sonarcloud

- Checkstyle for code analysis



### SOME BENEFIT OF USING AWS DEVELOPER TOOLS FOR CONTINUOUS INTEGRATION


- Short MTTR

- Fault isolation will be quick

- Agile

- No human intervention

- No operational overhead



#### ARTICHECTURE


Developers will make changes to the source code stored in AWS CodeCommit. Pipeline will get triggered and Sonar scanner will run and as well as Checkstyle for code analysis. For any dependencies it will download, it will be from AWS CodeArtifact and then the job will upload the report to Sonarqube cloud and get the result which will then trigger another code job and this will be to build the artifact. The artifact will be versioned and stored in AWS S3.
And also if there is any dependencies required for maven build it will be downloaded from AWS Artifact service.



..............................................
INSERT IMAGE


#### FLOW OF EXECUTION


**CodeCommit**


- Login to AWS account

- Create codecommit repo

- Create IAM user with codecommit policy

- Generate ssh keys locally

- Exchange keys with IAM user

- Transfer source code from github repository to codeCommit repository 

.......................................................................

**Code Artifact**


- Create an IAM user with CodeArtifact access

- Install AWS CLI and configure

- Export AUTH token

- Update settings.xml file in source code top level directory with steps shown

- update pod.xml file with CodeCommit repo details

................................................................................

**Sonarcloud**


- Create Sonarcloud account

- Generate token

- Create SSM parameters with sonar details

- Create Build project

- Update codebuild role to access SSM parameter store

................................................................................

**Create notifications for SNS or slack**


- Create a topic

- Create subscription and give endpoint

.................................................................................

**Build Project**


- update pom.xml with artifact version with timestamp

- create variables in SSM  in parameterstore

- Create build project

- update codebuild role to access SSMparameterstore

................................................................................

**Create Pipeline**

The flow will be like:

- Codecommit - Test code - Build - Deploy to S3 - Test pipeline


![image description](https://github.com/Helen-Chukwukelu/Project-repo/blob/d3ac56a92c9298680a757fc9bf93c6ba177704f3/pipeline.PNG)

