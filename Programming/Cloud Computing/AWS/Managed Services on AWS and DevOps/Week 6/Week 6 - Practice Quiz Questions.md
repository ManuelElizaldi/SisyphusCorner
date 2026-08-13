**A company is planning to launch a new application that will require a complex, multi-tier cloud infrastructure. The company wants to quickly create and deploy the necessary infrastructure using AWS CloudFormation. The company begins by creating a template that specifies all the resources and their configurations that will be required. This includes AWS EC2 instances, security groups, an ELB, a database instance, an S3 bucket and IAM roles.**

**The company then uses the CloudFormation template to create a stack. This stack creates all the necessary resources and configures them as specified in the template.**

**Once the stack is created, the company can deploy the application to the EC2 instances in the stack. The ELB will automatically distribute traffic across the instances, while the RDS instance provides the necessary database. The IAM roles and security groups are configured to provide secure access to the application and resources.**

**Finally, the S3 bucket is used to store any data associated with the application.**

**By using AWS CloudFormation, the company is able to achieve which of the following?**
Quickly and easily create, deploy and manage its complex cloud infrastructure
Document the required infrastructure along with dependencies
Focus more on the application and business features needed by the customers


**Which of these cannot be created using a cloud formation template?**
Elastic IPs, VPCs, Autoscaling group 

**Assume that you are creating an EC2 instance using a CloudFormation template. What is the condition for specifying a default key-value pair for the instance?**
The key-value pair must be created before the template is run

**You want to distribute a CloudFormation template to a group of trainee developers in your company so they can create EC2 instances as development and practice environments. However, you do not want them to create instances of type “large” and “small” and want to restrict them to “nano” or “micro”. Which attribute in the template would you set to accomplish this?**
Allowed Values


**Which option is NOT true about cloud formation?**
Cannot handle updates

**The default location of buildspec.yml is**
project root 
By default AWS CodeBuild looks for the buildspec.yml in hte root directory 
- you can specify a custom path as well 

**Which of the following functions are used to return a value corresponding to a key in CloudFormation template mapping?**
FindinMap
`Fn::FindinMap`


**Which of the following is required while executing the docker tag command prior to pushing an image to a private registry such as AWS ECR?**
Image name (or ID), URI (specific registry format)
`<aws_account_id>.dkr.ecr.<region>.amazonaws.com/<repository-name>:<tag>
`
**What is the default permission level of an AWS ECR Repository?**
Read/write by the IAM user who created it
No other account has the permission to read unless explicitly granted via IAM policy 

**Two applications need to run in a Linux OS of size 1.5GB. Both application's deployment environment is 0.5GB (maybe Java runtime). Application specific libraries are of 0.4GB and 0.6GB respectively. Calculate the disk space savings in deploying the applications in containers as opposed to deploying them in virtual machines.**
2GB
### 🚀 Case 1: Deploying in **Virtual Machines**

Each VM needs:

- OS: **1.5 GB**
    
- Runtime: **0.5 GB**
    
- App libraries: **0.4 GB** and **0.6 GB**
    

For **App1** VM → 1.5 + 0.5 + 0.4 = **2.4 GB**  
For **App2** VM → 1.5 + 0.5 + 0.6 = **2.6 GB**

👉 Total for 2 VMs = **2.4 + 2.6 = 5.0 GB**

### 🚀 Case 2: Deploying in **Containers**

Containers share the host OS. So:

- OS: **1.5 GB (shared)**
    
- Runtime: **0.5 GB (shared)**
    
- Libraries: **0.4 GB + 0.6 GB = 1.0 GB**
    

👉 Total for containers = **1.5 + 0.5 + 1.0 = 3.0 GB**

**What happens to the layers when an image is deleted?**
Deleted if no other image is referring to it 
images are made up of layers -> layers are shared between images whenever possible -> when  you delete an image only the unique layers to that image are deleted. 


**Under which of the following circumstances would a Git push command from an Ubuntu EC2 instance to CodeCommit fail?**
The instance does not have the relevant IAM permissions


**The docker command used to log into a shell in a running container is __**
exec
`docker exec -it my_container /bin/bash
`
**Which of the following connections types are supported by CodeCommit?**
HTTPS and SSH
- **HTTPS** – typically used with IAM credentials or Git credentials.
    
- **SSH** – using SSH keys associated with your IAM user.

**The environment required by the CodeDeploy agent to run is __**
Ruby
AWS CodeDeploy agent is written in ruby 

**What is the default port used by the load balancer created by the ECS service?**
80
By default the load balancer listens on port 80
You can configure it to run on any other port

**Which of the following is not a valid source to be used by Code Pipeline?**
Answer : none of these

options: Bitbucket, S3, ECR 

**File gateways facilitate the transfer of files to __**
S3
File gateway provides a file interface to Amazon S3 

**what is the payment model for cloud formation?**
Based on resources created 
AWS CloudFormation itself is free, you get charged by the resources deployed. 

**Consider the given architecture which is the production for a startup. Assume the startup is also using ECR for their image repository.**
![[Pasted image 20250915185629.png]]

**The containers were created from a proprietary image developed by the startup. The image had a specific version of an open source dependency (among others) which was deprecated. This was causing a lot of warnings to appear in the logs. The operations engineer manually updated the environment by getting in each container using "docker exec -it ..... bash". This fixed the issue immediately.**

**Later that day, there was a spike in traffic and an autoscaling group (ASG) provisioned more instances with containers to handle the traffic. Soon, the operations team discovered the problem of warnings has resurfaced.**

**Which of the following errors did the engineer commit?**
The docker image is still using the deprecated dependency 

When ASG lunches an instance that runs a container it pulls it from the container registry, if you don't update this image, the not updates version will be used to create the instances. 

ASG does not pull containers from S3

**An application consists of a set of containers, each hosted on individual EC2 instances. Each container performs a different job, but all of them require a common area to read certain configuration file and other static files (reading parts of these files is possible).**
Volume mapping to an EFS mount point
- **EFS (Elastic File System)** provides a **shared, network-accessible file system** that can be mounted simultaneously by multiple EC2 instances or containers.
    
- Since your containers need **a common area to read configuration and static files**, EFS is ideal because it supports **concurrent reads/writes** across multiple instances.
    
- **EBS** is **block storage** and can only be attached to **one instance at a time**, so it won’t work for multiple containers on different EC2s.
    
- **S3** is object storage and **cannot be mounted as a traditional filesystem** without additional tools; it’s better for storing objects or logs, not a shared live filesystem.

**What is the level of isolation among Docker containers?**
Process