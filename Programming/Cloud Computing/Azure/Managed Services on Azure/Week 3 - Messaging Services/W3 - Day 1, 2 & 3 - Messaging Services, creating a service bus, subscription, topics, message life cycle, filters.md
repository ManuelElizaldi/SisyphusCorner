# Messaging Services
## Azure Queue Storage
Store large number of messages up to the capacity of Azure Storage

Manage messages between sender and receiver 

First in, first out. 

## Azure Service Bus
Fully managed, service broker with enterprise level features 

Handles variety of use cases - message delivery 

Enterprise grade service 
- partition
- filtering
- ensuring arrival

Reliable delivery of Messages from sender to receiver 

protocol used -> AMQP (Advanced messaging queuing protocol)

*Delivery Modes*:
- Ensures the receiver receives the message at least once.
- Exactly once 

Queues -> where messages go
## Topics and subscriptions
The topic is a big queue. Senders send messages to the topic. The topic adds the message to different subscriptions (queues that are inside the topic) depending on their filters. 

Receivers connect to the subscriptions to receive the messages added to the queue 

*Topic* -> Publishers sends message here. This acts as a broadcast, this does not send the message directly to consumers

*Subscription* -> Virtual queue attached to a topic. Each subscription receives and stores the messages. Consumers subscribe to subscriptions and read messages from here. 


### Use case for Azure Service Bus
Each has its advantages. What you use, depends on your application.
### Queue Based Load Leveling Pattern
messages are being generated and consumed at different paces. - This is why it's called *Queue Based Load Leveling Pattern*

The primary purpose of the **Queue-Based Load Leveling** pattern is to act as a **buffer** between the application (the task/producer) and the service (the consumer/resource).

The producer sends the messages as fast as it needs to, the queue then cab absorb the high amount of messages, acting as a buffer. Then the receiver can pull the messages at its predetermined rate. 


Email application system. You place marketing emails in your queue then sends them out to your email application.
### Competing Consumer Pattern
Multiple consumers/receivers of queue which will pick up messages in parallel from the queue and process them. This way you can process even more messages. 

There can be two receivers (two email applications). One message goes to one application. 
### Priority Queue Pattern 
If you want to give priority to certain messages, for example if you want to send an 'order placed' message first and not let this email get lost in the queue behind marketing emails, you can open several queues 

Different priorities depending on the message

Usually, in the priority = 1 queue, there wont be a lot of messages compared to marketing. 
![[Pasted image 20251117184411.png]]
You have to ensure that your application is aware of all the queues, to know where to send the messages. 

The topic (all 3 queues) receive the message, based on the filter placed on the message it will go to the right subscription

### Publisher Subscriber Pattern
Message will be published once but added to multiple queues/subscribers

*Example*
When an order is placed:
1) it needs to send an email
2) confirm with warehouse team
3) inform the courier team 
4) inform audit team
- Many things happen when an order is placed. 

You can create a queue for each message/team that needs to be notified

An example graph of an ecommerce processing an order:
![[Pasted image 20251117185626.png]]

The message broker ensures the corresponding subscribers receive the message.  
## Azure Event Hubs
Fully managed service - no infrastructure to handle

Used big data scenarios

Collecting events - Events happens at an instance of time 
- when, where and how it happened

up to receiver if they want to consume the message

Millions of events per seconds - thousands of devices/resources that are being recorded 

Event generator

### Events vs Messages
If you are tracking events - go with Event Hubs, if you are interested in sending messages go with Azure Service Bus

## Azure Event Grid
Used to build event driven applications. 
- for example, if you upload a file to blob storage and you want to trigger a function, you use this

This is an event consumer 

It doesn't store information, it only captures events and sends it to the receiver 

# Creating a Service Bus 
*Namespace* -> Collection of queues & topics
- When you create a service bus, the name needs to be unique because, as many as other resources in Azure, you get a URL

*Available tiers*:
![[Pasted image 20251118205003.png]]

Main difference is that Standard has support for topics 

Premium you pay for messaging units - think of units as VMs. And you have dedicated infrastructure - you don't share the resources with someone else. 

## Message life cycle:
There are a couple of options:

After a message is consumed, it is deleted

*Time to live* -> number of days If no receiver consumes the message from service bus, then message is deleted 

*Auto delete after idle for topics* -> deletes the topic if no one has consumed messages after x days. 

*Duplicate detection* -> duplicated detection window. In case there's duplicated messages you can decide the time window to detect these messages.
- For example, there could be an issue with the application that produces messages, it could generate 2 order messages, this could cause issues. This service uses the message ID to detect where there are duplication and deletes one of the messages. 
- **you** need to place the message ID 

## Inside Topics
After creating the service bus, you can go inside the Topic. Here you create the subscriptions. 

There is an option to delete after idea for x days. 

### Time To Live Property
At the topic and subscription level.

Meaning -> Whichever is lower will be considered. If the topic TTL is 10 days and the Sub level is 12, the topic one will be considered and all the messages TTL will be 10 days. 

### Dead Lettering (DLQ - Dead Letter Queue)
In case you don't want to delete the message, but you want TTL, you can send it to *dead letter queue*. 

When the message expires, instead of deleting it will be removed from the subscription and added to the dead letter queue. This queue is manually cleaned up. It is your responsibility to clean up the DLQ 
### Max Delivery Count & Message Lock Duration 
If the *Lock Duration* is 30 seconds then -> if the receiver picks up the message and does not respond within 30 seconds that the message has been processed , then the message will unlock and it will appear in the queue again 

The application sends an acknowledgement that the message has been processed successfully.

*Max Delivery Count* -> How many times a message can be extracted from the queue. If the max delivery count is reached it is deleted.  

If the receiver does not process the message and the message goes back to the queue this is called a *1 delivery count*. If that happens again it is called *2 delivery count*, then *3 delivery count* and so on.

Max Delivery Count determines that the message can only be taken out of queue. 

If the Max Count is reached, then the message is deleted. 

**You can use Dead Letter Queue with Max Delivery Count**

## Looking At Messages
*Destructive Receive* -> You look at the message and then it is deleted. 
- Messages are NOT always deleted just by looking at them. You can set up the service to behave this way. 

*Peek* -> Looking at the data in the message, but not actually receiving/opening the message, so this does not pick up the message. 

*If you send 2 messages with the same message ID, the queue will only count it as 1.*

*Peak and lock* -> default mode for azure, you must explicitly complete, abandon or dead letter the message after processing for it to be deleted. 

# Filters 
Placed after creating subscription

If no filters are placed, all the subscriptions get the message

Topics: A topic receives all messages sent to it. Each topic can have multiple subscriptions.

Subscriptions: Subscriptions receive copies of messages from the topic, but you can use filters to control which messages each subscription actually gets.

## Example of Filters

Topic: “SalesUpdates”

Subscriptions:
Subscription A filter: region = 'US'
Subscription B filter: priority = 'high'

Message with properties region = 'US', priority = 'high' will be delivered to both subscriptions.

Message with region = 'EU', priority = 'normal' will not go to either, unless you have a default/subscription with a broader filter.

## Conditions
Using SQL like syntax you can create filters 

If you say `ProcessWarehouse = 1` in the filter and in the message you are sending you set a custom property `ProcessWarehouse = 1`, the topics that fit this criteria will receive this message
![[Pasted image 20251119163739.png]]


## Partitioning
Inside topics

*Partitioning* -> After choosing 5GB when creating the topic, after enabling partitioning, the Topic will be 80GB

There will be more message brokers being created when enabling partitioning. 

Allows higher throughput and scale by splitting the data across multiple partitions that can process messages in parallel 

Each message has 16 options of queues. There is higher availability for our queue/topic. 
- If a subscription crashes, the message can go to the next sub and so on. 

# Storage Queues vs Service Bus
![[Pasted image 20251119165519.png]]

Storage queues is cheaper and holds massive amounts of messages. But storage queue does not have enterprise level features. 

