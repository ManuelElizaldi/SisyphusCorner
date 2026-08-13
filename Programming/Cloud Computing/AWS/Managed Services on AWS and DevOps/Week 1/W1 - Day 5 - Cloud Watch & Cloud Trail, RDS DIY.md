[[Monitoring]] [[SQS]] [[SNS]] [[DevOps]] [[CloudWatch]]

# AWS CloudWatch
**Obersvability** - helps determine the root cause of issues within your services. Gives you the necessary info to fix problems. 

Enabled by default

Used for monitoring 

Frequency determines if its free or not - intervals of monitoring
- 1 minute vs 1 second frequency of monitoring

2 types of CloudWatch
- free version
- Agent - for custom applications

Custom metrics from applications can also be monitored using CloudWatch

It helps maintain the health and performance of applications and infrastructure and ensures prompt response to potential issues 


## Log Groups
You monitor services in groups - logs are created based on the services you put in this group

You can also store the logs in a S3 or other storage tools - you can build an ecosystem of all the generated logs. 

## Alarms
You set customized alarms for your services and automatically responds to changes in the user environment

## EC2 Agent 
The agent is used to collect internal system level metrics 

This agent can also be used on on-prem servers 

You point this agent to multiple log files and it can pull those files and put them into CloudWatch


--- 
# On hands video
#### Inside the log groups:
Retention -> Logs will never expire. There are logs that are not necessary, for example logs older than 6 months. You determine the expiration date. 

Logs can be formatted - AWS has a pre defined format 

## Cloud Trail
This feature keeps track of everything that happens in your account

You can have a log group based on Cloud Trail that tracks EC2 instance creations - this can be modified to track whatever activity you need. 

## Flow logs - Insights
You have queries to 'ask' about insights - for example - you get top IPs that are trying to brute force into your VPC 

This is can be automated
![[Pasted image 20250726154742.png]]


## Metrics
You can map out metrics for specific services

## Service Lens
Used to be called X-Ray 

Makes it easier to track multiple services of a complex application - for example an application that has a lot of microservices 

This can be programmed in different programming languages. After its programmed, your application starts transmitting information about your app -> how resources are being used, health info, etc. 

## Synthetics 
Can be used to monitor canary deployments through testing end points (URLs). 


## Point Next
You build dashboards with graphs that help you monitor your environment 

Every time you refresh the dashboard, there's a cost associated to that. AWS gives you free actions, but if you go over that it starts to charge you. 

--- 

# Cloud Watch & Cloud Trail

### AWS Cloud Trail
*Audit, tracking* 

Logs API calls and user activity across your AWS 

**tracks who did what, when and where**

Used for security investigation and compliance audits

### AWS Cloud Watch
*Observability and monitoring*

Creates metrics, dashboards, logs and alarms  

Creates automated responses 

### ✅ Together:

- **CloudWatch** helps you **observe** and **respond to system behavior**
    
- **CloudTrail** helps you **audit** and **investigate user and service actions**

--- 
# RDS DIY
![[Pasted image 20250726171051.png]]

