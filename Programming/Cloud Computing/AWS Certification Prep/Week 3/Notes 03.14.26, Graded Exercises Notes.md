

# Creating a MySQL databases on Amazon RDS 
**instance type, storage size, and security settings**
![[Pasted image 20260311194554.png]]

Connecting lambda function to RDS MySQL. Use lambda to query the SQL database. 


First we create a RDS, then we downloaded the MySQL Workbench and create a new connection with the DNS we grabbed from the database Connectivity and security settings: mydatabaseinstance.c83u6ye42fzy.us-east-1.rds.amazonaws.com



correct so far 5
# Class 03-15-26
#Note: each paragraph was a small note from each question asked during class. 

Only *aurora* can scale up and down. That is the only service in AWS that can scale 
- There's an Aurora serverless and provisioned 


ElastiCache milisecond latency - used for example to serve the leader board of an online game. Instead of having reading operations constantly done to the RDS you can store that output in an ElastiCache and serve it from there. 
- Whenever you want fast read operations go with ElastiCache 
- **I need to to an ElastiCache exercise**

For no SQL we have MongoDB and DynamoDB, very similar but which one you decide depends on the clients requirements 


DAX vs ElastiCache -> Dax is Dynamodb caching. It still uses the same DynamoDB specific cache so it can use DynamoDB APIs


Amazon keyspace is Apache Cassandra, you can migrate an apache cassandra database. Fully managed service

AWS Fargate *Review this*. Lambda is for operations that at less than 15 minutes long 

AWS Compute Optimizer 




