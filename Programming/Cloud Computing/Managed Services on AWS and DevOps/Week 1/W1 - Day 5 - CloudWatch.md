[[Monitoring]]

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

![[Pasted image 20250726154742.png]]

