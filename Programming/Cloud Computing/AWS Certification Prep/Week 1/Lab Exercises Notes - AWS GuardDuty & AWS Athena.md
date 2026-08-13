[[AWS]]

[website for practice exams](https://portal.tutorialsdojo.com/courses/aws-certified-solutions-architect-associate-practice-exams/#learndash-course-content)
# AWS GuardDuty 

Monitors your work loads for malicious activity and delivers detailed security findings for visibility and remediation 

Using machine learning and anomaly detection it can detect:

- unauthorized activity
- suspicious network activity 
- malware infections
- data ex filtration
- account takeover 

Offer continuous monitoring, account take over, etc. 

## Integration
It can integrate with other AWS monitoring systems like AWS Security Hub and Amazon detective to help you investigate and respond to threats 

## Cost
No upfront cost, you only pay for what you use

## Architecture Diagram
![[Pasted image 20260303150109.png]]


**Detector ID** -> represents the resource GuardDuty 

**Service Roles** -> GuardDuty uses a service role to monitor data for you 

Finding can be automatically exported to CloudWatch or to a S3 bucket 

You can suspend and disable, but when you disable GuardDuty you lose all the custom settings and findings. 

**List Management** -> Inside this setting you can list safe IPs and threat IPs

**Accounts** -> here you invite other AWS accounts into your GuardDuty and you master account can monitor member accounts
- You can only have one master account per region and up to 1000 member accounts 

### Generating Findings
![[Pasted image 20260303155627.png]]

you can generate sample findings like in the screenshot above. 

When you click on a finding, you will see this window pop up detailing the services that are affected, the account, the severity, etc. 

![[Pasted image 20260303160002.png]]


You can investigate further with the 'investigate with Detective' button.

---

# Athena 
Query service that makes it easy to analyze data in S3 using standard SQL. 
- Serverless resource 
- Under the hood it uses Presto 

Pay per query model 

It can easily integrate with AWS Glue for metadata management 

![[Pasted image 20260303165640.png]]


> [!NOTE] Note
> Athena's serverless nature allows users to analyze data stored in S3 without the need for any infrastructure provisioning or management. This means that users can focus solely on querying and analyzing their data without worrying about setting up and maintaining servers or clusters. The pay-per-query pricing model of Amazon Athena ensures cost efficiency, as users are only charged for the actual queries they run. This flexibility and cost-effectiveness make Amazon Athena a powerful and convenient tool for data analysis tasks in AWS.


# Workgroups - Athena feature
Workgroups allow us to separate users, teams, applications, workloads and set limits on amount of data for each query or the entire workgroup process. 

you choose the analytics engine for each workgroup

When setting this up, you can also determine if athena manages the results or if you manage them yourself. 
- S3 query output management 

Inside IAM you can determine what data is visible to each work group 

Workgroups are also used to manage costs. 

# AWS Glue
Serverless data integration service. Helps you prepare data for data analysis and move it into different resources. 

You only pay for the resources used when preparing data. 

ETL service 

**Glue table** ->  Represents the structure and schema of the data stored in the S3 bucket.  
- This need to be associated to a Glue Database
- you decide the source of the data (s3, kinesis, kafka)
- You also need to point to the path of the S3 bucket 

After deciding on the settings of the table you have to create the schema and data format (csv, json, xml, etc.)

# Querying the table with Athena 
Athena console:
![[Pasted image 20260303171600.png]]

On the top right corner you choose the workgroup 
## Lab
We created a workgroup glue database, and a glue table and then we queried the S3 bucket which contained a csv file with expenses 


# Lab: Deploying a Highly Available Web Application and Bastion Host in AWS
1. This lab walks you through the steps to deploy a highly available Web application and use Bastion host to control the access to underlying private instances.

Something I don't think I have seen before. We select a security group as source for a web server in a private subnet. This allows only the Bastion server to SSH into the web server, but restricts the public SSH connections. 

And in the second inbound rule we choose load balancer security group type HTTP port 80, so that the load balancer can communicate to the web server.
![[Pasted image 20260322094555.png]]

User data script inserted:
```
#!/bin/bash
sudo su
dnf update -y
dnf install httpd -y
systemctl start httpd
systemctl enable httpd
echo "REQUEST HANDLING BY SERVER 1" > /var/www/html/index.html
```

Set up a highly available web server with a bastion host. First we use a template from CloudFormation that generates a custom VPC with 2 private subnets and 2 public subnets in 2 different AZs. (1 private and one public per AZ).

First step is creating a bastion host. This is used to securely access our web servers, it acts as a gateway filtering out unwanted traffic or malicious attacks. The bastion host has a security group with source from anywhere and port 22 open for SSH. 

### Why Bastion has open SSH to anywhere:
This is only done in lab/testing environments, usually this is not done in production. 

### How Bastion Hosts would look in production:
In production, you specify an IP that can access the server. Only x.x.x.x/32 IP can access the bastion server, as an example. 

**Examples:**
Option 1: Restrict to your office IP range
          SSH port 22 → source: 192.168.1.0/24

Option 2: Use AWS Systems Manager Session Manager
          No SSH at all — browser-based shell, no port 22 needed
          No bastion host needed either!

Option 3: AWS VPN → then SSH from VPN IP only


> [!NOTE] **SAA exam tip:**
>  If a question mentions "securely connect to private EC2 instances without opening port 22 to the internet" → **AWS Systems Manager Session Manager** is the answer, not a Bastion host.


Then we create 2 web server, each in it's own private subnet. Here we placed the web server in the private subnets because there's going to be a load balancer placed in front of these web server that will direct traffic accordingly so they don't need to be exposed to the public.

What is exposed to the public is the ALB. 
- SSH is allowed from the Bastion server by attaching the Bastion security group to the source. 
	- *Security Group Referencing* -> Only the instances that have the Bastion-SG attached can SSH into the web server. This could be better than an IP range since IP ranges change, SG membership is stable, the rule follows the security group not the IP. Much more precise only the bastion can access, nothing else. 

Then we create a Target Group composed of the 2 web servers we created. Load balancer will route the requests to the targets inside this target group and perform health checks at a determined interval to check if the instances are healthy and ready to receive traffic. 

- Ask claude: Inside the target group it asked me about which HTTP Version to use: HTTP1 vs HTTP2 vs gRPC, what's the difference between these 3?:
- **SAA exam tip:** These are different application protocols 
- Standard web app → HTTP/1.1
- Performance-sensitive modern app → HTTP/2
- Microservice-to-microservice → gRPC

REST/HTTP = humans and services talking in plain text
gRPC      = services talking to each other in optimized binary
  

Before we attach the instances to the target group we also have to make sure they have the right inbound rules to receive HTTP requests (if that is what they are meant for). In this setup the web servers have a security group rule that allows inbound HTTP traffic where the source is the load balancer security group. 

### Internal vs Internet Facing ALB
What is the difference between a internet facing load balancer and a internal? 
- Is internal ALB is used for internal/private service to service communication.
- Internet facing has a public DNS that anybody can access. Accepts traffic from the internet 

Real life example:
Internet
    ↓
Internet-facing ALB (public)  ← users hit this
    ↓
Web tier EC2s (private)
    ↓
Internal ALB (private)        ← web tier hits this
    ↓
App tier EC2s (private)
    ↓
RDS (isolated)

When creating the load balancer, choosing the AZ we chose the public subnets. Is this because it is internet facing? Correct. The ALB is internet facing. 

In listeners and routing we chose the target group that contains the web servers. Routing action forward to target group. 

Once we have everything created, we also tested the high availability of the web servers by stopping one of the instances. We saw that the ALB directed traffic to the healthy instance. 

Ask claude -> do uses go through the bastion host first? Or they don't see it and only view the ALB when entering the DNS?


### Full architecture of this lab:
Bastion-SG:   Inbound SSH (22) from 0.0.0.0/0 (lab only — bad practice)
WebServer-SG: Inbound SSH (22) from Bastion-SG
              Inbound HTTP (80) from ALB-SG
ALB-SG:       Inbound HTTP (80) from 0.0.0.0/0

### Security group chain
ALB-SG      → allows internet HTTP/HTTPS
WebServer-SG → allows HTTP from ALB-SG only
              → allows SSH from Bastion-SG only
Bastion-SG  → allows SSH from your IP only (not 0.0.0.0/0!)

#note source in bastion host 0.0.0.0/0 only used in testing/lab environments. 



