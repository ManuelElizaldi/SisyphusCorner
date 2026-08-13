[[RDS]] [[SQL]] [[Database]] [[Cache]]

# RDS - Managed Database Service

Managing a database on prem can be time consuming and expensive. RDS managed service offers a solution to this problem. You can connect your application easily to any of the engines. 

If you run a RDS on prem, you need to invest in hardware, software and human capital

**Benefits**:
- Cost saving - pay as you go
- Scalability - encryption, data storage 
- Security 
- Better performance 
- You don't have to worry about routine operations performed on a database, now you only worry about the core business operations

## Supported database engines
Oracle, MySQL, PostgreSQL, Microsoft SQL, IBM DB2, Maria DB

## RDS Terminology
*DB Instance* -> Isolated database environment. This environment can contain multiple databases.

*DB Instance Class* -> Determines the computational capacity of a Amazon RDS DB Instance
- This depends on your application's requirements

*Instance Storage* -> It uses Amazon Elastic Block Store volumes for database and log storage 


## Types of Storage

*General Purpose* -> cost effective and can cover a broad use case scenarios - medium sized DBs

*Provisioned IOPS SSD* -> Designed for intensive I/O workloads. This is used for low latency and consistent I/O through put.

*Magnetic* -> designed for backward compatibility 

## Monitoring and maintenance 
Amazon CloudWatch can be used for alerts and monitoring. Cloudwatch has charts that monitors the health of a DB Instance 


**Security Group** is set up to determine who can access the DB Instance - a range of IPs is given. 

*Maintenance window* -> there is a weekly window of time where maintenance is performed on the DB Instance - patching, updates, etc is applied.
	- This is performed randomly, but you can also determine when this happens. 
	- This is what receives maintenance:
		- Hardware
		- OS - security reasons 
		- database engine version

Patches are deployed because of security reasons and instance reliability 

# Deployments
## Multi  AZ Deployment
You have your main RDS and then a stand by on another AZ in case one fails. It provides data redundancy and minimizes latency spikes during system backups

If you are providing maintenance to the RDS, you can use your *stand by instance*

![[Pasted image 20250724161018.png]]

*Synchronous replication* -> They always have the same data  

## Read Replicas - Redundant Deployment 
Read only copy of a DB Instance. You can improve performance by routing queries to this *read only replica*.

![[Pasted image 20250724163227.png]]

When you make updates to the main/primary DB, Amazon RDS updates the read replica asynchronously. 

## Multi AZ Cluster
![[Pasted image 20250724163457.png]]

This deployment is semisynchronous, high availability deployment mode with 2 standby replications. 

1 writer DB instance 2 readable standby instances. Everything in 3 AZs

This deployment model uses semisynchronous replication. 

Reader DB instances can act as a fail over in case the writer (main) DB instance fails. Amazon RDS chooses the reader instance with the most up to date change record 


## Types of replication

Replication -> writing data from one DB instance to another one | back up of sorts 

*Synchronous* -> The primary DB instance sends the write operation to all replica DB instances and it waits for confirmation that they have received and committed the transaction before completing the write. 

*Asynchronous* -> The primary DB does not wait for any replicas. It just sends the data and moves on. This is fast but the risk of losing data exists because replicas might have not catch up to the primary 

*Semisynchronous* -> The primary DB sends the write operation and it only waits for acknowledgment from one replica DB

--- 

# Amazon ElastiCache

**Cache** -> Small, fast memory storage that temporarily holds frequently used or recently used data. 
- faster than disk based databases 

## Why is it important?
Instead of retrieving the same data multiple times, you keep it in the cache for faster retrieval. This way you circumvent latency issues, disk access, etc. You have the information right there for use. 

It also provides a **layer** between the application and the database the mitigate the impact of database failures. In case the database is down or temporarily slow, you have the memory in your *cache*.

#### Use case in distributed systems
#note *Distributed system* -> multiple computers working in a cluster to solve a problem. It appears as a single computer.

In this approach cache offers an option to have data replication at the ready in case a computer - that's part of the system - fails and data needs to be retrieved. 

**Redis** is used for this example

## Features

*Engines* -> Redis and memcached 

Fast operation speeds 

One click configuration

AWS ElastiCache can be monitored through AWS CloudWatch 

Pay as you go

Security and compliance

### Redis
Used for internet real time applications. Blazing fast

Open source, accessed through APIs

Uses the Redis Data format

### Memcached
In memory key-value store service that can be used as cache or data store

fully manged, scalable and secure, making it an ideal candidate for use cases where frequently accesses data must be in memory

# RDS Metadata TIO
[Link](https://d6opu47qoi4ee.cloudfront.net/genAI/msad/rds/rds-metadata.pdf)

The objective of this hands-on exercise is to develop an automated pipeline that integrates Amazon S3, Amazon SQS, and an EC2- hosted Python script to efficiently process and store metadata of uploaded objects

Event Driven Architecture

The goal The goal of this hands-on exercise is to implement an event-driven system that automates metadata extraction from files uploaded to Amazon S3. The system should achieve the following: 
1. Trigger an Event When a File is Uploaded: Configure Amazon S3 Event Notifications to send a message to Amazon SQS when a new file is uploaded to the S3 bucket. 
2. Process S3 Events Using an EC2-Hosted Script: Deploy a Python script on an EC2 instance that continuously polls the SQS queue for new messages. Once a new event is detected, retrieve the event details and extract the object metadata from S3 using the Boto3 SDK. 
3. Store Metadata in Amazon RDS: Establish a connection to Amazon RDS (MySQL) from the Python script. Ensure that the metadata table exists, and insert details such as the file name, bucket name, file size, content type, and last modified timestamp into the database.

![[Pasted image 20250804194317.png]]

Access policy was set by a Json

### Creating S3 Event Notification to Send Messages to SQS

This is done inside the properties tab of the S3 bucket, you scroll down a little bit and you find the Create Event Notification button 

There are multiple *Event Types*, you can specify multiple. This is what we selected for this exercise:
![[Pasted image 20250804195446.png]]

We also need to select the *Destination*. For this we select the radio button for *SQS Queue*

![[Pasted image 20250804195614.png]]

After this we created our RD Instance - for testing and development. Most of the settings are unchecked, but should be checked for production databases 

## rds-sg security group

Inside the EC2 management console, I opened the security group we created for the RD instance. I was asked to modify the inbound rules card to 
![[Pasted image 20250804201054.png]]

## EC2 Instance Security Group & IAM Role
We need to open port 3306 to communicate with MySQL

Source Type anywhere - this instance can be accessed from anywhere - if you have the creds 
![[Pasted image 20250804201410.png]]

We also changed the EC2 instance IAM role to LabInstanceProfile

## Connecting to Ubuntu EC2

We ran all the necessary maintenance commands - sudo update, etc and we also installed python via:
```
sudo apt install python3 python3-pip -y
```

and we also installed via pip the AWS SDK for python and mysql for python

```
pip3 install boto3 pymysql
```

We also installed awscli and ran the command aws configure
![[Pasted image 20250804203110.png]]



## Metadata.py

From the SQS details we created earlier we grabbed the url:

```
https://sqs.us-east-1.amazonaws.com/715923492212/S3MetadataQueue
```

we also grabbed the RDS endpoint

```
gl-rds.c2nnpahz9s69.us-east-1.rds.amazonaws.com
```

Script will be saved inside /Scripts folder from this week. 


After making these changes, I copied the script file from my PC to the ubuntu instance using this command:

```
manu@ManuelDesktop:~/Desktop/Projects$ scp -i testing-development.pem /home/manu/Desktop/Projects/Scripts/metadata.py ubuntu@54.198.6.92:/home/ubuntu/scripts
``` 

Then ran it:
![[Pasted image 20250804204022.png]]

The script will wait until something is uploaded to the S3 bucket 

I uploaded a World of Warcraft screenshot:
![[Pasted image 20250804204212.png]]

And the script responded:
![[Pasted image 20250804204220.png]]

you can follow the instructions created by the script and select to view the metadata available:
![[Pasted image 20250804204308.png]]

## TIO Conclusion
Solution to capture metadata using Amazon S3 *Event Notifications*, which triggers messages to Amazon SQS whenever a new file is uploaded. 

Then we had a EC2 instance continuously poll the SQS via a python script, retrieves the metadata and inserts it into Amazon RDS. 

*Event Driven* strategy 

AWS Services used:
- AWS RDS
- SQS
- S3
- EC2

### How to optimize this
You can bypass the EC2 instance and SQS by deploying a lambda function that is invoked every time a new file is uploaded. The same python file can be used inside the lambda function to extract the metadata and write it to a RD instance

This approach allows for:
*autoscaling* -> Here you depend on 1 EC2 instance to do the job 

*serverless approach* -> not need to maintain the EC2 instance and the SQS

*event driven* -> almost instant processing of metadata, with the EC2 instance there could be delays

*reduced complexity* -> simpler architecture: S3 -> lambda -> rds

*lower cost* -> lambda is pay for use, and EC2 instances run continuously incurring in costs 

Where our approach could be better -> if this was an intense, time consuming process. Lambda functions are short lived and have limits. If the workload takes longer or requires more complex dependencies EC2 + SQS could be better suited  

