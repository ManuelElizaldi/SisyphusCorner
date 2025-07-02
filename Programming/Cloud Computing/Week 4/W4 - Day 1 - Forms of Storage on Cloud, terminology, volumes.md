[[Storage]] [[Cloud Computing]]
# Forms of storage on cloud

Any application will generate data, this data needs to be stored somewhere.

## Instance storage
Storage you will find inside EC2. You wont have anything attached to the instance, no additional services. 

This storage is ephemeral. Meaning, if this instance is terminated, any data stored in here will be lost. 

Since the objective is to build a resilient architecture, this wont be a good approach. EC2 storage should not be used for long term data 

1:1 relationship to the instance

## Elastic Block Storage
Elastic 

You can keep up extending the storage

1 EBS can only mount to 1 EC2. They both need to be in the same AZ. 

Think about it as a SSD

You pay for a fixed amount of storage but this can be increased
## Elastic File System

Can be mounted to multiple EC2 instances.

You are charged for what you use, if you use 1 MB you are charged for this amount
##### Who takes care of concurrency?
*Concurrency* -> when a system performs multiple processes at the same time
EFS is not built to handle concurrency, you need to design your code in order to handle it. 

Read and write permissions

## S3 - Simple Storage System
Object based 

This works as a Dropbox or google cloud storage, but only dedicated for AWS.

You can use APIs to talk to S3. 

Programming language agnostic - you can use any language you want

Origin -> where you originally created your S3 bucket

You can build applications within the S3, for example, if you need to work with a particular file, you can set up a trigger that finds that file and then performs what the application needs. Similar to what I do with CHS in the vm5 

You can talk to the S3 with the CLI or through an API

Most of the managed services in AWS use S3 within them. 

Extremely flexible and powerful 

You can replicate the data from one region into another


#### Practice quiz question: Where would you store a temporary, non critical cached copy of a file?

Instance store - this is ephemeral storage. 

# Introduction to EBS - Elastic Block Storage 
You need one place to store the data and another one to store the application -> ESB is the best choice for this

Volume -> a disk, there are several types:
1) General purpose
2) Provisioned IOPS
3) Throughput optimized 
4) Cold

You attach the volume to an instance, if this is the first you attach it will be determined as 'Root volume'
- You can't remove the volume, but you can replace it. The OS lives in the volume. 
- You can attach multiple volumes 

Storing the data for extended period of time is important 

## Block 
EC2 always uses EBS, a block is an important part of this system

Store and retrieve data easily. Organization is key 

*block* -> small part of the disk that can hold information. Setting up blocks inside the disk is called *formatting*

Blocks have fixed sizes, they are defined by the OS.

A series of blocks make up a file

Block size is the minimum data that the OS will read from the disk.

*Defragmenting* -> computer process that organizes and consolidates fragmented data on a storage device. Reduces data seek operations 

#### Practice quiz question: Which of the following is not a type of amazon EBS volume
Tape drives

## Terminology of storage
Formatting -> create the block structure that allows the machine to store and retrieve data 

File system -> big filing cabinet, keeps track of where everything is located 

Attaching & detaching disk or volume -> connecting and disconnecting a solid state drive to the instance

Mounting & unmounting -> directory that is assigned to an attached disk (/ is root)

I/O Input/Output -> measured using IOPS, transferring data between the instance memory and the volume. Reading data from the disk and writing data onto it.  
- IO operations per second, measures performance of the volume 

Freezing and unfreezing IO -> temporarily stopping, this is done to get a snapshot of a system/disk. Prevent any changes
- Thawing -> restore operations

Crash consistent vs application consistent -> only the disk vs disk + memory
- consistent state -> prevents data loss if there's an unexpected shutdown.
- system can restart without corruption or data loss. This does not guarantee integrity of applications, especially information that was in memory 

# Feature Analysis EBS

Ability to provider block devices -> direct and efficient storage 

Blocks can be formatted per the user's requirements 

AWS recommends having the storage and instance being on the same AZ

Data can be retrieved in real time 

EBS persistent state 
- You can terminate the EC2 and the EBS will remain running 

## EBS Volume types 

There are several types of volumes that can be used, SSD, throughput optimized etc. Even a magnetic storage is available 

The general approach is to understand the app and the build based on that. 

The instructor suggests a 2P approach to deciding what volume to use:
- Performance and Price:
	- Performance -> Throughput -> bits/bytes per sec | IOPS = number of RW per second 

#### Practice quiz question: What is the primary purpose of EBS in AWS? 
Storing block-level data persistently 

## EBS Snapshot
Copy of data at a given point in time. If something fails you can use this to recover it. 

Sometimes business requirements means that you will be moving data from AZ1 to AZ2. Snapshots allow this

Gibi -> 1024 mb 
Giga -> 1000 mb

it takes snapshots gradually, at the beginning it takes a snap of 10 gigs, if 4 gigs are added, it will take a snap of that, so the total snaps are snap A + snap B
![[Pasted image 20250623200549.png]]


# Life cycle, encryption and best practices 

### Data lifecycle
Stages that data goes through from its creation to its eventual deletion. 

Creation/collection -> Storage -> Processing -> Sharing -> Archive -> deletion 
## Data lifecycle manager
Amazon Data Life cycle Manager -> automated EBS snapshots 

Automation helps protect data, meet compliance and reduce storage cost 

Lifecycle policy -> frequency, retention, cross region copy, cross account sharing 

Backup solution 

## Encryption
### EBS
Encryption of boot and data volumes 

secures data at rest, in transit, snapshots and volumes 

AWS KMS-generated data key 

EBS volume can be created from an encrypted snapshot 

### Snapshots 
encrypted volumes yield encrypted snapshots -> if you want to read them you will need the key as well. 

Data is secure at transit and at rest 

owners can create volumes from their snapshots 

Unencrypted snapshots can be shared -> not as secure 

#### Practice quiz question Which AWS resources can AWS key management service (KMS) be utilized to encrypt?
EBS volumes 

## EBS Best Practices

Understand requirements, then set up the EBS volumes

Right size volumes -> cost impact, you don't want to pay for over utilization

Use encryption 

Properly tagging 

Snapshot regularly 

Monitor

#### Practice quiz question From an operations perspective tagging volumes is recommended 
True 









