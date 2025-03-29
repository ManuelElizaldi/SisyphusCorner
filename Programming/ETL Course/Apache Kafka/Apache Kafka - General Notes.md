{{date: YYYY-MM-DD}}
Tags: [[]]

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