[[Storage]]
# Azure Storage
Object storage -> store massive volumes of data 

Max capacity -> 5PiB per account. 
- You can create multiple accounts, every storage account gives you 5 PiB
- You pay for the data you are storing 

Multiple data replication options 

Different tiers to store data based on requirements 

Rest API compliant -> every file has a URL
- But there are multiple SDKs to work with 

## Storage Account 
Storage account -> storage service -> blobs/files

Storage account can be thought of a building, within the building you have rooms (storage services), inside those rooms you keep items (blobs/files)

You determine who can enter which part of the building by declaring RBAC (role-based access control) or you can also deploy access keys but this is not recommended since they have to much power. Or also deploy a SAS (shared access signature) for temporary limited access. 

## Azure Storage Services
*Blob Storage* -> This is the most used. Unstructured data. This is similar to google drive or S3 in AWS. 
- You access files using URLs, again similar to google drive 
- Supports streaming for videos and audio files 
- **Does not support folder structure** 

*File Storage* -> Azure hosted file share. 
- Supports SMB and NFS protocols 
- Caching available on windows servers using file sync 
	- **file sync*** allows to connect to your on prem systems  

*Queue Storage* -> Message broker, store huge number of messages in a queue up to size of storage account. 
- Allows asynchronous architecture 
- Bus functionality is available in Azure service bus
*same as SQS?* -> AWS SQS has more features like the dead letter queue. But they both offer asynchronous architecture

*Azure Table Storage* -> No SQL database, structured and non relational data. Key-value type of NoSQL database 
- *CosmosDB -> any type of no sql database. Also available as Table API*

# Creating a Storage Account
Account names are unique - be careful when you choose an account 
- It has to be unique because it is shown in the url of the files

**Microsoft Global Network Routing** -> If a user in India wants to access a storage account in the US, his request will be sent to the nearest data center and from there it will flow inside the Microsoft Global Network and wont go through the internet 
![[Pasted image 20251008211155.png]]

Inside the storage account, you can have 4 services:
- containers = blob storage
- file share
- tables
- queues

and also the SDKs

### Public Access Level
*Private* -> no one can read the files anonymously

*Blob* -> if you have the url of the file, the person can read the file anonymously, but the user can not see what other files are present

*Container* -> if you have the url you can read the file + you can see what files are present in the container 

### Advanced Options - Blob File Upload
*Upload to Folder* -> although there is no folder structure, there is an option that can help you organize your files. 

*Blob Types*: 
Once you upload a file, the blob type can't be changed
- *Block blobs*: blob = files. binary large object = blob. File is divided into multiple blocks and each block has the same size. This makes the handling of files faster. The max size is 50,000 blocks. 
	- Each block has an ID. If you want to modify a small part of the file, you can get the block id and modify that instead of modifying the whole thing. 
	- Download happens in parallel via blocks

- *Append Block* -> Similar to block blobs with max size of 4MB block size but these are optimized for append operations. New blocks are appended to the end of the file. 
	- You can't update or delete blocks 

- *Page blobs* -> Store disks inside storage and then connect to VM. Optimized for read and write operations. 

### Snapshots of Files
Back ups of files. The size of snapshots are also considered into the total data you are paying for. 

For example, if you have a file that has a size of 1kb but it's snapshot is 1mb, the total amount of data you are paying for is 1kb + 1mb 
- You are charged for the total unique storage 

**Snapshots are pointers to the a file!**

*promote snapshot* -> replaces the actual file with the snapshot 

