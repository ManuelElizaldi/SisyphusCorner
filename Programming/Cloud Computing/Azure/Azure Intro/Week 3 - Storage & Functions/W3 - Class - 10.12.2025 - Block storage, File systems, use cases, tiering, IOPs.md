[[Storage]] [[Functions]]

# Azure Storage Services
Physical Server -> VMWare (hypervisor) -> VM file system -> App/DB

*Storage Area Network (SAN)* -> this is where the file systems live. EMC/Dell -> connected via fiber channel -> HBA Card on physical server  

### File Systems
You have to format the hard drive into one of these, after you can mount

- NTFS -> File system inside Windows -> Block storage 
- XFS, EXT4 -> File systems for Linux 

## Use Cases
1) Block storage -> usually 1 per VM but it can be shared 

2) shared file system -> NFS, SMB
- SMB -> The one I am using for my network SSD that can talk to multiple OS systems 
3) Data lake

### Network Attached Storage 
NAS -> NetApp -> Ethernet -> NIC card 

## Storage Tiering 
*SSD* (highest performance, more expensive)
- production because it has higher requirements
*SAS*

*SATA* (low performance, very cheap)
- development environment usually uses this

## IOPs - Performance Metric
Input & output operations per second 

*Example*
- Transaction 1 -> amazon.com -> browsing through catalog -> read operation 
- Transaction 2 -> amazon.com -> checkout process -> write 

For both of these you need to access data 

CPU and memory have evolved faster than disk technology, so if the disk can't keep up with demand user experience will suffer. 

How do you know this is happening? Metrics 
- Kb/reads, kb/writes , % io wait 

#### It is very important to understand your IOPs requirements before deciding which hard drive option to choose
## Creating a managed disk 
*Encryption*
Platform-managed -> the cloud provider provides the key 

*Networking* 
How are you going to access this disk:
- public
- private
- Through a VM

**You have to create a VM first before you can interact with the disk. Cloud providers decoupled the compute and storage** 
- If a VM starts failing, you can throw it out and launch a new one 

*OS Disk* -> This is only used to launch the OS, store binaries, dependencies, etc. 

## Creating a File Share
*Redundancy* -> LRS (locally redundant), ZRS (zone redundant)

*mount point* 

*networking* -> public endpoint or private

## Azure Data Lake
amazon.com -> API Gateway -> LB -> web -> app -> DB (OLTP | Producer) -> Batch update -> raw data -> ETL -> data warehouse <- BI Tool 

**You can have multiple consumers of raw data**:
data warehouse -> tableau/power BI <- *Consumer 1*
RAG Model -> Tune ML Model -> ML Inference -> ML Practitioner <- *Consumer 2*

- Consumer = people that are using the data

- No one will allow you to touch the DB, so you wont be able to connect to a BI tool 

Data Governance -> Who is the producer and consumer

