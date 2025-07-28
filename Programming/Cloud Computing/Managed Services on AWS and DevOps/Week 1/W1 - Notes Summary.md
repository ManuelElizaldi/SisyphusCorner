**Class Notes – Managed Services on AWS and DevOps Week 1**
# Amazon SNS

Amazon Simple Notification Service (Amazon SNS) is a managed service that provides message delivery from publishers to subscribers (also known as _producers_ and _consumers_). Publishers communicate asynchronously with subscribers by sending messages to a _topic_, which is a logical access point and communication channel. Clients can subscribe to the SNS topic and receive published messages using a supported endpoint type, such as Amazon Kinesis Data Firehose, Amazon SQS, AWS Lambda, HTTP, email, mobile push notifications, and mobile text messages (SMS).

![](file:///tmp/lu1473514f9wnk.tmp/lu1473514f9wr2_tmp_932f6158.png)

# Features

Amazon SNS provides the following features and capabilities:

1. **Application-to-application messaging**  
    Application-to-application messaging supports subscribers such as Amazon Kinesis Data Firehose delivery streams, Lambda functions, Amazon SQS queues, HTTP/S endpoints, and AWS Event Fork Pipelines.
    
2. **Application-to-person notifications**  
    Application-to-person notifications provide user notifications to subscribers such as mobile applications, mobile phone numbers, and email addresses.
    
3. **Standard and FIFO topics**  
    Use a FIFO topic to ensure strict message ordering, to define message groups, and to prevent message duplication. Only Amazon SQS FIFO queues can subscribe to a FIFO topic. Use a standard topic when message delivery order and possible message duplication are not critical. All of the supported delivery protocols can subscribe to a standard topic.
    
4. **Message durability**  
    Amazon SNS uses a number of strategies that work together to provide message durability:
    

- Published messages are stored across multiple, geographically separated servers and data centers.
    
- If a subscribed endpoint isn't available, Amazon SNS runs a delivery retry policy.
    
- To preserve any messages that aren't delivered before the delivery retry policy ends, you can create a dead-letter queue.
    

5. **Message archiving and analytics**  
    You can subscribe Kinesis Data Firehose delivery streams to SNS topics, which allow you to send notifications to additional archiving and analytics endpoints such as Amazon Simple Storage Service (Amazon S3) buckets, Amazon Redshift tables, and more.
    
6. **Message attributes**  
    Message attributes let you provide any arbitrary metadata about the message.
    
7. **Message filtering**  
    By default, each subscriber receives every message published to the topic. To receive a subset of the messages, a subscriber must assign a filter policy to the topic subscription. A subscriber can also define the filter policy scope to enable payload-based or attribute-based filtering. The default value for the filter policy scope is MessageAttributes. When the incoming message attributes match the filter policy attributes, the message is delivered to the subscribed endpoint. Otherwise, the message is filtered out. When the filter policy scope is MessageBody, filter policy attributes are matched against the payload.
    
8. **Message security**  
    Server-side encryption protects the contents of messages that are stored in Amazon SNS topics, using encryption keys provided by AWS KMS.  
    You can also establish a private connection between Amazon SNS and your virtual private cloud (VPC).
    

  

  

  

# SQS

Amazon Simple Queue Service (Amazon SQS) offers a secure, durable, and available hosted queue that lets you integrate and decouple distributed software systems and components. Amazon SQS offers common constructs such as dead-letter queues and cost allocation tags. It provides a generic web services API that you can access using any programming language that the AWS SDK supports.

![](file:///tmp/lu1473514f9wnk.tmp/lu1473514f9wr2_tmp_79444960.png)

# Features

1. Functionality
    

- **Unlimited queues and messages:** Create unlimited Amazon SQS queues with an unlimited number of messages in any Region
    
- **Payload Size:** Message payloads can contain up to 256KB of text in any format. Each 64KB ‘chunk’ of payload is billed as 1 request. For example, a single API call with a 256KB payload will be billed as four requests. To send messages larger than 256KB, you can use the Amazon SQS Extended Client Library for Java, which uses Amazon Simple Storage Service (S3) to store the message payload. A reference to the message payload is sent using SQS.
    
- **Batches:** Send, receive, or delete messages in batches of up to 10 messages or 256KB. Batches cost the same amount as single messages, meaning SQS can be even more cost effective for customers that use batching.
    
- **Long polling:** Reduce extraneous polling to minimize cost while receiving new messages as quickly as possible. When your queue is empty, long-poll requests wait up to 20 seconds for the next message to arrive. Long poll requests cost the same amount as regular requests.
    
- Retain messages in queues for up to 14 days.
    
- Send and read messages simultaneously.
    
- **Message locking:** When a message is received, it becomes “locked” while being processed. This keeps other computers from processing the message simultaneously. If the message processing fails, the lock will expire and the message will be available again.
    
- **Queue sharing:** Securely share Amazon SQS queues anonymously or with specific AWS accounts. Queue sharing can also be restricted by IP address and time-of-day.
    
- **Server-side encryption (SSE):** Protect the contents of messages in Amazon SQS queues using keys managed in the AWS Key Management Service (AWS KMS). SSE encrypts messages as soon as Amazon SQS receives them. The messages are stored in encrypted form and Amazon SQS decrypts messages only when they are sent to an authorized consumer.
    
- **Dead Letter Queues (DLQ):** Handle messages that a consumer has not successfully processed with dead- letter queues (DLQs). When a message's maximum receive count is exceeded, Amazon SQS moves the message to the DLQ associated with the original queue. DLQs must be of the same type as the source queue (standard or FIFO). You can inspect the messages in DLQs to understand why your consumer has not successfully received them. Once you have remediated the issues, you can move the messages from the DLQ to their respective source queues.
    

2. Using Amazon SQS with other AWS infrastructure web services
    

Amazon SQS message queuing can be used with other AWS services such as Amazon Redshift, Amazon DynamoDB, Amazon Relational Database Service (RDS), Amazon Elastic Compute Cloud (EC2), Amazon Elastic Container Service (ECS), AWS Lambda, and Amazon S3, to make distributed applications more scalable and reliable. Below are some common design patterns:

- **Work Queues:** Decouple components of a distributed application that may not all process the same amount of work simultaneously.
    
- **Buffer and Batch Operations:** Add scalability and reliability to your architecture, and smooth out temporary volume spikes without losing messages or increasing latency.
    
- **Request Offloading:** Move slow operations off of interactive request paths by enqueuing the request.
    
- **Fanout:** Combine SQS with Simple Notification Service (SNS) to send identical copies of a message to multiple queues in parallel.
    
- **Priority:** Use separate queues to provide prioritization of work.
    
- **Scalability:** Because message queues decouple your processes, it’s easy to scale up the send or receive rate of messages — simply add another process.
    
- **Resiliency:** When part of your system fails, it doesn’t need to take the entire system down. Message queues decouple components of your system, so if a process that is reading messages from the queue fails, messages can still be added to the queue to be processed when the system recovers.
    

  

  

  

  

  

  

# RDS

Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database in the AWS Cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks.

![](file:///tmp/lu1473514f9wnk.tmp/lu1473514f9wr2_tmp_916af6ee.png)

# Features

1. **Lower administrative burden**
    

- Easy to use
    

- Amazon RDS Blue/Green Deployments
    
- Automatic software patching
    
- Best practice recommendations
    

2. **Performance**
    

- General Purpose (SSD) Storage
    
- Provisioned IOPS (SSD) Storage
    
- Amazon RDS Optimized Writes
    
- Amazon RDS Optimized Reads
    

3. **Scalability**
    

- Push-button compute scaling
    
- Easy storage scaling
    
- Read Replicas
    

4. **Availability and durability**
    

- Automated backups
    
- Database snapshots
    
- Multi-AZ deployments
    
- Automatic host replacement
    

5. **Security**
    

- Encryption at rest and in transit
    
- Network isolation
    
- Resource-level permissions
    

6. **Manageability**
    

- Monitoring and metrics
    
- Event notifications
    
- Configuration governance
    

7. **Cost-effectiveness**
    

- Pay only for what you use
    
- Reserved instances
    
- Stop and start
    

8. **Developer Productivity**
    

- Trusted Language Extensions for PostgreSQL
    

# Elasticache

Amazon ElastiCache is a web service that makes it easy to set up, manage, and scale a distributed in-memory data store or cache environment in the cloud. It provides a high-performance, scalable, and cost-effective caching solution. At the same time, it helps remove the complexity associated with deploying and managing a distributed cache environment.

  

![](file:///tmp/lu1473514f9wnk.tmp/lu1473514f9wr2_tmp_48ea9a55.png)

# Features

Amazon ElastiCache provides:

- Support for two engines: Memcached and Redis
    
- Ease of management via the AWS Management Console. With a few clicks you can configure and launch cache nodes for the engine you wish to use.
    
- Compatibility with the specific engine protocol. This means most of the client libraries will work with the respective engines they were built for - no additional changes or tweaking required.
    
- Detailed monitoring statistics for the engine nodes at no extra cost via Amazon CloudWatch
    
- Pay only for the resources you consume based on node hours used
    

  

# CloudWatch

Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real time. You can use CloudWatch to collect and track metrics, which are variables you can measure for your resources and applications.

The CloudWatch home page automatically displays metrics about every AWS service you use. You can additionally create custom dashboards to display metrics about your custom applications, and display custom collections of metrics that you choose.

# Features

![](file:///tmp/lu1473514f9wnk.tmp/lu1473514f9wr2_tmp_f85b8a99.png)

1. **Collect**
    

- Easily collect and store logs
    
- Collect and aggregate infrastructure and application metrics
    
- Collect and aggregate container metrics and logs
    
- Collect and aggregate Lambda metrics and logs
    
- Stream Metrics
    

2. **Monitor**
    

- Cross-account observability across multiple AWS accounts
    
- Unified operational view with dashboards
    
- Composite alarms
    
- High-resolution alarms
    
- Logs and metrics correlation
    
- Application Insights
    
- Container monitoring insights
    
- Internet Monitor (preview)
    
- Lambda monitoring insights
    
- Anomaly Detection
    
- ServiceLens
    
- Synthetics
    
- RUM
    

3. **Act**
    

- Auto Scaling
    

- Automate response to operational changes with CloudWatch Events
    

- Alarm and automate actions on EKS, ECS, and k8s clusters
    

4. **Analyze**
    

- Granular data and extended retention
    
- Custom operations on metrics
    
- Log analytics
    
- Analyze container metrics, logs, and traces
    
- Analyze Lambda metrics, logs, and traces
    
- Contributor Insights
    
- Metrics Insights
    
- Evidently
    

5. **Compliance and Security**
    

Amazon CloudWatch is integrated with AWS Identity and Access Management (IAM) so you can control which users and resources have permission to access your data and how they can access it. Amazon CloudWatch Logs is also PCI and FedRamp compliant. Data is encrypted at rest and in transit. You can also use AWS Key Management Service (AWS KMS) encryption to encrypt your log groups for added compliance and security.

Amazon CloudWatch Logs data protection helps you to define data protection policies that can discover and protect sensitive data logged by systems and applications. This feature automatically identiﬁes and masks sensitive information in your logs using ML and pattern matching based on the policy that you define. Data protection can help you streamline your architecture by offloading data protection logic from your applications, while helping support your compliance objectives. You can define your data protection policies to scan logs as they are ingested to determine how much sensitive data they contain and mask sensitive data that is detected. Masked data can also be unmasked for validation by security engineers through elevated privileges with IAM.

# Concepts

1. **Namespaces**
    

A _namespace_ is a container for CloudWatch metrics. Metrics in different namespaces are isolated from each other, so that metrics from different applications are not mistakenly aggregated into the same statistics.

2. **Metrics**
    

_Metrics_ are the fundamental concept in CloudWatch. A metric represents a time-ordered set of data points that are published to CloudWatch. Think of a metric as a variable to monitor, and the data points as representing the values of that variable over time. For example, the CPU usage of a particular EC2 instance is one metric provided by Amazon EC2. The data points themselves can come from any application or business activity from which you collect data.

3. **Time stamps**
    

Each metric data point must be associated with a time stamp. The time stamp can be up to two weeks in the past and up to two hours into the future. If you do not provide a time stamp, CloudWatch creates a time stamp for you based on the time the data point was received.

4. **Metrics retention**
    

CloudWatch retains metric data as follows:

- Data points with a period of less than 60 seconds are available for 3 hours. These data points are high-resolution custom metrics.
    
- Data points with a period of 60 seconds (1 minute) are available for 15 days
    
- Data points with a period of 300 seconds (5 minute) are available for 63 days
    
- Data points with a period of 3600 seconds (1 hour) are available for 455 days (15 months)
    

5. **Dimensions**
    

A _dimension_ is a name/value pair that is part of the identity of a metric. You can assign up to 30 dimensions to a metric.

AWS services that send data to CloudWatch attach dimensions to each metric. You can use dimensions to filter the results that CloudWatch returns. For example, you can get statistics for a specific EC2 instance by specifying the InstanceId dimension when you search for metrics.

6. **Dimension combinations**
    

CloudWatch treats each unique combination of dimensions as a separate metric, even if the metrics have the same metric name. You can only retrieve statistics using combinations of dimensions that you specifically published. When you retrieve statistics, specify the same values for the namespace, metric name, and dimension parameters that were used when the metrics were created. You can also specify the start and end times for CloudWatch to use for aggregation.

7. **Resolution**
    

Each metric is one of the following:

- Standard resolution, with data having a one-minute granularity
    
- High resolution, with data at a granularity of one second
    

8. **Statistics**
    

_Statistics_ are metric data aggregations over specified periods of time. CloudWatch provides statistics based on the metric data points provided by your custom data or provided by other AWS services to CloudWatch. Aggregations are made using the namespace, metric name, dimensions, and the data point unit of measure, within the time period you specify.

9. **Units**
    

You can specify a unit when you create a custom metric. If you do not specify a unit, CloudWatch uses None as the unit. Units help provide conceptual meaning to your data. Though CloudWatch attaches no significance to a unit internally, other applications can derive semantic information based on the unit.

10. **Periods**
    

A _period_ is the length of time associated with a specific Amazon CloudWatch statistic. Each statistic represents an aggregation of the metrics data collected for a specified period of time. Periods are defined in numbers of seconds, and valid values for period are 1, 5, 10, 30, or any multiple of 60. For example, to specify a period of six minutes, use 360 as the period value. You can adjust how the data is aggregated by varying the length of the period. A period can be as short as one second or as long as one day (86,400 seconds). The default value is 60 seconds.

11. **Aggregation**
    

Amazon CloudWatch aggregates statistics according to the period length that you specify when retrieving statistics. You can publish as many data points as you want with the same or similar time stamps. CloudWatch aggregates them according to the specified period length. CloudWatch does not automatically aggregate data across Regions, but you can use metric math to aggregate metrics from different Regions.

12. **Percentiles**
    

A _percentile_ indicates the relative standing of a value in a dataset. For example, the 95th percentile means that 95 percent of the data is lower than this value and 5 percent of the data is higher than this value. Percentiles help you get a better understanding of the distribution of your metric data.

13. **Alarms**
    

You can use an _alarm_ to automatically initiate actions on your behalf. An alarm watches a single metric over a specified time period, and performs one or more specified actions, based on the value of the metric relative to a threshold over time. The action is a notification sent to an Amazon SNS topic or an Auto Scaling policy. You can also add alarms to dashboards.

  
  

References

1. SNS Documentation - [https://docs.aws.amazon.com/sns/](https://docs.aws.amazon.com/sns/)
    
2. SQS Documentation - [https://docs.aws.amazon.com/sqs/](https://docs.aws.amazon.com/sqs/)
    
3. RDS Documentation - [https://docs.aws.amazon.com/rds/](https://docs.aws.amazon.com/rds/)
    
4. Elasticache Documentation - [https://docs.aws.amazon.com/elasticache/](https://docs.aws.amazon.com/elasticache/)
    
5. CloudWatch Documentation - [https://docs.aws.amazon.com/cloudwatch/](https://docs.aws.amazon.com/cloudwatch/)
    

Datasheets

1. SNS: - [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_SNS_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_SNS_Datasheet.pdf)
    
2. SQS: [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_SQS_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_SQS_Datasheet.pdf)
    
3. RDS: [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_RDS_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_RDS_Datasheet.pdf)
    
4. Elasticache: [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_ElastiCache_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_ElastiCache_Datasheet.pdf)
    
5. CloudWatch: [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_CloudWatch_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_CloudWatch_Datasheet.pdf)