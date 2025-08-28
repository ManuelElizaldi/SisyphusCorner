[[Dev Ops]]

# Deploying code tools 
AWS CodeCommit, CodeBuild, CodePipeline - help to automate the code deployment process and make it easier for developer to quickly deploy their code

Write code and stored in repo. Then we issue the build process, the artifacts are taken and deployed. 

*code commit* -> storing in a code repository. After you commit you start the code build process. Once the artifacts are built, you do code deploy to update any managed service. 

**Code -> code commit -> code build -> code deploy**

What sits on top of the above chain is *Code Pipeline*.
- This makes deploying easier and more manageable 
- You can deploy to environments that have a specific *tag*

After the code has been built, you can do a manual approval before deployment to other environments. 

You can also add your own jenkins process to this code pipeline

# Operations Workflow Details - Automated Code Release in Test Environment 
Test environment can be deployed on the cloud or on your laptop or on prem systems

Inside the dev environment (EC2), you can install git and establish a connection to CodeCommit through SSH. 

> [!Agents in this scenario]
> Developers, System Admins and Quality Assurance Teams 

When putting your code inside the EC2 instance, you can do it through multiple ways, for example getting it from a storage solution like S3 or drop box. Another example could be getting it from a git repo or even SCPing it to the EC2 instance 

### Pushing source code to CodeCommit
For this we need IAM with the right permissions to be able to push

### CodeBuild and Programming Environments
Once the code has been committed, you integrate that with CodeBuild. CodeBuild creates an environment, here you need to pay attention to the environment you are using because each programming language has a different environment. 
- Keep an eye out on documentation to make sure you are using the right environment. 

The artifact of CodeBuild is stored in a S3 bucket
### CodeDeploy
CodeDeploy grabs the artifact in S3 and then pushes to the target environment. 

*Target Environment* -> It can be an EC2 instance, which is very simple. 
- We can also have a target group that sits behind a load balancer and there's a bunch of EC2 instances that can be used to deploy. 
- Each EC2 has a tag to identify them easily. You can also have a container based environment that depends on ECS

#### Blue Green Deployment/Immutable Infrastructure:
if you have V1 already deployed, but want to deploy V2, with Blue Green Deployment you don't need to touch the existing deployment. First you deploy a new environment and then deploy V2 there. Once you ensure it works, terminate V1 environment. 
- With this approach your existing environment isn't affected/touched. You have a fall back you can rely on. 

## CodeDeploy Agent 
This is the part of the infrastructure that is able to push the S3 artifact (your code) to the EC2 instance

### How to generate a generic code deployment strategy that works with all environments?
Aspects file - specifies how the environment is deployed, the SysAdmin/DevOps people are in charge of creating this. Thanks to this file the CodeDeployment Agent knows if we are using a tomcat or flask or what ever you are deploying.
- Similar to a Dockerfile 

#### In place deployment 
Takes the existing environment and pushes the new version there. 