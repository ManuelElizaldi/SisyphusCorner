03/29/2025
Tags: [[Event Streaming Platform]] [[Streaming]] [[ETL]] [[Data Engineering]] [[Open Source]] [[Distributed System]]

Apache Kafka -> Distributed real time event streaming platform
- Distributed means that it runs across multiple computers/machines/nodes -> It is a cluster
- It uses the TCP [[Protocol]] -> Transmission Control Protocol

Created to track user activity. Now it is used for many things.
- [[Fun fact]], it was created in LinkedIn! x

It has high Throughput (can handle high volume of data)
## Kafka Architecture
![[Pasted image 20250329114420.png]]

Core components:
- Brokers -> Dedicated server to store, process and distribute data.
- Topics -> Container or databases of events
- Partitions -> Divide topics into different brokers
	- This increases fault tolerance
- Replications -> Duplicates partitions into different brokers 
- Producers -> Kafka client applications that publish events into topics.
- Consumers -> Kafka client applications that subscribe to topics and read events from them 


---
### Reference