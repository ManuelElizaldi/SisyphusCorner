**Microsoft Azure - 6**
  

**Azure SQL Database**

- It is a fully managed platform as a service (PaaS) database engine that handles most of the database management functions such as upgrading, patching, backups, and monitoring without user involvement.
    
- Azure SQL Database is always running on the latest stable version of the SQL Server database engine and patched OS with 99.99% availability.
    
- PaaS capabilities built into Azure SQL Database enable you to focus on the domain-specific database administration and optimization activities that are critical for your business.
    
- With Azure SQL Database, you can create a highly available and high-performance data storage layer for the applications and solutions in Azure.
    
- SQL Database can be the right choice for a variety of modern cloud applications because it enables you to process both relational data and nonrelational structures, such as graphs, JSON, spatial, and XML.
    
- Azure SQL Database is based on the latest stable version of the Microsoft SQL Server database engine.
    
- You can use advanced query processing features, such as high-performance in-memory technologies and intelligent query processing. In fact, the newest capabilities of SQL Server are released first to Azure SQL Database, and then to SQL Server itself.
    
- You get the newest SQL Server capabilities with no overhead for patching or upgrading, tested across millions of databases.
    
- It is scalable and highly available
    
- It also supports geographical replication and failover
    

  

**Deployment models**

- SQL Server on Azure VM
    
    - You can deploy your own database on Azure VM
        
    - Azure also provides pre-built images with SQL Server on Azure VM
        
    - User will have full control over the created SQL server, databases, and other infrastructure
        
- SQL Database
    
    - It is a fully managed platform as a service (PaaS)
        
    - Most of the features of on-prem SQL servers are supported (some are not)
        
    - It is very inexpensive and highly scalable
        
    - It supports SQL Servers, MySQL and PostgreSQL Databases
        
- SQL Managed instance
    
    - It is a PaaS service that has nearly 100% compatibility with the latest Enterprise Edition SQL Server database engine, providing a native virtual network (VNet) implementation that addresses common security concerns, and a business model favorable to existing SQL Server customers.
        
    - SQL Managed Instance allows existing SQL Server customers to lift and shift their on-premises applications to the cloud with minimal application and database changes.
        
    - It will be deployed inside the Virtual Network
        
    - It is costlier than Azure SQL Database
        

  

**Logical Server in Azure SQL Database**

- A server is a logical construct that acts as a central administrative point for a collection of databases.
    
- At the logical server level, you can administer logins, firewall rules, auditing rules, threat detection policies, and auto-failover groups.
    
- A logical server can be in a different region than its resource group.
    
- The logical server must exist before you can create a database in Azure SQL Database. All databases managed by a single logical server are created within the same region as the logical server.
    

  

**Creating SQL Database**

- By default, the SQL server name will have the suffix database.windows.net
    
- Database collation-
    
    - Defines a collation of a database or table column, or a collation cast operation when applied to character string expression.
        
    - The collation name can be either a Windows collation name or a SQL collation name.
        
    - If not specified during database creation, the database is assigned the default collation of the instance of SQL Server. If not specified during table column creation, the column is assigned the default collation of the database.
        
- Workload environment-
    
    - The Azure portal provides a Workload environment option that helps to pre-set some configuration settings. These settings can be overridden.
        
    - This option applies to the Create SQL Database portal page only. Otherwise, the Workload environment option has no impact on licensing or other database configuration settings.
        
- Service tiers-
    
    - The vCore-based purchasing model offers three service tiers:
        
        - The General Purpose service tier is designed for common workloads. It offers budget-oriented balanced compute and storage options.
            
        - The Business Critical service tier is designed for OLTP applications with high transaction rates and low latency I/O requirements. It offers the highest resilience to failures by using several isolated replicas.
            
        - The Hyperscale service tier is designed for most business workloads. Hyperscale provides great flexibility and high performance with independently scalable compute and storage resources. It offers higher resilience to failures by allowing the configuration of more than one isolated database replica.
            
    - The DTU-based purchasing model offers two service tiers:
        
        - The Standard service tier is designed for common workloads. It offers budget-oriented balanced compute and storage options.
            
        - The Premium service tier is designed for OLTP applications with high transaction rates and low latency I/O requirements. It offers the highest resilience to failures by using several isolated replicas.
            

  

- **Connecting to SQL Database - Query Editor**
    
    - The Azure SQL Database Query editor (preview) is a tool to run SQL queries against Azure SQL Database in the Azure portal.
        
    - To connect with SQL authentication, under SQL server authentication, user needs to enter a Login and Password for a user that has access to the database.
        
    - You can type out your query in the query editor and run it.
        
    - Optionally, you can select Save query to save the query as an .sql file, or select Export data as to export the results as a .json, .csv, or .xml file.
        
    - Firewall and virtual networks in Azure SQL server-
        
        - By default, you can not connect to your created SQL servers until you manually give access
            
        - You need to create a Rule and add your IP address to give access
            
    - The user can also connect to their database using third party tools
        

**Database security-**

- Transparent Data Encryption (Encryption-at-rest)
    
    - Transparent data encryption (TDE) for SQL Database, SQL Managed Instance, and Azure Synapse Analytics adds a layer of security to help protect data at rest from unauthorized or offline access to raw files or backups.
        
    - Common scenarios include data center theft or unsecured disposal of hardware or media such as disk drives and backup tapes. TDE encrypts the entire database using an AES encryption algorithm, which doesn't require application developers to make any changes to existing applications.
        
    - In Azure, all newly created databases are encrypted by default and the database encryption key is protected by a built-in server certificate.
        
    - Certificate maintenance and rotation are managed by the service and require no input from the user.
        
- Auditing
    
    - SQL Database and SQL Managed Instance auditing tracks database activities and helps maintain compliance with security standards by recording database events to an audit log in a customer-owned Azure storage account.
        
    - Auditing allows users to monitor ongoing database activities, as well as analyze and investigate historical activity to identify potential threats or suspected abuse and security violations.
        
    - All the logs will be stored in azure storage account
        
    - You can have a custom retention period
        
- Data Masking
    
    - Dynamic data masking helps prevent unauthorized access to sensitive data by enabling customers to designate how much of the sensitive data to reveal with minimal effect on the application layer.
        
    - It's a policy-based security feature that hides the sensitive data in the result set of a query over designated database fields, while the data in the database isn't changed.
        
    - You set up a dynamic data masking policy in the Azure portal by selecting the Dynamic Data Masking blade under Security in your SQL Database configuration pane.
        
    - Dynamic data masking policy-
        
        - **SQL users excluded from masking:** A set of SQL users, which can include identities from Microsoft Entra ID (formerly Azure Active Directory), that get unmasked data in the SQL query results. Users with administrative rights like server admin, Microsoft Entra admin and db_owner role can view the original data without any mask. (Note: It also applies to sysadmin role in SQL Server)
            
        - **Masking rules:** A set of rules that define the designated fields to be masked and the masking function that is used. The designated fields can be defined using a database schema name, table name, and column name.
            
        - **Masking functions:** A set of methods that control the exposure of data for different scenarios.
            

**NoSQL**

- NoSQL, also referred to as “not only SQL”, “non-SQL”, is an approach to database design that enables the storage and querying of data outside the traditional structures found in relational databases.
    
- While it can still store data found within relational database management systems (RDBMS), it just stores it differently compared to an RDBMS.
    
- The decision to use a relational database versus a non-relational database is largely contextual, and it varies depending on the use case.
    
- Instead of the typical tabular structure of a relational database, NoSQL databases, house data within one data structure, such as JSON document.
    
- Since this non-relational database design does not require a schema, it offers rapid scalability to manage large and typically unstructured data sets.
    
- NoSQL is also type of distributed database, which means that information is copied and stored on various servers, which can be remote or local. This ensures availability and reliability of data. If some of the data goes offline, the rest of the database can continue to run.
    
- Each NoSQL database has its own unique features. At a high level, many NoSQL databases have the following features:
    
    - Flexible schemas
        
    - Horizontal scaling
        
    - Fast queries due to the data model
        
    - Ease of use for developers
        
- Types of data models with NoSQL databases-
    

1. Key-value- It stores pair keys and values using a hash table. Key-value types are best when a key is known and the associated value for the key is unknown.
    

  

Key features of the key-value store:

- Simplicity.
    
- Scalability.
    
- Speed.
    

  

2. Document- Document databases extend the concept of the key-value database by organizing entire documents into groups called collections. They support nested key-value pairs and allow queries on any attribute within a document.
    

  

Key features of documents database:

- Flexible schema: Documents in the database has a flexible schema. It means the documents in the database need not be the same schema.
    
- Faster creation and maintenance: the creation of documents is easy and minimal maintenance is required once we create the document.
    
- No foreign keys: There is no dynamic relationship between two documents so documents can be independent of one another. So, there is no requirement for a foreign key in a document database.
    
- Open formats: To build a document we use XML, JSON, and others
    

  

3. Columnar- Columnar, wide-column, or column-family databases efficiently store data and query across rows of sparse data and are advantageous when querying across specific columns in the database.
    

  

Key features of columnar oriented database:

- Scalability.
    
- Compression.
    
- Very responsive.
    

  

4. Graph- Graph databases use a model based on nodes and edges to represent interconnected data—such as relationships between people in a social network—and offer simplified storage and navigation through complex relationships.
    

  

Key features of graph database:

- In a graph-based database, it is easy to identify the relationship between the data by using the links.
    
- The Query’s output is real-time results.
    
- The speed depends upon the number of relationships among the database elements.
    
- Updating data is also easy, as adding a new node or edge to a graph database is a straightforward task that does not require significant schema changes.
    

  

**Azure Cosmos DB**

- It is a fully managed NoSQL and relational database for modern app development.
    
- It offers single-digit millisecond response times, automatic and instant scalability, along with guaranteed speed at any scale. Business continuity is assured with SLA-backed availability and enterprise-grade security.
    
- It supports all the NoSQL features such as-
    
    - Distribution
        
    - Replication
        
    - Horizontal scaling
        
    - High throughput
        
    - Low latency etc
        
- As a fully managed service, Azure Cosmos DB takes database administration off your hands with automatic management, updates and patching.
    
- It also handles capacity management with cost-effective serverless and automatic scaling options that respond to application needs to match capacity with demand.
    
- Build fast with open source APIs, multiple SDKs, schemaless data and no-ETL analytics over operational data.
    
- Users can choose from multiple database APIs including the native API for NoSQL, MongoDB, PostgreSQL, Apache Cassandra, Apache Gremlin, and Table.
    
- Azure Cosmos DB's schema-less service automatically indexes all your data, regardless of the data model, to deliver blazing fast queries.
    
- Gain unparalleled SLA-backed speed and throughput, fast global access, and instant elasticity.
    
    - Real-time access with fast read and write latencies globally, and throughput and consistency all backed by SLAs
        
    - Multi-region writes and data distribution to any Azure region with just a button.
        
    - Independently and elastically scale storage and throughput across any Azure region- even during unpredictable traffic bursts- for unlimited scale worldwide.
        
- Automatically expiration of documents using time-to-leave feature
    

  

**Considerations when choosing an API**

- API for NoSQL is native to Azure Cosmos DB.
    
- API for MongoDB, PostgreSQL, Cassandra, Gremlin, and Table implement the wire protocol of open-source database engines.
    
- These APIs are best suited if the following conditions are true:
    
    - If you have existing MongoDB, PostgreSQL Cassandra, or Gremlin applications
        
    - If you don't want to rewrite your entire data access layer
        
    - If you want to use the open-source developer ecosystem, client-drivers, expertise, and resources for your database
        
    - If you want to use the Azure Cosmos DB core features such as:
        
    - Global distribution
        
    - Elastic scaling of storage and throughput
        
    - High performance at scale
        
    - Low latency
        
    - Ability to run transactional and analytical workloads
        
    - Fully managed platform
        

  

- You can build new applications with these APIs or migrate your existing data. To run the migrated apps, change the connection string of your application and continue to run as before. When migrating existing apps, make sure to evaluate the feature support of these APIs.
    

1. **API for NoSQL**
    

- The Azure Cosmos DB API for NoSQL stores data in document format. It offers the best end-to-end experience as we have full control over the interface, service, and the SDK client libraries.
    
- Any new feature that is rolled out to Azure Cosmos DB is first available on API for NoSQL accounts. NoSQL accounts provide support for querying items using the Structured Query Language (SQL) syntax, one of the most familiar and popular query languages to query JSON objects.
    

2. **API for MongoDB**
    

- The Azure Cosmos DB API for MongoDB stores data in a document structure, via BSON format.
    
- It's compatible with MongoDB wire protocol; however, it doesn't use any native MongoDB related code.
    
- The API for MongoDB is a great choice if you want to use the broader MongoDB ecosystem and skills, without compromising on using Azure Cosmos DB features.
    

3. **API for Apache Cassandra**
    

- The Azure Cosmos DB API for Cassandra stores data in column-oriented schema.
    
- Apache Cassandra offers a highly distributed, horizontally scaling approach to storing large volumes of data while offering a flexible approach to a column-oriented schema.
    
- API for Cassandra in Azure Cosmos DB aligns with this philosophy to approaching distributed NoSQL databases.
    
- This API for Cassandra is wire protocol compatible with native Apache Cassandra. You should consider API for Cassandra if you want to benefit from the elasticity and fully managed nature of Azure Cosmos DB and still use most of the native Apache Cassandra features, tools, and ecosystem.
    
- This fully managed nature means on API for Cassandra you don't need to manage the OS, Java VM, garbage collector, read/write performance, nodes, clusters, etc.
    

4. **API for Apache Gremlin**
    

- The Azure Cosmos DB API for Gremlin allows users to make graph queries and stores data as edges and vertices.
    
- Use the API for Gremlin for scenarios:
    
    - Involving dynamic data
        
    - Involving data with complex relations
        
    - Involving data that is too complex to be modeled with relational databases
        
    - If you want to use the existing Gremlin ecosystem and skills
        
- The API for Gremlin combines the power of graph database algorithms with highly scalable, managed infrastructure.
    
- This API provides a unique and flexible solution to common data problems associated with lack of flexibility or relational approaches. API for Gremlin currently only supports OLTP scenarios.
    

5. **API for Table**
    

- The Azure Cosmos DB API for Table stores data in key/value format. If you're currently using Azure Table storage, you may see some limitations in latency, scaling, throughput, global distribution, index management, low query performance.
    
- API for Table overcomes these limitations and it's recommended to migrate your app if you want to use the benefits of Azure Cosmos DB.
    
- API for Table only supports OLTP scenarios.
    

  

**Creating a Cosmos DB account**

- **Subscription-** Select the Azure subscription that you want to use for this Azure Cosmos DB account.
    
- **Account Name-** Enter a name to identify your Azure Cosmos DB account. Because documents.azure.com is appended to the name that you provide to create your URI, use a unique name.
    
- **Location-**Select a geographic location to host your Azure Cosmos DB account. Use the location that is closest to your users to give them the fastest access to the data.
    
- **Capacity mode-** Select Provisioned throughput to create an account in provisioned throughput mode. Select Serverless to create an account in serverless mode.
    
- **Limit total account throughput-** Limit the total amount of throughput that can be provisioned on this account. This limit prevents unexpected charges related to provisioned throughput. You can update or remove this limit after your account is created.
    
- **Database throughput-** Manual throughput allows you to scale request units per second (RU/s) yourself whereas autoscale throughput allows the system to scale RU/s based on usage. Select Manual for this example.
    
- **Database Max RU/s-** If you want to reduce latency, you can scale up the throughput later by estimating the required RU/s with the capacity calculator.
    

Note: This setting isn't available when creating a new container in a serverless account.

- **Partition key-** The sample described in this article uses /category as the partition key.
    

  

The following image shows the hierarchy of different entities in an Azure Cosmos DB account:

![](file:///tmp/lu1423066dovsh.tmp/lu1423066dovwn_tmp_2d7adc05.png)

- **Azure Cosmos DB databases**
    

In Azure Cosmos DB, a database is similar to a namespace. A database is simply a group of containers.

- **Azure Cosmos DB containers**
    
    - An Azure Cosmos DB container is where data is stored.
        
    - Unlike most relational databases which scale up with larger VM sizes, Azure Cosmos DB scales out. Data is stored on one or more servers, called partitions.
        
    - To increase throughput or storage, more partitions are added.
        
    - This relationship provides a virtually an unlimited amount of throughput and storage for a container.
        
    - When you create a container, you configure throughput in one of the following modes:
        
        - **Dedicated throughput:** The throughput on a container is exclusively reserved for that container. There are two types of dedicated throughput, standard and autoscale.
            
        - **Shared throughput:** Here throughput is specified at the database level, then shared with up to 25 containers within the database. Sharing of throughput excludes containers that have been configured with their own dedicated throughput.
            
- **Azure Cosmos DB items**
    
    - Every Azure Cosmos DB item has the following system-defined properties. Depending on which API you use, some of them might not be directly exposed.
        

  

![](file:///tmp/lu1423066dovsh.tmp/lu1423066dovwn_tmp_bc192d43.png)

NOTE: Uniqueness of the id property is enforced within each logical partition. Multiple documents can have the same id property with different partition key values.

  

**Triggers and Bindings-**

- Triggers cause a function to run. A trigger defines how a function is invoked and a function must have exactly one trigger. Triggers have associated data, which is often provided as the payload of the function.
    
- Binding to a function is a way of declaratively connecting another resource to the function; bindings may be connected as input bindings, output bindings, or both. Data from bindings is provided to the function as parameters.
    
- You can mix and match different bindings to suit your needs. Bindings are optional and a function might have one or multiple input and/or output bindings.
    
- Triggers and bindings let you avoid hardcoding access to other services. Your function receives data (for example, the content of a queue message) in function parameters. You send data (for example, to create a queue message) by using the return value of the function.
    
- All triggers and bindings have a direction property in the function.json file:
    
    - For triggers, the direction is always in
        
    - Input and output bindings use in and out
        
    - Some bindings support a special direction inout. If you use inout, only the Advanced editor is available via the Integrate tab in the portal.
        
- You can create custom input and output bindings. Bindings must be authored in .NET, but can be consumed from any supported language.