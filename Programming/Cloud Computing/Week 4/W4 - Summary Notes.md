**Class Notes – Cloud Computing on AWS 4**


**Forms of Storage on Cloud**

Any application you create for your customer will generate data that requires storage. Any form of data is essential to any organization, and selecting the right storage service for specific types of data becomes critical. So storage is one of the **core building blocks** of cloud services, also called "**Cloud Storage**".

- According to AWS - "The provider securely **stores**, **manages**, and **maintains** the storage servers, infrastructure, and network to ensure you have access to the data **when you need it at virtually unlimited scale, and with elastic capacity**. 
- Cloud storage **removes the need to buy and manage your own data storage infrastructure**, giving you agility, scalability, and durability, with any time, anywhere data access."
- Different storage options available on AWS-

- *Instance Storage* - **Ephemeral** storage, not recommended for storing the long term data.
- *EBS/Block Storage* - You will be able to mount an EBS to **only one EC2 instance** and both have to be in the **same availability zone**.
- *EFS/File system Storage* - This can be attached and mounted on **multiple ec2 instances**. **Automatically scales**, **no specified size limit**. You will be able to mount this on multiple ec2 instances , ec2 instances will have access to it in both Read/Write manner. EFS **can’t handle Concurrency**. Applications will have to handle concurrency.
- Object Storage (AWS S3) - Dedicated only to AWS. You can write Applications and use the **API** to start talking to S3, create a folder and upload a file in it. You can use **programming languages** of choice. There are SDKs available from AWS that allow us to do this. You can use the **Serverless architecture AWS Lambda** for the same task. CloudFront is a **Content Distribution Network** used to distribute the content all across **POP locations** around the world so that users will be able to draw the content from any location near to them saving significant amount of network latency. **Origin** is the place where you create an S3 instance/Bucket. Events give you a lot of flexibility. Kinesis allows you to to **read data from S3** and **transform the data** and **put the data back in S3**

  

**Block Storage - EBS**

- EBS volumes are like the **hard drives** of a laptop. These can host the operating system and an application with data. 
- These volumes are attached to an EC2 instance. An EC2 instance will have at least one volume with the operating system.
- Multiple volumes can be attached either via the **management console** or **automation scripts**.

  

**Network Storage - EFS Concepts**

- AWS EFS is an ideal solution for applications that require **highly available**, **shared storage**. 
- It's also a great choice for applications that need to **share data between multiple servers**, such as web servers and application servers. 
- EFS also offers scalability and performance, making it a **great choice for applications that require high throughput and/or high I/O performance**.

- In order for the EFS to be used from the EC2 instances and other services, it requires a mount target. In the above diagram, you can see the VPC has 3 availability zones and a couple of subnets. A file system must have a mount target in each of the availability zones. The ec2 must have port 2049 open for internal traffic
- File system grows over a period of time, so will be the cost, unlike EBS. EFS supports moving the data to infrequently accessed storage which reduces the cost.
- According to AWS - With Amazon EFS, you pay only for the storage used by your file system and there is no minimum fee or setup cost. Amazon EFS offers a range of storage classes designed for different use cases. These include:

- **Standard storage classes** – EFS Standard and EFS Standard–Infrequent Access (Standard–IA), which offer Multi-AZ resilience and the highest levels of durability and availability.
- **One Zone storage classes** – EFS One Zone and EFS One Zone–Infrequent Access (EFS One Zone–IA), which offer you the choice of additional savings by choosing to save your data in a single Availability Zone.

  

EFS is designed to provide the throughput, IOPS, and low latency needed for a broad range of workloads. You can choose from two performance modes and three throughput modes:

- The default General Purpose performance mode is the recommended mode. General Purpose is ideal for latency-sensitive use cases, like web-serving environments, content-management systems, home directories, and general file serving.
- File systems in the Max I/O performance mode can scale to higher levels of aggregate throughput and operations per second. However, these file systems have higher latencies for file system operations.
- With the default Bursting Throughput mode, throughput scales with the amount of storage in your file system and supports bursting to higher levels for up to 12 hours per day.
- With Elastic Throughput mode, Amazon EFS automatically scales throughput performance up or down to meet the needs of your workload activity.
- With Provisioned Throughput mode, you specify a level of throughput that the file system can drive independent of the file system's size or burst credit balance.

  

**Object Storage - Simple Storage Service**

S3 is an object store. In other words, this system is all about file upload, download, lifecycle and access control, among other features specifically for files. Let's look at an overview of these features that has made S3 the go-to storage service for many customers worldwide.

  

**The main difference between EBS and S3** - Both work with files, however a file in an EBS volume can be opened and the application can read only a few bytes. In S3 we download/upload files like Google Drive, Dropbox etc. It does not make sense to upload or download files from your laptop's hard disk.

- Think of Object as a file, for instance, you want to create a folder in there and put a file in there or create a file or download from in there, now the file can be either text or binary, binary could be a video file or an audio file or word document or it could be anything of that matter. S3 is object based storage rather than block based storage. 

  

- At the root you have **Buckets**, the name of the bucket needs to be **globally unique**. For every account has a soft upper limit of about 100 buckets. For example, images. If you want to upload an image of your pet cat, and you want to put it up there on S3 by the common name cats. You are not going to find it as it is a common name. It is important to keep the name globally unique. Chances are somebody else has already taken that name. So you have to be really creative in terms of creating the top level bucket names.

  

- What goes inside a bucket ?. You can either put your objects in there or files in there, or you can create folders and organize your data appropriately, the way your business wants it, or even for your own personal use. There is no limit to the number of folders that you can create within the top level. And obviously there can be a nested level as well like folders within folders.

  

- As per the documentation, the minimum file size that S3 can store is **zero bytes**. That's allowed, and the maximum is **five terabytes**. And do note that in order for you to create a five terabytes and upload the file, the thing is, imagine uploading five terabytes of storage all at one shot from on prem location onto the cloud which can be a long process and it can break somewhere in the middle. S3 comes along and says you need to break it up into smaller chunks and the chunk size cannot exceed more than 5gb. It's called a multi part upload.  You can achieve this programmatically, using the SDKs, the APIs.

  

- The versioning capabilities that S3 has in versioning, one very interesting thing to note here is that once you enable versioning, there is nothing called **Disable versioning**.You can **suspend** the versioning which behaves very much like disable.

  

- You can set an entire lifecycle in S3 with zero coding. The way you need to set that up is enable versioning if you want to, then for each of the versions, the current version as well as the older version, you can make S3 move the files from the live environment to reduced redundancy after a certain time. From reduced redundancy you can move on to infrequently accessed. From infrequently accessed, you can throw it in archival, which is called **glacier**. Once it has spent a certain amount of time  in the glacier, you can auto delete the content. That's the entire lifecycle that you can pretty much create with no coding effort

  

**S3 features**

- **Durability** - S3 is designed to provide 99.999999999% durability and 99.99% availability of objects over a given year. The documentation suggests that S3 internally stores as much as ten copies of your data to ensure that the important data stays.

  

- **Multi-region replication** - You can save the document in one region and seamlessly replicate that over to the other region. If one region goes down, you will still have the data available in the other region. 

  

- **S3 compatibility with CloudFront** - S3 and CDN(Cloudfront) are a great combination. S3 serves as the source of data and Cloudfront acts as the delivery and as well as the cache. You can have your users all around the world and have the data settings in S3. Cloudfront will pull all the data out and start caching around the words so that your users go through the minimum latency. Even more powerful is Reverse synchronization, as in which will allow you to update the cache at the point of presence and the document travels back to the origin. It is kind of a bidirectional CDN. All of these capabilities make this a very good choice. 

  

- Imagine you have created a top level bucket and there is a folder inside the bucket, you uploaded a file and let's assume these actions have been performed using the APIs. The next second you want to fetch this particular file using APIs , the file will be downloaded instantly just fine. Now that the file is there, if you upload yet another version of this particular file which actually has a different new content , if you want to fetch the same document, you might get the old file with the old content. It is essentially eventual consistency for all the writes which are nothing but the override of the existing data. Do note this is an object based store, internally it is a key value, key is the file name here in the JSON . Some of the other areas that S3 supports is encryption,either you can use KMS for the encryption or provide your own encryption mechanism

  

- **Cost** - Completely depends on the type of storage you are going to place your data on. If you are storing in real time, the cost is going to be more along with the good durability. In the lifecycle management, as the data goes through the lifecycle management, reduced redundancy costs less. Obviously the Glacier or Archival costs the least. You can expect the glacier to return your documents in a few seconds nowadays unlike the old days.

  

- **Ability to host static sites** - Imagine you are hosting a static website, you will not need an application server and S3 will ask you simple questions including the file names and the error page and will give you a DNS.

  

**Cost control** - is an essential aspect of any business. It is the process of controlling costs and expenditures to ensure that the organization can maximize its profits and minimize its losses. 

- In the context of S3, cost control involves examining all aspects of the organization’s storage and understanding how business applications access files. 
- It is crucial to identify areas where costs can be reduced, such as changing the storage class. This module will also look at organizing files in buckets and folders.
- Amazon S3 offers a range of storage classes that you can choose from based on the data access, resiliency, and cost requirements of your workloads. 
- S3 storage classes are purpose-built to provide the lowest cost storage for different access patterns. 
- S3 storage classes are ideal for virtually any use case, including those with demanding performance needs, data residency requirements, unknown or changing access patterns, or archival storage.

  

References -  

AWS Documentation

- [https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html)
- [https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html](https://docs.aws.amazon.com/efs/latest/ug/whatisefs.html)
- [https://docs.aws.amazon.com/s3/](https://docs.aws.amazon.com/s3/)

Datasheets

- [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_Elastic_Block_Store_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_Elastic_Block_Store_Datasheet.pdf)
- [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_Elastic_File_System(EFS)_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_Elastic_File_System\(EFS\)_Datasheet.pdf)
- [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_S3_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_S3_Datasheet.pdf)