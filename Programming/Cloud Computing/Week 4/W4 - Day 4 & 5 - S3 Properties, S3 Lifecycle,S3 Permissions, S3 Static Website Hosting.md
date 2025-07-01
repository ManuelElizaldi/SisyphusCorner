[[Storage]] [[Web Dev]] [[Filesystem]] [[S3FS - FUSE]] [[Open Source]] [[Data Lake]] [[S3]]
# S3 properties
You can find all of these settings inside the management console for S3

*versioning* -> once you enable, you can't disable but you can suspend it 

Server access logging -> log requests for access to your bucket

CloudTrail data events -> important from a user perspective. There are certain API calls that will be tracked and logged 

server access logging + cloud trail -> great tool for investigating what happened

*Event Notifications* -> This acts like a cron job. Event Notifications allows you to trigger jobs when something happens. 
- Destination -> what will catch the event 

*Transfer Acceleration* -> reduces latency. - enable or disable, its amazon's responsibility for this to happen but it requires no set up. Of course it costs more.  

*Requester pays* -> The customer (your client) pays to have access 

#### Practice quiz question -> What are the typical S3 bucket properties?
Tags, Version control, life cycle management 

# S3 Lifecycle, replication, metrics
Content lifecycle management is important for content management because it allows organizations to effectively manage their digital content, making sure the most up to date version is live and that it complies with regulations. 

This also ensures that content is only stored for the amount of time that is necessary. 

Replicating content across regions lowers latency for customers.

Lifecycle is determined by *lifecycle rules*. You determine how content progresses. You decide if this applies to the whole bucket or just a prefix. 

There's a couple of settings to set up the lifecycle:
![[Pasted image 20250626181749.png]]

It works in steps, it transitions according to the days you set:
![[Pasted image 20250626181911.png]]


*Expiration* -> S3 will delete objects after a certain period of days passes. 
- Expiration needs to be larger than the max transition days 

## Replication
Replicate data from one source (bucket) to another destination

This is set up based on rules. 

rule scope -> whole bucket or only some prefixes or based in another filter. 

Replication requires bucket versioning. 

There are several options of replication:
![[Pasted image 20250626182939.png]]

#### Practice quiz question: What is the minimum number of days needed to change a document's storage class via a lifecycle configuration?
30 days. 


# S3 Versioning, Replication, Delete markers


If your replication does not happen, you have 2 options 1) Open a ticket with AWS, 2) Create a program (CLI, python, etc.) that executes the replications. 

In the Bucket management console, you can enable *list versions* to view the different versions of a file.
- This creates additional versions of the file -> more storage is used. You wont only store 1 version, but version 1, 2, 3... 
- Remember that versioning is important for compliance reasons, back up, etc. 

##### Deleting a file -> is a soft delete, it adds a delete marker. 
- If versioning is enabled on a bucket, when you delete an object/file, it will create a soft delete called *delete marker*. To restore the file, you have to delete the marker which makes the previous version the current version again. 
- Deleting a file in a replica, wont delete the file in the main bucket  

![[Pasted image 20250628164724.png]]

##### It is your responsibility to keep the main and replica buckets in syncs. 
The replica bucket is not in sync with the main bucket



# S3 Permissions
Giving access to others.
- public access or access for other AWS users. 

By default, buckets are not public.

## Bucket Policy Feature
JSONSs are used to set the custom permissions 

Here's an example where access is granted to a specific user. In the #actions section you can see what this user (*sid*) will be allowed to do
![[Pasted image 20250628165900.png]]

By default when you create a bucket you become the owner. But with Object Ownership feature, you can assign people how ownership is assigned within your bucket. 
- You can have *object writer ownership* -> who ever created/uploaded the object is the owner
- or the owner of the bucket is the owner of everything that is within the bucket. 

## Access Control List 
This feature is used to grant basic read and write permissions to other AWS users 
- This feature is the same as the Bucket Policy. There is overlap, you can choose whatever works for you. 

## Static Website Hosting - Cross Origin Resource Sharing 

Client web app applications that are loaded in one domain to interact with resources in a different domain

Other websites can access your S3 files 

You create a XML or JSON to determine what websites are allowed to perform calls to your static website and vice versa 


## Access Points 
When setting up the Bucket Policy, your JSON can become huge and unmanageable, this is where *Access Points* come in. 

They simplify access management. You create application specific access points permitting access to a shared data sets with policies tailored to the specific application. 

Each entry point has its own policy. 


#### Practice quiz question: What are the best practices for implementing access control of documents in S3 to help improve the security posture of an organization?
Disable access control lists
- S3 Object Ownership is an Amazon S3 bucket-level setting that you can use to control ownership of objects uploaded to your bucket and to disable or enable ACLs. By default, Object Ownership is set to the Bucket owner enforced setting and all ACLs are disabled. When ACLs are disabled, the bucket owner owns all the objects in the bucket and manages access to data exclusively using access management policies.

- A majority of modern use cases in Amazon S3 no longer require the use of [access control lists (ACLs)](https://docs.aws.amazon.com/AmazonS3/latest/userguide/acl-overview.html). **We recommend that you disable ACLs**, except in unusual circumstances where you must control access for each object individually. To disable ACLs and take ownership of every object in your bucket, apply the bucket owner enforced setting for S3 Object Ownership.


# S3 Security Best Practices:
- Ensure that your Amazon S3 buckets use the correct policies and are not publicly accessible
- Identify potential threats to your Amazon S3 buckets
- Implement least privilege access
- Use IAM roles for applications and AWS services that require S3 access
- Consider encryption of data at rest
- Enforce encryption of data in transit
- Consider using S3 Object Lock

#### Practice quiz question: If you delete an object (in a bucket with versioning enabled), instead of removing the object permanently, S3 inserts a delete marker, which becomes the current object version. You can then restore the previous version by deleting the delete marker.
True
- A _delete marker_ in Amazon S3 is a placeholder (or marker) for a versioned object that was specified in a simple `DELETE` request. A simple `DELETE` request is a request that doesn't specify a version ID. Because the object is in a versioning-enabled bucket, the object is not deleted. But the delete marker makes Amazon S3 behave as if the object is deleted. You can use an Amazon S3 API `DELETE` call on a delete marker.

# S3 Storage Lens overview, Historical UI updates

Batch operations -> jobs on a list of objects. Bulk operations.  
- This can also be ran as IaC

## Storage lens
Gives you an idea across all buckets, across all regions of how your buckets are being used. If you have a AWS organization, this gives you a whole view of everything.
- You will need the necessary permissions:
- ![[Pasted image 20250628184500.png]]

This is an example:
![[Pasted image 20250628184512.png]]


Gives you a good idea of overall cost for your buckets.

## Clean up resources

click on the bucket name -> delete -> maybe will give you an error because your bucket is not empty.
- there is an empty button that clears the contents of a bucket
![[Pasted image 20250628184643.png]]


## History
It has evolved as a service, but the fundamental knowledge is the same. 

You have bucket name, events, delete market, different version of objects, prefixes, archive - glacier.

UI will change, but the core feature is the same 

#### Practice quiz question A banking and financial services company has created a web portal. The deployment topology consists of EC2 instances which is running the web application. The company has decided to use ________ for installing the application. One of the use case allows the customers to upload application forms which will be stored in ______. The application may produce non critical intermediate files which can be easily recreated which needs to be saved in ______. The application also needs global configuration files and intends to produce logs and for this scenario the company intends to use ________ such that these files can be accessed by another fleet of management instances.
EBS, S3, InstanceStore, EFS
- - EBS volumes will survive in case the servers need to be stopped in addition to providing multiple options from a performance perspective.
- S3 is designed for object store and is a great fit to store documents uploaded by the customers.
- Transient files should be stored in instance store, especially when they are non critical.
- EFS is a perfect fit for usecases when the file system needs to be attached to multiple instances which will allow one (or few) copies of the configuration file(s). Furthermore, the EFS can have different directories which can have the server logs and a different fleet of instances can read from this location for log analysis.

# S3 Transition Options
There are several storage options in S3. If you want fast read operations for your application (because that's what it demands), you can get a high performance S3 bucket. 

Same goes for infrequent accessed items. You can set rules to transfer items to a less optimized hard drive when they haven't been accessed in a set period of time. 

This will save you costs. 

The archive S3 bucket is called glacier. 

AWS makes money by transferring items that are less frequently accessed to hard drives that are slower

# Mounting S3 on Local Filesystems 
You can mount a S3 bucket in a local filesystem path in order to upload and extract objects (files) from and to the S3 bucket. That way you don't have to worry about specific code infrastructure, communication protocols, security mechanisms or specific API calls to communicate with S3. 

This is similar to when you mount an SSD to a linux system. 

## Use case:
If you have a photo upload application, you can point it to a specific path to use a folder as a working directory. You can then map the S3 bucket to this folder and the app can communicate directly to the bucket without needing to program infrastructure

### S3FS - FUSE
Free open source software/plug in utility which supports linux and mac os. This plug in takes care of caching files locally to improve performance. 

*caching* -> Storing data temporarily so it can be accessed faster later. 
- #note it can be stored in RAM and dedicated cache sections of the CPU 
# Data Lake Powered by S3-3 
Amazon Simple Storage (S3), largest and most performant object storage service for structured and unstructured data. 

This can be used to run big data applications, run analytics, AI, ML, high performance computing (HPC) and media data processing applications. 

Leverage the knowledge within your unstructured data

AWS Glue helps movement of data between data lake and your application



--- 
#### Sources
[AWS data lakes](https://aws.amazon.com/big-data/datalakes-and-analytics/datalakes/)

