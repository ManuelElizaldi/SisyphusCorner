[[Storage]] [[Cloud Computing]] [[Data Lake]]

EBS, EFS, S3 -> main ones
# Data Center vs AWS
## Enterprise Data Center
persistence storage 
VM (OS + File system) -> App uses the file system. 
- There are different file systems:
	- Windows -> NTFS
	- Linux -> XFS, EXT4

*Direct attachment storage* -> The storage that's inside your PC/laptop. This has physical limitations. This can't be scaled up.

Usually in data centers you have *External Storage* as well:
### Set up of an app inside a data center/on prem with External Storage
#### Block Storage
Storage Area Network SAN EMC -> fiber channel -> HBA card -> Physical Server -> VMware -> VM (OS + file system)/ data -> App

#### Network Attached Storage
Network Attached Storage (Net App) -> Ethernet -> NIC card -> Physical Server -> VMware -> VM (OS + file system)/ data2 -> App 

Shared file systems:
Windows -> SMB Share
Linux -> NFS

## Cloud Storage
###### note try to remember the fundamental use case instead of remembering the names. 

### Elastic Block Storage
Elastic because you can use multiple features for the volumes. Hardware like, you plug and unplug this type of storage.

#### AWS build of app 
EC2 - Default disk (root disk) = OS 

EBS = separated compute and storage = attach/detach -> it includes the file system. 

EBS -> Ethernet -> NIC card -> EC2 -> VM (OS + file system)/ data <- App
- Shared responsibility model
	- EBS, Ethernet, NIC card <- responsibility of AWS
	- EC2 -> VM (OS + file system)/ data <- App <- responsibility of customer 
##### Never attach you data to the default disk. This is ephemeral storage. Inside EBS you'll have more security and features. 

#### Setting up EBS:
You are able to add EBS storage inside the *launch instance window*
##### Metric for storage performance:
IOPS = reads/sec + writes/sec

##### When deciding which Volume Type to use:
*You can't go wrong with general purpose SSD* If you have no idea of your IOPS requirements, go with general. GP3 
###### Data ETL requires high IOPs, for that, you can go to an upgraded version (IO 1-3, etc.) of General purpose SSD. This is very expensive
##### Types of storage:
SSD - expensive, but high performance
SAS - 15000 rpms <- middle ground
SATA - 7500 rpms <- Cheap, low performance

##### Metrics:
To decide which *Volume Type* to use, let metrics guide you
If your IOPs is high you can look at -> CPU, Mem, NIC, Disk IO

EBS needs to be in the same AZ as the EC@ instance it will be attached to. 

#### Plugging/mounting the EBS/Hard drive
Whenever you attach a new hard drive, it will detect it, but not its type. For this, you need to *format it*

If you are mounting a hard drive with data in it, you don't want to format it, this will delete all the data in there. *So you have to be very careful with it*.

##### CLI commands used by instructor:
[Guide](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-using-volumes.html)

`sudo su -` <- giving root privilege 
`df -h` -> displaying mounted file systems
`lsblk` -> mounted storage
`mkfs -t xfs /dev/xvdb` <- formatting disk. With this, you have to be *extremelly careful* 

then you create a directory and mount it:
`mkdir /data`
`mount /dev/xvdb /data` 

#### Snapshots
Ability to create backups. From a snapshot, you can create another EBS

AFR -> Annual failure rate

#### Lifecycle Manager - To automate the back up process

### EFS - Elastic File System
Scalable, elastic and cloud-native EFS system. 
You pay for what you use. 

Here you don't need to specify the size. It allocates space as you go


### Amazon S3 - Buckets
Millions of operations - its a beast. It can handle any amount of data and traffic. 

Object = file

Replicates an object in 3 AZ. Chance of loosing data is very low. 

Number 1 use case -> *Data Lake*

LB -> Web -> App -> DB (OLTP)

JDBC -> Tableau (or any BI tool) -> BI Analyst

#note BI analysts wont be able to access production databases. But they need the data, so how do we solve it?

Batch updates -> S3 -> ETL (AVARO/Parquest) -> data warehouse -> 

#note Map reduce -> data processing service


*Bucket* -> General container where you place your data. The name has to be globally unique. 
- buckets can be created through IaC

#### Setting up a bucket

Encryption is forced. 

You can customize a notification system. You decide what you want to get notified on.

Object versioning 
##### Static Websites
You can host a static website through S3

#### Lifecycle configuration
You create a replication rule, you can determine the source, you decide what you want to replicate: some objects, everything or some prefixes? What's your destination going to be? 


Life cycle policies -> think about 
#### S3 tiers 
S3 storage classes. There's general purpose, high performance(used in pharmaceuticals), there's also smart/intelligent tiering that decides what to use based on your use patterns.

Infrequent access is also available to store your archives/backups. 
- *Deep archive - Glacier*
	- This is will grant a cost reduction

![[Pasted image 20250629105327 1.png]]

This is cheaper because AWS does not create copies of your objects inside different AZs. Also, data is stores in non high performance systems. There's low IO on these storage systems. 

AWS makes money from this because data retrieval is way slower. 

##### The professor recommended spending more time in S3 compared to the other services. Learn data lakes. Machine learning requires data lakes and that's where the $ is

## Cost Comparison 











---- 
###### research file systems, HBA Card, block storage, Shared file system, EBS, Research the above types of storage, IOPS, JDBC