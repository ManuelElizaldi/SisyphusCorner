[[Storage]]
# Object Storage - S3
S3 -> system that is all about file upload, download, lifecycle and access control among other features. 

Think of object as a file 

S3 is object rather than block. It does not have folders, it has a bucket.

Buckets are globally unique. You have to be creative on determining the name of this buckets. 

You can create folders inside the buckets, there is no limit of folders. Also they can be nested - folder inside a folder

The min of a bucket is 0 bytes, the max is 5 terabytes. 

S3 receives files in chunks, to ensure that it does not break if you are uploading files. The max size of a chunk is 5 gigabytes. 

Multi part upload -> uploading a huge file in chunks 

S3 has *versioning*. -> Similar to GitHub -> you can see how a file has evolved through a period of time 
- The fundamental difference between bucket/file versioning and git -> S3 keeps multiple versions of the file. Git track changes to the file.  

## Use case - Content Lifecycle
When you are in the content management industry -> you need to receive/create and then destroy the content. The content has a lifecycle which can be set up in S3.

You can set the the frequency of use of the file, and it is categorized as such. For example, one you don't want to use it you can archive it inside:
- Archival = Glacier service

## Availability
S3 is very durable, you can't loose a document using S3. It has received outages, but you won't lose files.

You still need to build/design your architecture to avoid outages

S3 is a *multi region replication*. You can save a file in 1 region and you can easily duplicate it in another region. 
- but you have to bake in the availability to go to another region if 1 is down. 

## S3 and CDN (CloudFront)
They are usually paired together

S3 -> source of data

CloudWatch -> delivery, caching 

Bidirectional CDN. 

You can use this set up to distribute your data around the world

## Eventual Consistency 
Using APIs, you created a bucket and a folder inside.  You get eventual consistency for the overwrites. Meaning, let's say you upload a file named 'test.py' with some python code. After some time you add code to this file and you want to check whats inside, you *might* see the older version. That's because there's *eventual consistency*. 

You get strong read-after-write consistency for the new objects, but you get eventual consistency for the files that are already there. 

There's no right answer to how much it takes to get the new version of the file. It is proportional to the amount of data you are uploading 

## Key - Value
Internally it works as a key - value pair. Buckets are viewed as Json. You get the bucket name and its pair is one of the many files inside 

## Cost
The cost depends on the type of storage you are using. If you want real time storage, cost will go up. 

## Hosting Static sites
S3 has the ability to host a static website. If you are only deploying a static website, you save the money of a server and just host it on S3.

One use case is, if you have product manuals you can upload them here. 


### What is the difference between EBS and S3? Both work with files
A file in a EBS volume can be opened and the application can read only a few bytes. In S3 we download/upload files like Google Drive, Dropbox, etc. it does not make sense to upload or download files from your laptop's disk. 

#### Practice quiz question AWS S3 bucket name needed to be unique in: 
Globally 

# S3 Overview and Buckets 
From the console you can create a Bucket
##### Scenario -> Customer interface with us giving contracts, documents, in voices, etc. We have to keep them in the books for archive. 

We decide to store all this documents inside a bucket.

Should we build a bucket for each customer or a folder per customer? We need to consider that buckets need to be unique in the entire AWS space, across all regions and across all customers. 

- for this, bucket names can be hard to come by. 


There is a hard upper limit for buckets, 1000 per user

prefix = folder 

Write-once-read-many -> once an object is uploaded, that object can't be deleted or overwritten for a specified time set by us. 
- This can be used for an audit 
- This ensures us that we are dealing with the original file 

*Intelligent-Tiering* -> allows us to archive files and save cost 

*Event Triggering* -> If something happens in the bucket, trigger a business process

*Custom bucket policy* -> more granular 

You can also measure the *metrics* inside the Bucket Overview 

S3 is a global service, you can access buckets across regions very easily. 

#### Practice quiz question AWS will restrict public access of all buckets by default
True 

## Storage Classes
They are designed for certain uses. 
![[Pasted image 20250625190152.png]]


## Best practice: performance

The reason why we isolate customers at the folder level instead of buckets is -> performance. 

Having more folders increases the transaction capacity of put/copy/post/delete or get/head operations.

Each folder/prefix has an upper threshold. 


#### Practice quiz question: As an educational organization, which of the following storage options would you use to store records of past students that have to be retrieved only once a year for alumni meets?
S3 Standard Infrequent Access 


###### write down the differences between S3, EBS and EFS
