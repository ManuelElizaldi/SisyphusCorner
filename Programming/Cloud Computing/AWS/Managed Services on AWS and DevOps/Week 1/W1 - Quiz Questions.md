**In an e-commerce application which service seems like a good fit for processing a paid-up order that can be fulfilled at a later point in time?**
SQS - The order ID can be queued for later processing depending on logistics and warehouse operations.


**Your customer has an application which writes and reads a lot of data from a database. The application is under stress due to heavy demand, and so is the database. Due to its stateless nature, the application is leveraging elasticity principles to scale, but the database is struggling to keep up. What are your best fit options? (Select two)**

Evaluate a higher machine specification for the database perhaps with more CPU and Memory
Add a caching layer to cache frequently read data

Increasing the size of the database server enhances its processing power and memory capacity, allowing it to handle more simultaneous queries and transactions. This leads to improved response times and higher throughput, enabling the server to serve more requests per second.

Adding a cache stores frequently accessed data temporarily, allowing faster retrieval by reducing repeated database queries. This minimizes the load and improves overall performance and efficiency.

*why maintaining more the one copy was not an option:*
Splitting an RDBMS is challenging because maintaining ACID properties and ensuring data consistency across distributed nodes requires complex transaction management and synchronization. Additionally, optimizing query performance across split databases involves intricate data partitioning and balancing and hence it is not the right choice.


**Like security, monitoring and observability are required for all teams who operate and administer cloud applications and services. Your teams must define, capture, and analyze operations metrics to gain visibility into workload events so that you can take appropriate action. In the management layer, this also means understanding operational metrics as you provide guardrails, network, security, and identity services in your management platform. Which AWS services cater to these enterprise needs?**
Cloud Trail and Cloud Watch
AWS CloudTrail is an AWS service that helps you enable operational and risk auditing, governance, and compliance of your AWS account. Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications.

**In a multi-AZ environment, RDS___**
primary is created in an AZ. Admin has to trigger the secondary DB creation in another AZ

RDS creates a primary DB instance in one AZ and a replica in another one. A read replica can be created once the primary is ready

**Which cannot be an subscriber for SNS topics?**
VPC

Lambda, email, sms, can subscribe

**Which service can be used to run SQL queries on data stored in S3**
Athena

Athena helps you analyze data in S3 using SQL syntax. Its serverless so there's nothing to manage, but you pay for the queries that you run.

**In which of the following scenarios would you use FIFO queues over the Standard queue in SQS?**
Order of message is important - FIFO guarantees deliver of messages 

**A developer has created a MySQL RDS instance at his work (office desktop). All the default settings were used except for the username and password. Later in the evening, he attempts to connect to the instance using a Java program from his laptop at home with JDBC drivers but is unable to do so. What could be the "main reason" for this?**
The RDS security group that got created allows access from a specific IP address (mostly the router at work or the developer's desktop)

The default RDS security group will only allow access to the database from the IP address of the machine where the RDS instance was created (work desktop)

