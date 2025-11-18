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
### Topics and subscriptions
The topic is a big queue. Senders send messages to the topic. The topic adds the message to different subscriptions (queues) depending on their filters. 

Receivers connect to the subscriptions to receive the messages added to the queue 

### Use case for Azure Service Bus
Each has its advantages. What you use, depends on your application.
### Queue Based Load Leveling Pattern
Email application system. You place marketing emails in your queue then sends them out to your email application.

Emails are being generated and consumed at different paces. - This is why it's called *Queue Based Load Leveling Pattern*
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
