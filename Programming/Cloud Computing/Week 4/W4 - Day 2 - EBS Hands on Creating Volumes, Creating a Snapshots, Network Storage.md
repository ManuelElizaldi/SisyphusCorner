[[Storage]] [[Volumes]]

In this TIO, we created an EC2 instance, then created a volume and attached this storage to the instance. After that we created a file system in the blocks inside the volume we attached. 

## ChatGPT breakdown here


We also expanded from 10 Gig to 15 Gig the existing volume. 

Using the command `lsblk` we can get a view of all the disk devices and their mount points 
![[Pasted image 20250624183624.png]]

We also created a snapshot based on the first volume we created, and then we created a volume from this snapshot 

# Network Storage - EFS Concepts

EFS -> Elastic File System

it requires a mount target in each AZ where it wants to be available. 
![[Pasted image 20250624185337.png]]

Mount Target will have an IP address and it also requires the port 2049 to be open, this port is open through a security group. 

EFS grows overtime, the cost will grow based on the size. AWS automatically provisions more storage for you. 

EFS has a feature where it moves not frequently used files to a specified storage for this to reduce cost. This is done through lifecycle rules that you set up. 

EFS has a couple of performance models. If you have many EC2 instances or you are working with big data, you can set it up as Performance. But you can't modify it once its running, if you need to switch model, you will need to perform a migration from EFS 1 to EFS 2 (new performance model)

*Throughput* -> EFS offers multiple options for IOPS. You can set an amount of IOPS (from what I understand) and then if you don't use some of them you will get credit. Once you pass that limit, AWS will use the credit you have.
- AWS will make sure you always have enough IOPS

##### ask about this:
EFS is not cross region 

#### Practice quiz question: Which of the following storage solutions would be a better fit for a distributed application spanning a large number of EC2 instances and performing analytics jobs on a large dataset.
EFS because Amazon Elastic File System (EFS) is a serverless file system that provides shared storage for use with AWS Cloud compute instances. EFS is highly available within the AWS Region and can scale up quickly and automatically to meet spikes in workload demand. It also allows instances in different availability zones, VPCs, and on-premise systems to connect to it. It provides high levels of durability and availability for your workloads and applications, including big data and analytics, media processing workflows, content management, web serving and others.


##### How does EBS and EFS compare?
Can a EBS be connected to multiple EC2s?


# EFS Hands on 
When creating the port 2049 security group you can use the type: Custom TCP. The source is custom and you have to set up the value for the VPC CIDR Block according to what you currently have set up.

Make sure to add the new security group for port 2049 to the instances that will be using the EFS 

You choose the throughput mode of the EFS 

When creating the Network Access of your EFS, choose all AZ to ensure higher availability 

The EFS has a monitoring area. 

To mount the EFS to an instance, the video did it through DNS and using NFS tools. The web console gave us the commands in other to do this. 
Things the instructor did:
1) created a dir /efs
2) ran command provided by web console

`sudo su` <- command to elevate privileges in linux 

`mount` and `unmount` are used to mount the EFS into the instance, same as the EBS

##### Look up what is VPC CIDR block and what about its IP value

#### Practice quiz question What are the different types of "File System" in AWS EFS?
Regional and One zone


EFS has the following types -

- **Regional** – Regional file systems (recommended) store data redundantly across multiple geographically separated Availability Zones within the same AWS Region. Storing data across multiple Availability Zones provides continuous availability to the data, even when one or more Availability Zones in an AWS Region are unavailable.
    
- **One Zone** – One Zone file systems store data within a single Availability Zone. Storing data in a single Availability Zone provides continuous availability to the data. In the unlikely case of the loss or damage to all or part of the Availability Zone, however, data that is stored in these types of file systems might be lost.
    

The following are the different types of storage classes -

- **EFS Standard** – The EFS Standard storage class uses solid state drive (SSD) storage to deliver the lowest levels of latency for frequently accessed files. New file system data is first written to the EFS Standard storage class and then can be tiered to the EFS Infrequent Access and EFS Archive storage classes by using lifecycle management.
    
- **EFS Infrequent Access (IA)** – A cost-optimized storage class for data that is accessed only a few times each quarter.
    
- **EFS Archive** – A cost-optimized storage class for data that is accessed a few times each year or less.

