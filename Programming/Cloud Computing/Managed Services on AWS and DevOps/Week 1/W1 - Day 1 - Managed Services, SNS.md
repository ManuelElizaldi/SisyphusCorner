[[DevOps]] [[SNS]]
# Course Outline 
Discuss managed databases, caching, messaging, logging and more. Also look at serverless

- AWS RDS - Relational database 
- Cache management - AWS Elasticache
- Monitoring - AWS CloudWatch
- Messaging, Queue & notifications - SQS, SNS
- AWS Lambda

# Overview of Managed Services
Cloud managed services are a type of IT. The cloud provider takes over the IT operations. 


> [!NOTE] Why cloud?
> Remember that if you have a on prem operations, you are in charged of the whole operation, which takes a lot of time, effort and money. By off loading the work to a cloud provider, you don't have to worry about the infrastructure.


*Managed service* -> Monitoring, database, cache, enterprise bus service, alarms, there is a whole lot of services that can be performed by a cloud provide.
- Managed services abstract complexity so that you can focus on the core competencies of the business. 
- Scaling, managing, automation, etc. benefits

##### Practice Quiz Question -> How can a small business save money and resources when it needs to rapidly scale up its IT infrastructure comprising of various technologies like databases, NoSQL, Messaging and Streaming, among others. Which option will be the best fit?
Evaluate various managed services from AWS


# Topic and Queue - An Overview
## SNS - Simple Notification System
Trigger can come from any of the components - user actions, back end job failing, EC2 instance running into something, etc. 

**Push based model**
Push to an endpoint -> https, email, lambda function, mobile device, text sms, SQS

x happens -> there's a push notification to -> y 

Instantaneous notifications, example:
- In a ASG, if a threshold is passed or instances are added you will be notified. You can customize

Cross region deliveries - SNS, SQS and lambda functions

### There are different types of models:

- SNS -> You create a topic and users subscribe to it

- SQS -> Simple Queuing Service -> Pull based model, end point asks for information, data can be stored until a consumer comes and ask for something

- Amazon MQ -> Standard APIs that you can easily integrate 

# SNS Feature Illustrations

Application to application (A2A): publisher -> SNS Topic -> AWS Lambda, Amazon SQS, HTTPs
- Fan out -> when its sent to multiple apps

Application to person (A2P) -> The end points are services that are consumed by a person, email, text message, push notification. 

## SNS - Different Forms:
### FIFO Topic 
Message order is maintained - for some applications order of messages is important, for example prices of products, stocks, etc. 

Architecture for FIFO Topic:
![[Pasted image 20250722202224.png]]

There's a compromise in *through put*, but maintains the queue

### Message Deduplication 

SNS has a feature that removes duplicate messages
![[Pasted image 20250721173956.png]]

There are a couple of ways of removing duplicates - using IDs or Hashs This is done through APIs, SDK

### Message Grouping
![[Pasted image 20250722202605.png]]

You maintain order of messages based on a 'grouping'. For example based on a product.

Message groups are independent, order is maintained within the group


### Subscription Filters
Producer and Consumer/Subscriber 

You decide which messages you get - this is set up through a json

![[Pasted image 20250722203159.png]]

Each row follows an `AND` logic. in customer_interests = [] <- inside the list, each value is evaluated as an `OR` statement

```json
store -> example_corp
and
event -> anything but
and
.
.
rugby or football or baseball
```


> [!NOTE] Filter Criteria as Business Routing
> These filter criteria can be used as a routing technique. Each message goes to different sections of the business based on the filters set. 

### HTTP/S Delivery Retry Policy 
 
HTTP End point inside an EC2 instance that can be accessed by a push request from SNS. You can delay the rate at which you send messages based on the response you get back from the server. 

### Policy - Security
Producers will need certain privileges to send messages  


### Asynchronous vs synchronous - messages



