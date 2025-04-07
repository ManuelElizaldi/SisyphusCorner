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

### [[Messages Keys]]:
Recommended to always use to prevent incoming events to be distributed randomly across partitions. 

Without key:
```
{"atmid": 1, "transid": 100}
```

Not using a key will distribute events like so:
`Partition 0` -> `Partition 1` -> `Partition 0` -> `Partition 1` …


This is how an event looks like with keys enabled:
```
1:{"atmid": 1, "transid": 103}
```

In this example, keys are enabled with the 1st command and the ":" separator is defined. Like so:

```
--property parse.key=true
--property key.separator=:
```

The key will be user defined - meaning you say what it is. In this case, we use the atmid as a key. 

### [[Consumer Offset]]:
To understand consumer offset, you need to know that partitions keep published messages (or events) stored as a list. 

Each item in this list has an index, that index = the offset. 

The example that was given in the module, is:
- If a partition is empty, its offset will be 0. If you publish/post/send the first message/event, its offset will be 1. 
	- *Message offset indicates a message's position in the sequence.* 

Using consumer offsets allows you to specify the starting position for message consumption. 
- I want messages from offset 1 - 5

You usually group consumer, example given in module: you have a consumer per ATM in the region and you want to group them all.

![[Pasted image 20250407171901.png]]

#### Log end offset: 
end of the sequence

#### Lag
Unconsumed messages




---
### Reference
IBM ETL Course Module 4 