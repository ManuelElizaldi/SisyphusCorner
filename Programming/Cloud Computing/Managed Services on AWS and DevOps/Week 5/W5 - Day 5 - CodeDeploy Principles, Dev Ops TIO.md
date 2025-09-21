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

# Elastic Beanstalker 



# AWS CodePipeline Advanced DIY Exercise

Objectives:
1. Deploy a web application on PaaS (Elastic Beanstalk) using a CI/CD pipeline (CodePipeline) after fetching the source code from a version control system (GitHub). 
2. Push an update to the application after deployment and observe the automatic execution of the pipeline

Created key pair 

Created role - for EC2 and added permission AWSElasticBeanstalkWebTier
