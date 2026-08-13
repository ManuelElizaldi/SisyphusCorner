https://manuelpracticeaws1.signin.aws.amazon.com/console

MFA -> factor -> piece of evidence. 
possession, inheritance, location, etc. 
- Convenience vs security 


account = root user 

# IAM

3 different identity objects:
user -> people or applications that need access to your account
Group -> collection of related users
Role -> used by AWS services or granting external access to your account 
policy -> allow or deny access to AWS services 

IAM main uses:
1) identity provider - IDP. 
2) authentication
3) authorize - allow or deny access to resources 

only 1 account root user - only used for the initial account user, then you use IAM users. 
- You only give the specific permissions needed to the IAM users. 

When you create IAM users you get a URL. They must be unique inside your account. 

*Least privilege access* -> Only grant the necessary permissions for an account. 

IAM can do as much as the root user, root user has full privilege, so it is best practice to create an additional identity and only give it the permissions it requires. 

IAM Policy -> Objects that allow or deny access to AWS services. 

No cost 

# Services
## Compute Services
Orchestration -> AWS Batch -> Batch workloads. Dynamically deploys the compute resources based on the requirements 
- Planning, scheduling and execution of your batch workloads using a EC2 instance

AWS beanstalk -> automates the deployment, management, scaling and monitoring of your custom applications in AWS. 
- Upload add and it will automatically handle the common tasks to run your application.
- Handles capacity provisioning, load balancing, database management,auto scaling and health monitoring. 

**Jack and the Beanstalk**
- your applications = beans in the fairy tale. They grow overnight by themselves 

AWS Light sail -> Virtual private server. Has its own web management console. 

AWS outputs -> hybrid service that allows you to run AWS services like amazon EC2 on your on prem infrastructure. 
- AWS offers a physical server, you only need to plug it in, configure and you are ready to go. 

## Container Services
Virtual machine -> emulates a computer
- hyperversion

Container -> emulates an application, light weight version of a virtual machine. 
- Container engine

ECS -> Container orchestration service that supports docker containers. 
- TaskRoleARN

EKS -> Kubernetes service. Manages containerized workloads and services. Launches and orchestrates a cluster of compute resources using EC2 or Fargate. 

Fargate -> serverless compute engine. Works with ECS and EKS


ECR Container registry service 

CLI tools -> command line tools 
- AWS App2Container 
- AWS Copilot 

# Security 
DETECT threats in real time?
→ GuardDuty (VPC Flow Logs + CloudTrail + DNS)

FIND PII/sensitive data in S3?
→ Macie (S3 ONLY — never EC2, RDS, or EBS)

SCAN for vulnerabilities/CVEs?
→ Inspector (EC2 + Lambda + ECR images)

AGGREGATE all findings, one dashboard?
→ Security Hub (never remediates alone)

BLOCK web application attacks (SQL injection, XSS)?
→ WAF (L7, in front of ALB/CloudFront/API GW)

ABSORB DDoS attacks?
→ Shield Standard (free, basic)
→ Shield Advanced ($3K/month, serious attacks)

AUTO-REMEDIATE anything?
→ EventBridge + Lambda (triggered BY Security Hub)
→ Never Security Hub alone

# Cloud Formation
You don't need to specify resource order when creating infrastructure. CLoudFormation figures it out on its own.

There is an attribute you can determine on the config file `DependsOn` but this is used for resources that are not as obvious. 
- You don't need to declare 1) vpc, 2) subnet 3) EC2. CloudFormation can determine the order on its own. 
- **Cloud Formation is Declarative not Imperative**

CloudFormation can detect drift -> when a resource differs from the config file/template. 
- but it cannot remediate the drift. You can perform a **Stack Update** that brings everything back to the template format. 
  
In order to fix drift you can pair Cloud Formation with AWS Config. 

# IAM Identity Center
User to login to AWS with corporate credentials 

