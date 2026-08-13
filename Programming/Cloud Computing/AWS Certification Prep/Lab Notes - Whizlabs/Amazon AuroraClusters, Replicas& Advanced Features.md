# Aurora Cluster Architecture 
Primary instance -> reader instance 1 and 2 
- Primary instance handles all writes (insert/update/delete, etc)

Readers handle the select queries 

So if you use Aurora in an app, when customers look at your data, the request only goes to readers? 

ALL INSTANCES READ/WRITE TO SAME STORAGE
- what does this mean?
- Shared distributed storage layer - 6 copies across 3 AZS
## Failover 
Reader promoted to primary in < 30 seconds 
- How does this compare to RDS multi AZ?

# Aurora Cluster and RDS
To create a cluster we first go to Amazon RDS and create a database. To create an Aurora database you have to select the Aurora Engine.

we create a security group for this database 

back up retention period - 1 day

1 hour window backtrack 
- each hour it takes snapshot? 


![[Pasted image 20260408220134.png]]

We created an Aurora DB with one instance 
- Regional cluster and writer instance - what is regional cluster here? 

## Cluster end points
The lab mentions that there should be 3 endpoints but I only see 2. The writer and the reader end points. I am missing the aurora lab instance 1 

The writer endpoints updates automatically during a fail over - advantage over RDS Multi AZ where the DNS update takes 60 - 90 seconds. 

## Connect and Create Sample Data 