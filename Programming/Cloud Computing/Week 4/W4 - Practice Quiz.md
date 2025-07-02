##### Assume you have a large ERP application that has a relational database. Your department is responsible for the management of the database. Due to certain security and privacy reasons you have decided to manage the database yourself. However, you are unsure regarding the data growth. Which kind of storage service will you prefer to store your live database DB files?
- Elastic Block Storage 
	- With Elastic Volumes, you can dynamically modify the size, performance, and volume type of your Amazon EBS volumes without detaching them.
	- After you increase the size of an EBS volume, you must use file system–specific commands to extend the file system to the larger size. You can resize the file system as soon as the volume enters the optimizing state.

##### Which of the following storage options would you use to store a temporary, non critical cached copy of a file?
- Instance Store
- To quote AWS - An _instance store_ provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for temporary storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

##### As an educational organization, which of the following storage options would you use to store records of past students that have to be retrieved only once a year for alumni meets?
- S3 Standard Infrequent Access
- S3 standard infrequent access storage will provide the most cost-effective storage for data which is not retrieved frequently while providing the same resiliency as standard storage.


##### Practice quiz question A banking and financial services company has created a web portal. The deployment topology consists of EC2 instances which is running the web application. The company has decided to use ________ for installing the application. One of the use case allows the customers to upload application forms which will be stored in __ . The application may produce non critical intermediate files which can be easily recreated which needs to be saved in __ . The application also needs global configuration files and intends to produce logs and for this scenario the company intends to use ________ such that these files can be accessed by another fleet of management instances.
EBS, S3, InstanceStore, EFS
- - EBS volumes will survive in case the servers need to be stopped in addition to providing multiple options from a performance perspective.
- S3 is designed for object store and is a great fit to store documents uploaded by the customers.
- Transient files should be stored in instance store, especially when they are non critical.
- EFS is a perfect fit for usecases when the file system needs to be attached to multiple instances which will allow one (or few) copies of the configuration file(s). Furthermore, the EFS can have different directories which can have the server logs and a different fleet of instances can read from this location for log analysis.

##### Which of the following options is the most optimum to check if a new object/file is uploaded in an S3 bucket?
Set up an event notification for PUT event
- Event notifications is the best option to detect any changes to the bucket contents
- They can be captured by SNS, SQS as well as lambda

##### Web apps from one domain can interact with content served by S3 (another domain) using _______
CORS
- Cross-origin resource sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. With CORS support, you can build rich client-side web applications with S3 and selectively allow cross-origin access to your S3 resources.