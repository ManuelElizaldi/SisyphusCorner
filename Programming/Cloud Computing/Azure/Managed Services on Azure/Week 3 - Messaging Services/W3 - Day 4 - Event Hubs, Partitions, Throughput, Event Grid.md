# Azure Event Hubs
Fully managed, stream ingestion service used in big data scenarios 

*Event* -> Something that has happened at a moment. For example, if a patient is wearing a wrist band that tracks health measurements 

Events are continuously being generated. Event Hubs can handle millions of events per second.

Can manage logs as well 

Temporarily stores information and then the application that processes events can consume it at its own pace. 

## Terminology & Example 
*Example* -> different people wearing wristbands tracking health measurements. Event Hub has partitions - this partitions are internal. Events can land in any partition - round robin algorithm.

Partitions are important to handle huge amounts of data 

Event Data = message

Publisher = producer

*Partition Key* = Same as filters from Azure Bus Service placed on subscriptions. If you set a partition key, it wont perform the round robin distribution. 

**Producer creates event -> it is sent to Azure Event Hub -> Consumer Group keeps track of events -> Receiver/Consumer/Application takes in the events**

The job of the *Consumer Group* helps you keep track of the events consumed by the receiver/application. 

Opposed to Azure Bus Service, when you consume an event, this is not deleted. 
- There is a retention period. Events are only deleted after the retention period has expired. 

If the events expire before the receiver consumed them, it wont be able to consume them 
- Make sure you set the right retention period 

![[Pasted image 20251119211849.png]]

Protocol used -> AMQP

# Creating Event Hub in Azure 
Global unique name 

Collection of Event Hubs
![[Pasted image 20251120182857.png]]
Message retention in standard is 7 days (professor mentioned it might be wrong).

Partition -> allows for people to partition their specific section. More speed at processing events. High availability. Can process data in parallelism.
- Partition keys 

# Partitioning 
Once you create the number of partitions, you can't change it.

You will have partition Ids - which can be specified manually. 

Partition key and id must match, if they don't, then round robin happens. 

1 partition per event. 

## Event Data
Each event has a body - which is binary format. They can be stored in json, xml, etc. 

The max event size is 256 kb. 

### Capture Feature
If you enable this, all the events that come in, you will store them in your storage account. 

You determine how often you create a file to save this events. 

**App -> Event Hub -> Capture and put in storage**

For this you need to update the Access Policies with the connection string. 

In this case, the connection string is added to the code. Inside the code you can also specify the partition key. 

Event capture has a specific format that it follows 

# Through put of Event Hub
Throughput units -> pre purchased capacity of computer power. 

ingress -> 1 throughput unit -> 1 mb/sec or 1000 events/sec
egress -> 1 throughput unit -> 2 mb/sec or 4096 events/sec 

from 1 to 20 available, but you pay for what you choose 


*Auto inflate* -> auto scaling capacity for event hub. You can start with 1 and grow based on demand. 

There is also *Geoerovery* -> This will set up another event hub somewhere else if the one you have crashes. 
- note -> this does NOT recover the data, it only creates another event hub space. 


# Event Grid
For event driven applications 
![[Pasted image 20251120204029.png]]

*Event sources* -> they generate the event. For example, if there is a new event in blob storage, then this event is captures by the event grid and invoke something in the event handler.

*Event Handler* -> what is being invoked based on the event. 

## Demo
There is a blob storage account (event source), new file upload (blob created event). -> Sent to event grid -> placed the information into a queue that a file has been uploaded - this is the event handler (or end point).

### Setting up the Event Grid
In most of the Azure resources, you will see an option for 'Events' in the left hand management console. Here you can create a Event Subscription = this is the event grid.

Each resource has a different Event Grid to track different features/events. 

Here you also specify the end point 


