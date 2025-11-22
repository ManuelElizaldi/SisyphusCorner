**Microsoft Azure - 7**

  

**Azure Messaging Services**

**Azure Queue Storage**

- Azure Queue Storage is a service for storing large numbers of messages.
    
- You access messages from anywhere in the world via authenticated calls using HTTP or HTTPS.
    
- A queue message can be up to 64 KB in size.
    
- A queue may contain millions of messages, up to the total capacity limit of a storage account.
    
- Queues are commonly used to create a backlog of work to process asynchronously.
    

  

**Azure Service Bus**

- Azure Service Bus is a fully managed enterprise message broker with message queues and publish-subscribe topics
    
- Service Bus is used to decouple applications and services from each other, providing the following benefits:
    
    - Load-balancing work across competing workers
        
    - Safely routing and transferring data and control across service and application boundaries
        
    - Coordinating transactional work that requires a high-degree of reliability
        
    - Provides a variety of use cases
        
- Data is transferred between different applications and services using messages.
    
- A message is a container decorated with metadata, and contains data. The data can be any kind of information, including structured data encoded with the common formats such as the following ones: JSON, XML, Apache Avro, Plain Text.
    
- Uses AMOP 1.0 (advanced messaging queueing protocol)
    
- **At-least once processing:** If the application crashes after it processes the message, but before it requests the Service Bus service to complete the message, Service Bus redelivers the message to the application when it restarts.
    
- **Exactly once processing:** If your scenario can't tolerate duplicate processing, add additional logic in your application to detect duplicates.
    

  

**Queues:**

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_f0684bc0.png)

- Messages are sent to and received from queues. Queues store messages until the receiving application is available to receive and process them.
    
- Works on first-in-first-out method
    
- Messages in queues are ordered and timestamped on arrival.
    
- Once the broker accepts the message, the message is always held durably in triple-redundant storage, spread across availability zones if the namespace is zone-enabled.
    
- Service Bus keeps messages in memory or volatile storage until they've been reported by the client as accepted.
    
- Messages are delivered in pull mode, only delivering messages when requested. Unlike the busy-polling model of some other cloud queues, the pull operation can be long-lived and only complete once a message is available.
    

  

**Different types of Queueing Design Pattern**

- **Queue-based Load Leveling Pattern-**
    
    - The sender sends messages at its own pace
        
    - The receiver receives messages at its own pace
        

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_bc8e134e.png)

- **Competing Consumer Pattern-** there will be multiple receivers (consumers) of the queue, which will pick the messages in parallel from the queue and then process them.
    

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_f0bd914e.png)

- Enable multiple concurrent consumers to process messages received on the same messaging channel.
    
- With multiple concurrent consumers, a system can process multiple messages concurrently to optimize throughput, to improve scalability and availability, and to balance the workload.
    

- **Priority Queue Pattern-**
    

Prioritize requests sent to services so that requests with a higher priority are received and processed more quickly than those with a lower priority. This pattern is useful in applications that offer different service level guarantees to individual clients.

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_921f4118.png)

- **Publisher/Subscriber Pattern-** In this case, one message will be added to multiple queues, and consumers of the particular queue will receive the message and then process it.![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_a41d64a3.png)
    

Pub/sub messaging has the following benefits:

- It decouples subsystems that still need to communicate. Subsystems can be managed independently, and messages can be properly managed even if one or more receivers are offline.
    
- It increases scalability and improves responsiveness of the sender. The sender can quickly send a single message to the input channel, then return to its core processing responsibilities. The messaging infrastructure is responsible for ensuring messages are delivered to interested subscribers.
    
- It improves reliability. Asynchronous messaging helps applications continue to run smoothly under increased loads and handle intermittent failures more effectively.
    
- It allows for deferred or scheduled processing. Subscribers can wait to pick up messages until off-peak hours, or messages can be routed or processed according to a specific schedule.
    
- It enables simpler integration between systems using different platforms, programming languages, or communication protocols, as well as between on-premises systems and applications running in the cloud.
    
- It facilitates asynchronous workflows across an enterprise.
    
- It improves testability. Channels can be monitored and messages can be inspected or logged as part of an overall integration test strategy.
    
- It provides separation of concerns for your applications. Each application can focus on its core capabilities, while the messaging infrastructure handles everything required to reliably route messages to multiple consumers.
    

  

**Termnilogies**

- **The dead-letter queue:** The purpose of the dead-letter queue is to hold messages that can't be delivered to any receiver, or messages that couldn't be processed.
    
- **Time to live**: if no consumer will receive the message, then the message will be automatically deleted after a period of time.
    
- **Lock duration:** If the consumer receives the message and does not respond within the specified time (that it has processed the message), then the message will be unlocked and appear in the queue again.
    
- **Maximum delivery count:** There's a limit on the number of attempts to deliver messages for Service Bus queues and subscriptions. The default value is 10.
    

  

**Topics:**

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_8bdc746a.png)

- You can also use topics to send and receive messages.
    
- While a queue is often used for point-to-point communication, topics are useful in publish/subscribe scenarios.
    
- Topics can have multiple, independent subscriptions, which attach to the topic and otherwise work exactly like queues from the receiver side.
    
- A subscriber to a topic can receive a copy of each message sent to that topic.
    

Subscriptions are named entities. Subscriptions are durable by default, but can be configured to expire and then be automatically deleted.

- Via the Java Message Service (JMS) API, Service Bus Premium also allows you to create volatile subscriptions that exist for the duration of the connection.
    
- You can define rules on a subscription.
    

A subscription rule has a filter to define a condition for the message to be copied into the subscription and an optional action that can modify message metadata.

- This feature is useful in the following scenarios:
    
    - You don't want a subscription to receive all messages sent to a topic.
        
    - You want to mark up messages with extra metadata when they pass through a subscription.
        
- Partitioning-
    
    - Service Bus partitions enable queues and topics, or messaging entities, to be partitioned across multiple message brokers.
        
    - Partitioning means that the overall throughput of a partitioned entity is no longer limited by the performance of a single message broker.
        
    - In addition, a temporary outage of a message broker, for example during an upgrade, doesn't render a partitioned queue or topic unavailable.
        
    - Partitioned queues and topics can contain all advanced Service Bus features, such as support for transactions and sessions
        

Namespaces

- A namespace is a container for all messaging components (queues and topics).
    
- Multiple queues and topics can be in a single namespace, and namespaces often serve as application containers.
    
- A namespace can be compared to a server in the terminology of other brokers, but the concepts aren't directly equivalent.
    
- A Service Bus namespace is your own capacity slice of a large cluster made up of dozens of all-active virtual machines.
    

  

Filters

- Subscribers can define which messages they want to receive from a topic.
    
- These messages are specified in the form of one or more named subscription rules.
    

Each rule consists of a filter condition that selects particular messages, and optionally contains an action that annotates the selected message.

- Service Bus supports three types of filters:
    
    - SQL filters- A SqlFilter holds a SQL-like conditional expression that's evaluated in the broker against the arriving messages' user-defined properties and system properties.
        

With SQL filter conditions, you can define an action that can annotate the message by adding, removing, or replacing properties and their values.

- Boolean filters- The TrueFilter and FalseFilter either cause all arriving messages (true) or none of the arriving messages (false) to be selected for the subscription. These two filters derive from the SQL filter.
    
- Correlation filters- A Correlation Filter holds a set of conditions that are matched against one or more of an arriving message's user and system properties.
    

  

**Azure Storage Queue vs Service Bus**

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_e0a2a5aa.png)

  

**Azure Event Hub**

- It is also a managed service.
    
- Azure Event Hubs is a cloud native data streaming service that can stream millions of events per second, with low latency, from any source to any destination.
    
- Event Hubs is compatible with Apache Kafka, and it enables you to run existing Kafka workloads without any code changes.
    
- Using Event Hubs to ingest and store streaming data, businesses can harness the power of streaming data to gain valuable insights, drive real-time analytics, and respond to events as they happen, enhancing overall efficiency and customer experience.
    

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_4409fa71.png)

- Event Hubs provides a unified event streaming platform with time retention buffer, decoupling event producers from event consumers.
    
- The producers and consumer applications can perform large scale data ingestion through multiple protocols.
    

  

**Key components of Event Hubs architecture:**

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_155a6b50.png)

- **Producer applications-** It can ingest data to an event hub using Event Hubs SDKs or any Kafka producer client.
    
- **Namespace**- It is the management container for one or more event hubs or Kafka topics. The management tasks such as allocating streaming capacity, configuring network security, enabling Geo Disaster recovery etc. are handled at the namespace level.
    
- **Event Hub/Kafka topic:** In Event Hubs, you can organize events into an event hub or a Kafka topic. It's an append only distributed log, which can comprise of one or more partitions.
    
- **Partitions-**
    
    - They are used to scale an event hub. They are like lanes in a freeway.
        
    - If you need more streaming throughput, you need to add more partitions.
        
    - If user will not use partitioning, then data will go in round robin pattern.
        
    - It also creates higher availability.
        
    - Event Hubs organizes sequences of events sent to an event hub into one or more partitions. As newer events arrive, they're added to the end of this sequence.
        

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_5a62e037.png)

- A partition can be thought of as a "commit log". Partitions hold event data that contains body of the event, a user-defined property bag describing the event, metadata such as its offset in the partition, its number in the stream sequence, and service-side timestamp at which it was accepted.
    

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_ee840ca7.png)

- Each event stores its content in its value. Besides the value, each event also contains a key, as the following diagram shows:
    

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_3a515979.png)

**Partition IDs** can be used when consumers are only interested in certain events. When those events flow to a single partition, the consumer can easily receive them by subscribing to that partition.

**Keys** can be used when consumers need to receive events in production order. Since all events with the same key go to the same partition, events with key values can maintain their order during processing. Consumers then receive them in that order.

  

**Advantages of using partitions**

Event Hubs is designed to help with processing of large volumes of events, and partitioning helps with that in two ways:

1. Even though Event Hubs is a PaaS service, there's a physical reality underneath, and maintaining a log that preserves the order of events requires that these events are being kept together in the underlying storage and its replicas and that results in a throughput ceiling for such a log. Partitioning allows for multiple parallel logs to be used for the same event hub and therefore multiplying the available raw IO throughput capacity.
    
2. Your own applications must be able to keep up with processing the volume of events that are being sent into an event hub. It may be complex and requires substantial, scaled-out, parallel processing capacity. The capacity of a single process to handle events is limited, so you need several processes. Partitions are how your solution feeds those processes and yet ensures that each event has a clear processing owner.
    

  

- **Consumer applications-** They consume data by seeking through the event log and maintaining consumer offset. Consumers can be Kafka consumer clients or Event Hubs SDK clients.
    
- **Consumer Group-** It is a logical group of consumer instances that reads data from an event hub/Kafka topic. It enables multiple consumers to read the same streaming data in an event hub independently at their own pace and with their own offsets.
    
- **Event Data-** It is a data/messgae which event producers produce.
    
- **Auto inflate-** With Event Hubs, you can start with data streams in megabytes, and grow to gigabytes or terabytes. This feature is one of the many options available to scale the number of throughput units or processing units to meet your usage needs.
    
- **Message Retaintion**- User can retain the message upto 7 days depending upon the pricing tier
    
- **Event Hubs Capture-** It enables you to automatically capture the streaming data in Event Hubs and save it to your choice of either a Blob storage account, or an Azure Data Lake Storage account.
    
- **Throughput units-** The throughput capacity of Event Hubs is controlled by throughput units. Throughput units are pre-purchased units of capacity. A single throughput unit lets you:
    
    - Ingress: Up to 1 MB per second or 1000 events per second (whichever comes first).
        
    - Egress: Up to 2 MB per second or 4096 events per second.
        

  

**Azure Event Grid**

- Azure Event Grid is a highly scalable, fully managed Pub Sub message distribution service that offers flexible message consumption patterns using the MQTT and HTTP protocols.
    
- With Azure Event Grid, users can build data pipelines with device data, integrate applications, and build event-driven serverless architectures.
    
- Event Grid enables clients to publish and subscribe to messages over the MQTT v3.1.1 and v5.0 protocols to support Internet of Things (IoT) solutions.
    
- Through HTTP, Event Grid enables you to build event-driven solutions where a publisher service announces its system state changes (events) to subscriber applications.
    
- Event Grid can be configured to send events to subscribers (push delivery) or subscribers can connect to Event Grid to read events (pull delivery).
    

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_1ba72b5e.png)

**Event**

- An event is the smallest amount of information that fully describes something that happened in a system.
    
- It represents a distinct, self-standing fact about a system that provides an insight that can be actionable.
    

**Topics and event subscriptions**

- Events published to Event Grid land on a topic, which is a resource that logically contains all events.
    
- An event subscription is a configuration resource associated with a single topic.
    
- Event subscription can be used to set event selection criteria to define the event collection available to a subscriber out of the total set of events present in a topic.
    

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_10fc4266.png)

**Push and pull delivery**

- Using HTTP, Event Grid supports push and pull event delivery.
    
- With push delivery, you define a destination in an event subscription, a webhook or an Azure service, to which Event Grid sends events.
    

Push delivery is supported in custom topics, system topics, domain topics and partner topics.

- With pull delivery, subscriber applications connect to Event Grid to consume events. Pull delivery is supported in topics within a namespace.
    

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_c4aae627.png)

  

  

  

**MQTT**

- MQTT is a publish-subscribe messaging transport protocol that was designed for constrained environments.
    
- It has become the go-to communication standard for IoT scenarios due to efficiency, scalability, and reliability.
    
- MQTT broker enables clients to publish and subscribe to messages over MQTT v3.1.1, MQTT v3.1.1 over WebSockets, MQTT v5, and MQTT v5 over WebSockets protocols.
    

**Data distribution using push and pull delivery modes**

- At any point in a data pipeline, HTTP applications can consume messages using push or pull APIs.
    
- The source of the data might include MQTT clients’ data, but also includes the following data sources that send their events over HTTP:
    
    - Azure services
        
    - Your custom applications
        
    - External partner (SaaS) systems
        

  

**Azure Resource Manager**

- Azure Resource Manager is the deployment and management service for Azure.
    
- It provides a management layer that enables you to create, update, and delete resources in your Azure account.
    
- You use management features, like access control, locks, and tags, to secure and organize your resources after deployment.
    
- User send a request through any of the Azure APIs, tools, or SDKs, Resource Manager receives the request. It authenticates and authorizes the request before forwarding it to the appropriate Azure service. Because all requests are handled through the same API, you see consistent results and capabilities in all the different tools.
    

![](file:///tmp/lu1683335g52yu.tmp/lu1683335g531s_tmp_a73f45ef.png)

  

**Terminologies**

- **Resource** - A manageable item that is available through Azure. Virtual machines, storage accounts, web apps, databases, and virtual networks are examples of resources. Resource groups, subscriptions, management groups, and tags are also examples of resources.
    
- **Resource group -** A container that holds related resources for an Azure solution. The resource group includes those resources that you want to manage as a group. You decide which resources belong in a resource group based on what makes the most sense for your organization.
    
- **Resource provider** - A service that supplies Azure resources. For example, a common resource provider is Microsoft.Compute, which supplies the virtual machine resource. Microsoft.Storage is another common resource provider.
    
- **Declarative syntax** - Syntax that lets you state "Here's what I intend to create" without having to write the sequence of programming commands to create it. ARM templates and Bicep files are examples of declarative syntax. In those files, you define the properties for the infrastructure to deploy to Azure.
    
- **ARM template** - A JavaScript Object Notation (JSON) file that defines one or more resources to deploy to a resource group, subscription, management group, or tenant. The template can be used to deploy the resources consistently and repeatedly.
    
- **Bicep file -** A file for declaratively deploying Azure resources. Bicep is a language that's been designed to provide the best authoring experience for infrastructure as code solutions in Azure.
    

  

**Benefits of using Resource Manager**

- Manage your infrastructure through declarative templates rather than scripts.
    
- Deploy, manage, and monitor all the resources for your solution as a group, rather than handling these resources individually.
    
- Redeploy your solution throughout the development lifecycle and have confidence your resources are deployed in a consistent state.
    
- Define the dependencies between resources so they're deployed in the correct order.
    
- Apply access control to all services because Azure role-based access control (Azure RBAC) is natively integrated into the management platform.
    
- Apply tags to resources to logically organize all the resources in your subscription.
    
- Clarify your organization's billing by viewing costs for a group of resources sharing the same tag.
    

  

**ARM templates consist of several sections, including:**

- **Parameters:** Provide values during deployment that customize the deployment for different environments. For example, you can define parameters such as storage account names with minimum and maximum length constraints.
    
- **Variables:** Define reusable values within the template to simplify complex expressions and improve readability. For example, you can declare a variable for the storage account type.
    
- **User-defined functions:** Create custom functions to encapsulate complex logic or calculations. You can define a function with a namespace, members, parameters, and output.
    
- **Resources:** Define the Azure resources to deploy or update. Resource definitions can include the resource type, API version, name, location, SKU, kind, and resource-specific properties.
    
- **Outputs:** Return values from the deployed resources for further processing or display. You can define output types and values, such as the storage account endpoint.