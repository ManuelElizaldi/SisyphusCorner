**Which of the following is a property of events in Azure Event Hub?**
An event can only be a part of one partition

You can use a partition key to map incoming event data into specific partitions for the purpose of data organization. Once an event is added to a partition, it cannot be added to any other partitions.

**Which of the following is an advantage of Azure Service Bus over Azure Storage Queue?**
Service Bus has support for detection of duplicate messages

The standard and premium tiers of Service Bus support duplicate detection. Enabling duplicate detection helps keep track of the application-controlled MessageId of all messages sent into a queue or topic during a specified time window.

****Consider a NoSQL database containing the customer information of an e-commerce site. One of the frequent use-cases is to retrieve the name, address, and account ID of a customer when required, in that order**

**Which of the following is a reason why a column-family database would be used here instead of a graph-based database?

Related fields can be put in a column family to make retrieval faster

Column-family databases are best used when you have established query patterns. In this case, for example, the name, address, and account ID can be put in a single column family to make access easier

**What is the maximum size of an event in Azure Event Hub using the basic plan?**
256 KB
The basic plan of Azure Event Hub allows for a maximum size of 256KB while the standard, premium and dedicated plans allow for a maximum event size of 1 MB

**At which point in its lifecycle is an event removed from the Event Hub?**
Event Hub will store events up to the event's specified retention period. Event Hubs Standard tier currently supports a maximum retention period of seven days. Event hubs aren't intended as a permanent data store. Retention periods greater than 24 hours are intended for scenarios in which it's convenient to replay an event stream into the same systems

**Which of the following algorithms is used to handle conflict management in CosmosDB by default?**
Last Write Wins

In Last Write Wins, if two or more items conflict on insert or replace operations, the item with the highest value for the conflict resolution path becomes the winner.

**Which of the following file formats is supported by the Azure resource manager?**
JSON
An ARM template is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax, which lets you state what you intend to deploy without having to write the sequence of programming commands to create it.

**How is data distribution performed among Event Hub partitions if no partition key is specified by the sender?**
Round Robin

If a partition key is not specified, Event hub uses the round-robin algorithm to ensure that all partitions receive an equal workload

**Which of the following queue patterns can be used to prevent a task from overloading a service with repeated messages?**
Queue-Based Load Leveling

A simple way to implement throttling with a service is to use queue-based load leveling and route all requests to a service through a message queue. The service can process requests at a rate that ensures that resources required by the service aren't exhausted, and to reduce the amount of contention that could occur.