[[Code Workflow]]

# CodeDeploy Principles
![[Pasted image 20250906123601.png]]

Step 1 is creating the tar file (config file) and putting it in the S3 bucket created to hold the artifact

Step 2 Deploy service - also deployed with a config file named *appspec.yml* 

# RPO & RTO 
https://olympus.mygreatlearning.com/courses/132234/modules/items/7609175?pb_id=19113

# DevOps TIO
Dev Ops = Development + IT 

The TIO has 3 sections that ilustrate different areas of DevOPs
![[Pasted image 20250921095802.png]]

## TIO 1 

TIO 1 -> Building a DevOPs instance where the code is first tested before deploying into production. 
- code compilation and creation of deployment artifact 

First we launch an EC2 instance - basic set up, linux system. 


> [!NOTE] TIO - Pending
> Due to version mismatch and AMI not available I left this exercise pending. 

# Elastic Beanstalk 
End to end web application management 

Helps you deploy and scale web applications and services developed with different programming languages. 


# AWS CodePipeline Advanced DIY Exercise

Objectives:
1. Deploy a web application on PaaS (Elastic Beanstalk) using a CI/CD pipeline (CodePipeline) after fetching the source code from a version control system (GitHub). 
2. Push an update to the application after deployment and observe the automatic execution of the pipeline

Created key pair 

Created role - for EC2 and added permission AWSElasticBeanstalkWebTier

Inside Elastic Beanstalk we create an application on PHP platform running on a Amazon Linux 2023 - application code set to sample and presets to single instance 

When configuring service we added an AWS elastic beantalk service role and the previous EC2-elb-role 

we didn't set up a network, database, instance traffic scaling nor monitoring capabilities but they are available. 

After that we create our service 

Creating CodePipeline - connects to github, depending on 


elastic beanstalk -> github -> code build 