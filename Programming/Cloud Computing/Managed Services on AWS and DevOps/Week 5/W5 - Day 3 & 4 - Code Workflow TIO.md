[[SSH]] [[DevOps]] [[Development]] [[CodeCommit]]
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