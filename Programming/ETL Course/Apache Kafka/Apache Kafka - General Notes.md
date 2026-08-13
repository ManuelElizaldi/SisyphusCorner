03/29/2025
Tags: [[Event Streaming Platform]] [[Streaming]] [[ETL]] [[Data Engineering]] [[Open Source]] [[Distributed System]]

Apache Kafka -> Distributed real time event streaming platform
- Distributed means that it runs across multiple computers/machines/nodes -> It is a cluster
- It uses the [[TCP]] [[Protocol]] -> Transmission Control Protocol. Ensures reliable, ordered and error checked *delivery of data between applications on a network| between clients and servers.* 
- Apache Kafka is a ESP - [[Event Streaming Platform]]

The main components of an ESP are:
- Event broker
- Event Storage
- Analytics
- Query Engine

Created to track user activity. Now it is used for many things.
- [[Fun fact]], it was created in LinkedIn! x

It has high Throughput (can handle high volume of data)
## Kafka Architecture
![[Pasted image 20250329114420.png]]

Core components:
- Brokers -> Dedicated server to store, process and distribute data.
	- All brokers are connected 
- Topics -> Container or databases of events
- Partitions -> Divide topics into different brokers
	- This increases fault tolerance
- Replications -> Duplicates partitions into different brokers 
- Producers -> Kafka client applications that publish events into topics.
- Consumers -> Kafka client applications that subscribe to topics and read events from them 
- Apache Kafka Controller -> Stores the metadata of all the clusters

### Note about Consumers and Producers
Consumers and producers are decoupled, meaning that they do not interact between each other. They do not need to be synchronized between each other. 

Real life example:
![[Pasted image 20250329122721.png]]

![[Pasted image 20250401213000.png]]

![[Pasted image 20250401213918.png]]

#### Source Processor
Extracts data from a source system to then be processed for further use

#### Sink Processor
Responsible for receiving and storing the processed data to then be sent to a destination system 


![[Pasted image 20250401213944.png]]


top image is more efficinet, bottom image is using an ad hoc app or script 

---
### Reference
IBM ETL Course Module 4 