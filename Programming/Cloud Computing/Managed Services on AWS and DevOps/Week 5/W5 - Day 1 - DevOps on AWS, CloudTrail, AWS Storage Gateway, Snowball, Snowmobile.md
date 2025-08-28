[[DevOps]]

# CloudTrail
*CloudTrail* -> Track user activity and API usage. Anything done inside the console, CLI and API will be captured. 
- Enabled by default 

If there's an attack or a hacking attempt, this allows forensic analysis. We are able to trace back with this tool. 

We figure out who did it and how we can prevent this in the future. 

## Management Console
You have a recent events section.

You can view events in json - then build your own analytics from this json.

### You can create a trail
You can apply to all regions - in case you have a multi regional environment 

*Management events* -> select all, both read and write. Unless you are only interested in tracking read or write.

*Data events* -> only applies to S3 and lambda. You can select all S3 buckets, but this can be very expensive. Same for lambda functions, you can track all of them but it can potentially be expensive. 

You can specify in which S3 buckets to store the created logs. 
- not sure if you can specify other storage option apart from S3. 
- Encryption is available 

*SNS Notification* -> You can enable SNS notifications. 
- There is potential to create a pipeline to analyse the logs, notify other people, etc. 
	- for example SNS could trigger a lambda function to parse the json and produce some sort of output 


## Management events
$2 USD per 100,000 events


## Data events
$0.10 cents per 100,000 events


#### Every AWS account should have CloudTrail enabled to the max. 

# AWS Storage Gateway

## Hybrid Cloud
This approach is very common now a days. On prem + cloud managed service. Context: During the late 90s and early 2000s enterprises would have a central place to store and version documents. People could access this regardless of where they were logging in from.  There were products that would address this need.

AWS Storage Gateway is one of those products. 

## AWS Storage Gateway
Enabled cloud work loads. 
- Allows seamless movement of data from on prem to cloud  

Back up and archive to AWS 
- You have all of your data on prem but you use Glacier archives to store back ups of data on AWS. 

Tiered Storage on AWS
- Can grow as needed 
- Expands on prem NAS and SAN storage 

### 3 Flavors of Storage Gateway

*File Gateway* -> File interface to S3
- Central storage becomes S3. 

*Volume Gateway* -> You can mount volumes into your on prem storage
- Cached volumes -> you store your data in S3 and retain a copy of frequently accessed data locally. Offers cost savings 
- Stored volumes -> Really fast, low latency access to your entire dataset. S3 acts as a backup, asynchronously back up. 

*Tape Gateway* -> you can have your entire data in tape drives and store it on the cloud. Uses Amazon Glacier. 


## AWS Snowball - Migration of data into cloud 
Assuming you have terabytes of data. 
![[Pasted image 20250826182804.png]]

AWS snowball uses the little boxes above to transfer your data. You order Snowball and the device (little box) is shipped to your organization. You transfer your data to the snowball and then AWS comes and picks it up. 
- Fun note: this box can resist several Gs of force and its waterproof. 

50 to 80 terabytes 


## AWS Snow mobile 
![[Pasted image 20250826183018.png]]

Same as the snowball, but this is bigger. They come to your prem on this truck. 

100 petabytes per snowmobile 

You can also have people protecting your shipment (armed people), just as extra insurance. 

Only AWS offers this massive transfer of data. 