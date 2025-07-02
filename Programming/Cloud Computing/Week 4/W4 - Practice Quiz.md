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

