2025-03-29
Tags: [[Event Streaming Platform]] [[Streaming]] [[ETL]] [[Data Engineering]] [[Open Source]] [[Distributed System]]

_Partition and Replications_: Each broker helps other brokers partitioning and replicating topics. This ensures reducing fualt and increasing throughput.

There's a CLI for each, producer, consumer and topics

### Producer

Receives the data, in the screenshot attached, logs, and User activities. Then it distributes it between the brokers and its corresponding topics. 

Producers publish events to a topic

![[Pasted image 20250329120428.png]]

### Using Keys

Events: An event can be associated to a key. Events with the same key will go to the same topic (topic partition)

If an event does not have a key, it will rotate between topics

	- Note: I believe that the best practice is to *ALWAYS* use a key


- Assigning/Creating a Kafka Producer with the CLI with and without a key:

![[Pasted image 20250329121939.png]]

A good example of a key would be: Application Name or User ID

### Consumer
Consumers subscribe to topics and can read all events from the beginning.


![[Pasted image 20250329122205.png]]

- Creating a Consumer with the CLI:

![[Pasted image 20250329122531.png]]



---
### Reference
IBM ETL Course Module 4 