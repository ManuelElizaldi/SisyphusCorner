2025-03-29
Tags: [[Streaming]] [[ETL]] [[Data Engineering]] [[Event Streaming Platform]]

[[Event]]: Entity's observable state change overtime. Some examples:
	- GPS
	- Temperature
	- Computer resource usage
	- Patient's blood pressure

Common formats for an event:
- Primitive -> "Hello World"
- Key-Value -> "User_01" : "Deleted"
- Key-Value with timestamp -> "Patient_01":"Blood Pressure: 154/160", (14:00 3/29/2025)

[[Event Streaming]]: Moving data from event source to event destination
	- Event Source: Data comes from here
	- Event Destination: This is where you will store your data

![[Pasted image 20250329112831.png]]


An Event Source can also be an Event Destination.
	Receive data, process it and send it again.

Event Streaming can get complex, one source can go into multiple destinations, or there could be many sources going into different event destinations. In addition to this, each Event Stream can have a different [[Protocol]]. Some examples of protocols are:
	- [[FTP]]
	- [[HTTP]]
	- [[JDBC]]
	- [[SCP]]

![[Pasted image 20250329112814.png]]

## ESP - Event Streaming Platform

To handle the complexity of Event Streaming an ESP (Event Streaming Platform) can be used.
	ESPs allow all Event Sources to send data to one place and all Data Destinations to subscribe to only one place.

### ESP Components 
- Event Broker 
	- Ingestor: Receive events
	- Processor: Cleans (normalize, format, etc.) data.
	- Consumption: Retrieves data from storage and sends it to destinations

![[Pasted image 20250329113125.png]]

### Popular ESPs
Apache Kafka, Amazon Kinesis, Apache Flink, IBM Event Stream, Azure Event Hub


---
### Reference

IBM ETL Course Module 4 