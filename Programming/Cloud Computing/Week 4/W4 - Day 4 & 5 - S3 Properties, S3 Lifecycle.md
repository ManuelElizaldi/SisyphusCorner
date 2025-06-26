[[Storage]]
# S3 properties
You can find all of these settings inside the management console for S3

*versioning* -> once you enable, you can't disable but you can suspend it 

Server access logging -> log requests for access to your bucket

CloudTrail data events -> important from a user perspective. There are certain API calls that will be tracked and logged 

server access logging + cloud trail -> great tool for investigating what happened

*Event Notifications* -> This acts like a cron job. Event Notifications allows you to trigger jobs when something happens. 
- Destination -> what will catch the event 

*Transfer Acceleration* -> reduces latency. - enable or disable, its amazon's responsibility for this to happen but it requires no set up. Of course it costs more.  

*Requester pays* -> The customer (your client) pays to have access 

#### Practice quiz question -> What are the typical S3 bucket properties?
Tags, Version control, life cycle management 

# S3 Lifecycle, replication, metrics
Content lifecycle management is important for content management because it allows organizations to effectively manage their digital content, making sure the most up to date version is live and that it complies with regulations. 

This also ensures that content is only stored for the amount of time that is necessary. 

Replicating content across regions lowers latency for customers.

Lifecycle is determined by *lifecycle rules*. You determine how content progresses. You decide if this applies to the whole bucket or just a prefix. 

There's a couple of settings to set up the lifecycle:
![[Pasted image 20250626181749.png]]

It works in steps, it transitions according to the days you set:
![[Pasted image 20250626181911.png]]


*Expiration* -> S3 will delete objects after a certain period of days passes. 
- Expiration needs to be larger than the max transition days 

## Replication
Replicate data from one source (bucket) to another destination

This is set up based on rules. 

rule scope -> whole bucket or only some prefixes or based in another filter. 

Replication requires bucket versioning. 

There are several options of replication:
![[Pasted image 20250626182939.png]]

#### Practice quiz question: What is the minimum number of days needed to change a document's storage class via a lifecycle configuration?
30 days. 


