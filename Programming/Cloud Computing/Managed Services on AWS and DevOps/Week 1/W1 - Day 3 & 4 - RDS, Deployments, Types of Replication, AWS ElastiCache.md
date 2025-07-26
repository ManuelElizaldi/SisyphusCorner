[[RDS]] [[SQL]] [[Database]] [[Cache]]

# RDS - Managed Database Service

Managing a database on prem can be time consuming and expensive. RDS managed service offers a solution to this problem. You can connect your application easily to any of the engines. 

If you run a RDS on prem, you need to invest in hardware, software and human capital

**Benefits**:
- Cost saving - pay as you go
- Scalability - encryption, data storage 
- Security 
- Better performance 
- You don't have to worry about routine operations performed on a database, now you only worry about the core business operations

## Supported database engines
Oracle, MySQL, PostgreSQL, Microsoft SQL, IBM DB2, Maria DB

## RDS Terminology
*DB Instance* -> Isolated database environment. This environment can contain multiple databases.

*DB Instance Class* -> Determines the computational capacity of a Amazon RDS DB Instance
- This depends on your application's requirements

*Instance Storage* -> It uses Amazon Elastic Block Store volumes for database and log storage 


## Types of Storage

*General Purpose* -> cost effective and can cover a broad use case scenarios - medium sized DBs

*Provisioned IOPS SSD* -> Designed for intensive I/O workloads. This is used for low latency and consistent I/O through put.

*Magnetic* -> designed for backward compatibility 

## Monitoring and maintenance 
Amazon CloudWatch can be used for alerts and monitoring. Cloudwatch has charts that monitors the health of a DB Instance 


**Security Group** is set up to determine who can access the DB Instance - a range of IPs is given. 

*Maintenance window* -> there is a weekly window of time where maintenance is performed on the DB Instance - patching, updates, etc is applied.
	- This is performed randomly, but you can also determine when this happens. 
	- This is what receives maintenance:
		- Hardware
		- OS - security reasons 
		- database engine version

Patches are deployed because of security reasons and instance reliability 

# Deployments
## Multi  AZ Deployment
You have your main RDS and then a stand by on another AZ in case one fails. It provides data redundancy and minimizes latency spikes during system backups

If you are providing maintenance to the RDS, you can use your *stand by instance*

![[Pasted image 20250724161018.png]]

*Synchronous replication* -> They always have the same data  

## Read Replicas - Redundant Deployment 
Read only copy of a DB Instance. You can improve performance by routing queries to this *read only replica*.

![[Pasted image 20250724163227.png]]

When you make updates to the main/primary DB, Amazon RDS updates the read replica asynchronously. 

## Multi AZ Cluster
![[Pasted image 20250724163457.png]]

This deployment is semisynchronous, high availability deployment mode with 2 standby replications. 

1 writer DB instance 2 readable standby instances. Everything in 3 AZs

This deployment model uses semisynchronous replication. 

Reader DB instances can act as a fail over in case the writer (main) DB instance fails. Amazon RDS chooses the reader instance with the most up to date change record 


## Types of replication

Replication -> writing data from one DB instance to another one | back up of sorts 

*Synchronous* -> The primary DB instance sends the write operation to all replica DB instances and it waits for confirmation that they have received and committed the transaction before completing the write. 

*Asynchronous* -> The primary DB does not wait for any replicas. It just sends the data and moves on. This is fast but the risk of losing data exists because replicas might have not catch up to the primary 

*Semisynchronous* -> The primary DB sends the write operation and it only waits for acknowledgment from one replica DB

--- 

# Amazon ElastiCache

**Cache** -> Small, fast memory storage that temporarily holds frequently used or recently used data. 
- faster than disk based databases 

## Why is it important?
Instead of retrieving the same data multiple times, you keep it in the cache for faster retrieval. This way you circumvent latency issues, disk access, etc. You have the information right there for use. 

It also provides a **layer** between the application and the database the mitigate the impact of database failures. In case the database is down or temporarily slow, you have the memory in your *cache*.

#### Use case in distributed systems
#note *Distributed system* -> multiple computers working in a cluster to solve a problem. It appears as a single computer.

In this approach cache offers an option to have data replication at the ready in case a computer - that's part of the system - fails and data needs to be retrieved. 

**Redis** is used for this example

## Features

*Engines* -> Redis and memcached 

Fast operation speeds 

One click configuration

AWS ElastiCache can be monitored through AWS CloudWatch 

Pay as you go

Security and compliance

### Redis
Used for internet real time applications. Blazing fast

Open source, accessed through APIs

Uses the Redis Data format

### Memcached
In memory key-value store service that can be used as cache or data store

fully manged, scalable and secure, making it an ideal candidate for use cases where frequently accesses data must be in memory

