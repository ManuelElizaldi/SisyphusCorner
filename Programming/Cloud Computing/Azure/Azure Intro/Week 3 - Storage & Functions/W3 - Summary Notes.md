**Microsoft Azure - 3**

  

**Azure Storage**

- The Azure Storage platform is Microsoft's cloud storage solution for modern data storage scenarios.
    
- Azure Storage offers highly available, massively scalable, durable, and secure storage for a variety of data objects in the cloud.
    
- Azure Storage data objects are accessible from anywhere in the world over HTTP or HTTPS via a REST API.
    
- Azure Storage also offers client libraries for developers building applications or services with .NET, Java, Python, JavaScript, C++, and Go.
    
- Developers and IT professionals can use Azure PowerShell and Azure CLI to write scripts for data management or configuration tasks.
    

  

**Benefits of Azure Storage**

- **Durable and highly available-** Redundancy ensures that your data is safe in the event of transient hardware failures. You can also replicate data across data centers or geographical regions for additional protection from local catastrophes or natural disasters. Data replicated in this way remains highly available in the event of an unexpected outage.
    
- **Secure-** All data written to an Azure storage account is encrypted by the service. Azure Storage provides you with fine-grained control over who has access to your data.
    
- **Scalable-** Azure Storage is designed to be massively scalable to meet the data storage and performance needs of today's applications.
    
- **Managed-** Azure handles hardware maintenance, updates, and critical issues for you.
    
- **Accessible-** Data in Azure Storage is accessible from anywhere in the world over HTTP or HTTPS. Microsoft provides client libraries for Azure Storage in a variety of languages, including .NET, Java, Node.js, Python, PHP, Ruby, Go, and others, as well as a mature REST API.
    

  

**Azure Storage services**

1. Blob Storage-
    

- Azure Blob Storage is Microsoft's object storage solution for the cloud. Blob Storage is optimized for storing massive amounts of unstructured data, such as text or binary data.
    
- Blob Storage is ideal for:
    
    - Serving images or documents directly to a browser.
        
    - Storing files for distributed access.
        
    - Streaming video and audio.
        
    - Storing data for backup and restore, disaster recovery, and archiving.
        
    - Storing data for analysis by an on-premises or Azure-hosted service.
        
- Objects in Blob Storage can be accessed from anywhere in the world via HTTP or HTTPS.
    
- Users or client applications can access blobs via URLs, the Azure Storage REST API, Azure PowerShell, Azure CLI, or an Azure Storage client library.
    
- The storage client libraries are available for multiple languages, including .NET, Java, Node.js, Python, PHP, and Ruby.
    
- Clients can also securely connect to Blob Storage by using SSH File Transfer Protocol (SFTP) and mount Blob Storage containers by using the Network File System (NFS) 3.0 protocol.
    

2. File Storage-
    

- Azure Files enables you to set up highly available network file shares that can be accessed by using the industry standard Server Message Block (SMB) protocol, Network File System (NFS) protocol, and Azure Files REST API.
    
- Multiple VMs can share the same files with both read and write access.
    
- The users can also read the files using the REST interface or the storage client libraries.
    
- One thing that distinguishes Azure Files from files on a corporate file share is that the users can access the files from anywhere in the world using a URL that points to the file and includes a shared access signature (SAS) token.
    
- The users can generate SAS tokens; they allow specific access to a private asset for a specific amount of time.
    

3. Queue Storage-
    

- Azure Queue Storage is a service for storing large numbers of messages.
    
- The users can access messages from anywhere in the world via authenticated calls using HTTP or HTTPS.
    
- A queue message can be up to 64 KB in size.
    
- A queue may contain millions of messages, up to the total capacity limit of a storage account.
    
- Queues are commonly used to create a backlog of work to process asynchronously.
    

  

4. Table Storage
    

- Azure Table storage is a service that stores non-relational structured data (also known as structured NoSQL data) in the cloud, providing a key/attribute store with a schemaless design.
    
- Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.
    
- Access to Table storage data is fast and cost-effective for many types of applications and is typically lower in cost than traditional SQL for similar volumes of data.
    
- The users can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.
    
- The users can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.
    
- Azure Table Storage is now part of Azure Cosmos DB and provides throughput-optimized tables, global distribution, and automatic secondary indexes.
    

  

**Creating an Azure Storage Account**

- Storage Account name must be globally unique
    
- **Network routing-**
    
    - The network routing preference specifies how network traffic is routed to the public endpoint of your storage account from clients over the internet.
        
    - By default, a new storage account uses Microsoft network routing.
        
    - The users can also choose to route network traffic through the POP closest to the storage account, which might lower networking costs.
        
    - The following diagram shows how traffic flows between the client and the storage account for each routing preference:
        

![](file:///tmp/lu38542759ixjk3.tmp/lu38542759ixjnl_tmp_a960828.png)

- **Require secure transfer for REST API operations-** Require secure transfer to ensure that incoming requests to this storage account are made only via HTTPS (default). Recommended for optimal security.
    
- **Allow enabling anonymous access on individual containers-** this setting allows a user with the appropriate permissions to enable anonymous access to a container in the storage account (default).
    
- **SFTP-** Enable the use of Secure File Transfer Protocol (SFTP) to securely transfer of data over the internet
    
- **Network connectivity:**
    
    - Network access- By default, incoming network traffic is routed to the public endpoint for your storage account. The users can specify that traffic must be routed to the public endpoint through an Azure virtual network.
        
    - Endpoint type- Azure Storage supports two types of endpoints: standard endpoints (the default) and Azure DNS zone endpoints (preview).
        
- **Encryption type-** By default, data in the storage account is encrypted by using Microsoft-managed keys. The users can rely on Microsoft-managed keys for the encryption of their data, or they can manage encryption with their own keys.
    
- **Data protection-**
    
    - **Point-in-time restore for containers-** Point-in-time restore provides protection against accidental deletion or corruption by enabling you to restore block blob data to an earlier state
        
    - **Soft delete for blobs-** Blob soft delete protects an individual blob, snapshot, or version from accidental deletes or overwrites by maintaining the deleted data in the system for a specified retention period. During the retention period, you can restore a soft-deleted object to its state at the time it was deleted.
        
    - **Soft delete for containers-** Container soft delete protects a container and its contents from accidental deletes by maintaining the deleted data in the system for a specified retention period. During the retention period, you can restore a soft-deleted container to its state at the time it was deleted.
        
    - **Soft delete for file shares-** Soft delete for file shares protects a file share and its contents from accidental deletes by maintaining the deleted data in the system for a specified retention period. During the retention period, you can restore a soft-deleted file share to its state at the time it was deleted.
        
    - **Versioning for blobs-** Blob versioning automatically saves the state of a blob in a previous version when the blob is overwritten.
        
    - **Blob change feed-** The blob change feed provides transaction logs of all changes to all blobs in your storage account, as well as to their metadata.
        
    - **Version-level immutability support-** Enable support for immutability policies that are scoped to the blob version. If this option is selected, then after you create the storage account, you can configure a default time-based retention policy for the account or for the container, which blob versions within the account or container will inherit by default.
        
- **Storage account access keys**
    
    - When the users create a storage account, Azure generates two 512-bit storage account access keys for that account.
        
    - These keys can be used to authorize access to data in your storage account via Shared Key authorization, or via SAS tokens that are signed with the shared key.
        
    - Microsoft recommends that you use Azure Key Vault to manage your access keys, and that you regularly rotate and regenerate your keys.
        
    - Using Azure Key Vault makes it easy to rotate your keys without interruption to your applications. The users can also manually rotate your keys.
        
    - Storage account access keys provide full access to the configuration of a storage account, as well as the data.
        
    - Always be careful to protect your access keys.
        
    - Access to the shared key grants a user full access to a storage account’s configuration and its data.
        
    - Access to shared keys should be carefully limited and monitored.
        
    - Use SAS tokens with limited scope of access in scenarios where Microsoft Entra ID based authorization can't be used.
        
    - Avoid hard-coding access keys or saving them anywhere in plain text that is accessible to others. Rotate your keys if you believe they might have been compromised.
        
    - A shared access signature (SAS) provides secure delegated access to resources in your storage account. With a SAS, you have granular control over how a client can access your data. For example:
        
        - What resources the client may access?
            
        - What permissions do they have to those resources?
            
        - How long is the SAS valid?
            
    - **Stored access policy**- It provides an additional level of control over service-level shared access signatures (SASs) on the server side. Establishing a stored access policy serves to group shared access signatures and to provide additional restrictions for signatures that are bound by the policy.
        
    

  

**Containers**

- Containers Public Access Level-
    

1. Private- No one can read the files stored in the container anonymously
    
2. Blob- With the URL of the file, anyone can read the file but can not see what other files are there inside the container
    
3. Container- With the URL of the file, anyone can read the file and also see what other files are there inside the container
    

- Containers do not support folder structure
    
- Blob types-
    
    - Block Blobs:
        
        - Block blobs are optimized for uploading large amounts of data efficiently.
            
        - Block blobs are composed of blocks, each of which is identified by a block ID.
            
        - A block blob can include up to 50,000 blocks. Each block in a block blob can be a different size, up to the maximum size permitted for the service version in use.
            
    - Page blobs:
        
        - They are a collection of 512-byte pages optimized for random read and write operations.
            
        - To create a page blob, the users initialize the page blob and specify the maximum size the page blob will grow.
            
        - To add or update the contents of a page blob, the users write a page or pages by specifying an offset and a range that both align to 512-byte page boundaries.
            
        - A write-to-a-page blob can overwrite just one page, some pages, or up to 4 MiB of the page blob.
            
        - Writes to page blobs happen in-place and are immediately committed to the blob.
            
        - The maximum size for a page blob is 8 TiB.
            
    - Append blob:
        
        - It is composed of blocks and is optimized for append operations.
            
        - When the users modify an append blob, blocks are added to the end of the blob only, via the Append Block operation.
            
        - Updating or deleting of existing blocks is not supported.
            
        - Unlike a block blob, an append blob does not expose its block IDs.
            
        - Each block in an append blob can be a different size, up to a maximum of 4 MiB, and an append blob can include up to 50,000 blocks.
            
        - The maximum size of an append blob is therefore slightly more than 195 GiB (4 MiB X 50,000 blocks).
            
- Snapshot-
    
    - It is a pointer to the file
        
    - The users will not be paying extra for the snapshots
        
    - When you delete the file, you need to delete the snapshots, if created
        
    - If the file is replaced by any other file with the same name, a snapshot of the previous file will still be present and the user can get the previous file back through promoting snapshot.
        

  

Access tiers

- Data stored in the cloud grows at an exponential pace.
    
- To manage costs for your expanding storage needs, it can be helpful to organize the data based on how frequently it will be accessed and how long it will be retained.
    
- Azure storage offers different access tiers so that you can store your blob data in the most cost-effective manner based on how it's being used.
    

Azure Storage access tiers include:

- **Hot tier -** An online tier optimized for storing data that is accessed or modified frequently. The hot tier has the highest storage costs, but the lowest access costs.
    
- **Cool tier -** An online tier optimized for storing data that is infrequently accessed or modified. Data in the cool tier should be stored for a minimum of 30 days. The cool tier has lower storage costs and higher access costs compared to the hot tier.
    
- **Cold tier -** An online tier optimized for storing data that is infrequently accessed or modified. Data in the cold tier should be stored for a minimum of 90 days. The cold tier has lower storage costs and higher access costs compared to the cool tier.
    
- **Archive tier -** An offline tier optimized for storing data that is rarely accessed, and that has flexible latency requirements, on the order of hours. Data in the archive tier should be stored for a minimum of 180 days.
    

![](file:///tmp/lu38542759ixjk3.tmp/lu38542759ixjnl_tmp_ee5cdbff.png)

  

Azure Storage lifecycle management

- It offers a rule-based policy that you can use to transition blob data to the appropriate access tiers or to expire data at the end of the data lifecycle.
    
- A lifecycle policy acts on a base blob, and optionally on the blob's versions or snapshots.
    
- A lifecycle management policy is composed of one or more rules that define a set of actions to take based on a condition being met. For a base blob, you can choose to check one of the following conditions:
    
    - The number of days since the blob was created.
        
    - The number of days since the blob was last modified.
        
    - The number of days since the blob was last accessed
        
- When the selected condition is true, then the management policy performs the specified action.
    

For example, if you have defined an action to move a blob from the hot tier to the cool tier if it has not been modified for 30 days, then the lifecycle management policy will move the blob 30 days after the last write operation to that blob.

- For a blob snapshot or version, the condition that is checked is the number of days since the snapshot or version was created.
    
- NOTE: A lifecycle management policy will not delete the current version of a blob until any previous versions or snapshots associated with that blob have been deleted
    

  

Azure Storage redundancy

1. Locally redundant storage-
    

![](file:///tmp/lu38542759ixjk3.tmp/lu38542759ixjnl_tmp_a67f6880.png)

- Locally redundant storage (LRS) replicates your storage account three times within a single data center in the primary region.
    
- LRS provides at least 99.999999999% (11 nines) durability of objects over a given year.
    
- LRS is the lowest-cost redundancy option and offers the least durability compared to other options.
    
- LRS protects your data against server rack and drive failures.
    
- However, if a disaster such as fire or flooding occurs within the data center, all replicas of a storage account using LRS may be lost or unrecoverable.
    

2. Zone-redundant storage (ZRS)-
    

![](file:///tmp/lu38542759ixjk3.tmp/lu38542759ixjnl_tmp_61973b0e.png)

- It replicates your storage account synchronously across three Azure availability zones in the primary region.
    
- Each availability zone is a separate physical location with independent power, cooling, and networking.
    
- ZRS offers durability for storage resources of at least 99.9999999999% (12 9's) over a given year.
    
- With ZRS, your data is still accessible for both read and write operations even if a zone becomes unavailable.
    
- If a zone becomes unavailable, Azure undertakes networking updates, such as DNS repointing. These updates may affect your application if you access data before the updates have been completed.
    

  

3. Geo-redundant storage
    

![](file:///tmp/lu38542759ixjk3.tmp/lu38542759ixjnl_tmp_f97d798c.png)

- Geo-redundant storage (GRS) copies your data synchronously three times within a single physical location in the primary region using LRS.
    
- It then copies your data asynchronously to a single physical location in a secondary region that is hundreds of miles away from the primary region.
    
- GRS offers durability for storage resources of at least 99.99999999999999% (16 9's) over a given year.
    
- A write operation is first committed to the primary location and replicated using LRS. The update is then replicated asynchronously to the secondary region. When data is written to the secondary location, it's also replicated within that location using LRS.
    

4. Geo-zone-redundant storage (GZRS)-
    

![](file:///tmp/lu38542759ixjk3.tmp/lu38542759ixjnl_tmp_866db0ed.png)

- It combines the high availability provided by redundancy across availability zones with protection from regional outages provided by geo-replication.
    
- Data in a GZRS storage account is copied across three Azure availability zones in the primary region and is also replicated to a secondary geographic region for protection from regional disasters.
    
- Microsoft recommends using GZRS for applications requiring maximum consistency, durability, and availability, excellent performance, and resilience for disaster recovery.
    
- With a GZRS storage account, you can continue to read and write data if an availability zone becomes unavailable or is unrecoverable.
    
- Your data is also durable in the case of a complete regional outage or a disaster in which the primary region isn't recoverable.
    
- GZRS is designed to provide at least 99.99999999999999% (16 9's) durability of objects over a given year.
    

NOTE: If your applications require high availability, then you can configure your storage account for read access to the secondary region. When you enable read access to the secondary region, then your data is always available to be read from the secondary, including in a situation where the primary region becomes unavailable. **Read-access geo-redundant storage (RA-GRS)** or r**ead-access geo-zone-redundant storage (RA-GZRS)** configurations permit read access to the secondary region.

![](file:///tmp/lu38542759ixjk3.tmp/lu38542759ixjnl_tmp_5be224c3.png)

Performance Tiers

1. Standard-
    

- Offers Hot, Cool, and Archive storage tier options to store data
    
- Supports all redundancy options
    
- Great for most of the use cases
    

2. Premium-
    

- Data is stored on SSDs
    
- No tier is available
    
- Supports only LRS and ZRS
    
- Great for the use cases which require high transactions and low latency
    

  

**Azure Functions**

- Azure Functions is a serverless solution that allows you to write less code, maintain less infrastructure, and save on costs.
    
- Instead of worrying about deploying and maintaining servers, the cloud infrastructure provides all the up-to-date resources needed to keep your applications running.
    
- You focus on the code that matters most to you, in the most productive language for you, and Azure Functions handles the rest.
    
- Supports infrastructure of Docker containers
    
- Multiple hosting options are available
    
- Built-in DevOps support
    
- Great for building microservices
    

  

**Hosting options**

- Functions provide a variety of hosting options for your business needs and application workload.
    
- Event-driven scaling hosting options range from fully serverless, where you only pay for execution time (Consumption plan), to always warm instances kept ready for the fastest response times (Premium plan).
    
- When you have excess App Service hosting resources, you can host your functions in an existing App Service plan. This kind of Dedicated hosting plan is also a good choice when you need predictable scaling behaviors and costs from your functions.
    
- If you want complete control over your functions' runtime environment and dependencies, you can even deploy your functions in containers that you can fully customize. Your custom containers can be hosted by Functions, deployed as part of a microservices architecture in Azure Container Apps, or even self-hosted in Kubernetes.
    

![](file:///tmp/lu38542759ixjk3.tmp/lu38542759ixjnl_tmp_a9ef1f39.png)

  

Terminologies-

- **Triggers-** They cause a function to run. A trigger defines how a function is invoked and a function must have exactly one trigger. Triggers have associated data, which is often provided as the payload of the function
    
- **Binding** to a function is a way of declaratively connecting another resource to the function; bindings may be connected as input bindings, output bindings, or both. Data from bindings is provided to the function as parameters.
    
- **Timer Trigger-** A timer trigger lets you run a function on a schedule.
    
- **Runtime stack-** Choose a runtime that supports your favorite function programming language. In-portal editing is only available for JavaScript, PowerShell, Python, TypeScript, and C# script. C# class library and Java functions must be developed locally.
    
- **Operating system-** An operating system is preselected for you based on your runtime stack selection, but you can change the setting if necessary. In-portal editing is only supported on Windows. Container publishing is only supported on Linux.
    
- **Deployment Slots-**
    
    - Azure Functions deployment slots allow your function app to run different instances called "slots".
        
    - Slots are different environments exposed via a publicly available endpoint.
        
    - One app instance is always mapped to the production slot, and you can swap instances assigned to a slot on demand. Function apps running under the Apps Service plan may have multiple slots, while under the Consumption plan only one slot is allowed