[[SSH]] [[DevOps]] [[Development]] [[CodeCommit]]

# Code Workflow TIO

## EC2 - Dev Environment
First you launch a dev environment inside EC2 - no special specs here.

The security group opens port 22 and port 8080 because we are building a tomcat app

*since you are using Code Commit - You will need to give this instance a role that allows it to use code commit*
- In the permissions look for code commit full access + Code deploy full access + code pipeline full access + **cloud watch full access for the production environment**
- The agent needs to access S3 to pull the artifact, so S3 access must be given 

#note depending on the architecture you set up, you need to make sure you have the right permissions set. 

Inside the EC2 setting you attach the role we created with the appropriate permissions 


## SSH into the EC2 instance
we do our update upgrade stuff, then we install aws cli tools and configure it. 

/opt directory will be the directory where we keep the code for this exercise (make sure to change the user ownership)

## Creating the Code Commit repo 
This is a managed service, so its just a matter of looking it up on the AWS services. 

You create a repository - name it and give a small description

### Code Guru reviewer
Is an optional service that you can enable on your repo to review your code instead of adding a custom/additional library
- At the moment we are not using this

### Creating a dev ops user in IAM for Code Commit Repo Setup
When setting up the repo: you'll probably see a warning message saying that you are signed on as a root user. You can't configure SSH connections for a root account so it recommends you to create a new user on the IAM and then setting up the connection
- Inside the IAM console you can add a user - for example - devops_user
- enable AWS management console access and Programmatic access (this gives you access to the aws cli tools)
- You also need to set up a password 

Build the permissions for this user, #recommendation when creating users, you have to be lenient with what permissions you give. Only give what is necessary. 

## Setup SSH, Git Clone
At this point we have code commit + EC2 development server

Inside Code Commit Repo you go to the SSH tab and it will give you the necessary steps to set up. The steps are very simple to follow. 

### Steps
1) First step is to *check if you have Git* - you might need to set this up. 

2) *Register the SSH public key* - You generate a key pair when you create the .pem file. You need to associate the public key to the dev root user we created above (new user for code commit). When you commit code to Code Commit you will need to authenticate yourself with the public key, if it matches the private key you are good to go. 
	- When you generate the .pem inside the EC2 instance, you are actually setting up a private and public key

#### Generating the key pair 
[[SSH]] 
In the EC2 development environment, run the command:
`ssh-keygen`

You choose which directory to save it on and the name 

Then you are prompted to enter a pass phrase 

After this, inside the directory you entered you will find a file without extension and one with .pub 

After this you need to `cat` your .pub file, grab the contents and go to the IAM console and in there go to users -> open opsroot user we created -> and upload the SSH public key. Just paste the contents of the public key. 

3) *Edit the Local SSH configuration* - here we are instructed to modify/create the config file for ssh to add the key-id from the SSH key and the path to the private key. 
	- The contents of the config file are given in the documentation and the key information can be obtained from the IAM console 
	- Also change the permissions of the file using `chmod 600`
	- `ssh git-codecommit.us-west-2.amazonaws.com`run that command and follow the prompts in the cli and then you will be authenticated 
	
After this your development environment is pointing at the CodeCommit

3) *Clone the repo* -> `git clone repo-name` similar to github 

## Putting Source Code into Code Commit
Create a directory in the EC2 then you can `scp` the file/directory to the remote machine from your local machine. Refer to [Bash Commands] to review how scp works. 

You can also do wget and the url from a s3 bucket or a link where you have your file stored

after moving the file to the remote machine you can `rsync`
it into the correct directory where you are going to keep the code base (repo)
- Not sure why not migrate it directly to the repo folder

After running that, your usual git add, git commit commands are used to push to the aws git commit repo

## Commands used in video:
**Codebase synch commands**

1. mkdir /opt/temp
2. cd /opt/temp
3. To be executed on your local laptop
    - scp -i your.pem HelloWorld-CodeBase.tar.gz ubuntu@PUBLIC-IP:/opt/temp
4. tar -zxf HelloWorld-CodeBase.tar.gz
5. cd HelloWorld
6. rm -rf .git
7. rsync -r /opt/temp/HelloWorld/ /opt/helloworld
8. cd /opt/helloworld
9. rm -rf /opt/temp

**Git commands**

1. cd /opt/helloworld
2. git add .
3. git status
4. git commit -a -m “First commit”
5. git push origin master

# Code Build
building your code base and creating the artifact you store in S3 

when Code Build is triggered -> Build environment - docker image - where source code compiles
- You can also create your own custom docker image 
- as the build progresses, you can have notifications through SNS = integration Code Build + SNS. This keeps you up to date as the code builds.

![[Pasted image 20250904122455.png]]

CloudWatch can monitor CodeBuild 
SNS Topic -> Cloud Watch rule for event and select Code Build

## Build Environment 
This build environment uses the source code

There are out of the box build environments that amazon can provide

There is a table inside the documentation that specifies which build environment version is needed for your programming language
### Build specification file - buildspec.yaml
buildspec is a collection of build commands and related settings, in YAML format, that CodeBuild uses to run a build. You can include a buildspec as part of the source code or you can define a buildspec when you create a build project.

This config file contains all the instructions on how to build your code. 

*Environment variables* -> in build environment you can declare variables for different uses. For example, you can declare a variable for the region of your Elastic Container Registry (ECR)
- You can create custom or use a standard set of variables

*Phases* -> you can also set phases, for example: first update the system, then download the libraries, etc. 

**The build specification file is just a set of instructions for the build environment**

## Code workflow 
Grab source code from CodeCommit -> execute the build spec file -> when build process is done, you can grab the artifact from the S3 bucket

# CodeBuild Project Setup
We first need a place to generate and store the artifacts - you create a bucket inside S3 -> destination of the build process

Build artifacts can store a lot of space. So we need to implement a clean up process: *life cycle*

*life cycle* -> how long files live, after some days, the buildspec file will be deleted. 

## Building a project
Inside CodeBuild, you create a *project*.

*Build badge* -> optional setting for public repos like open source projects

You determine the source of the code:
- CodeCommit
- S3 Bucket
- Github
- BitBucket
- Or no source
	- for no source, you can do a git clone of other repo but you are not connecting it to a repo 

Hook of the code to a specific *commit id, branch, or git tag*. It's better to use the branch option so anybody can push 
- you can have multiple branches attached 

Inside the *Build project* you also choose the build environment:
- You can choose a standard image
- or a custom image 

You also declare a *role* that we are using to determine the permissions 

in the *buildspec file* you can insert a file or you can program it in there. 

artifact or no artifact 

you can tar ball your buildspec files

logs -> creates a log group for CloudWatch
- you decide if your logs go to S3 


After all of this you fire up the project and see if it creates the artifact 

clicking on Start Build, it does not automate it, it does not create a pipeline. It just starts it. That comes with *Code Deploy*. 

Once its build, you can edit the configs that we created in the creation process. 


