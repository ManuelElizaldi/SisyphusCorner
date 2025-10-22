[[Storage]] [[Azure]]
# Data Protection
*Soft Delete for Blob* -> you can keep the blob in the thrash for a couple of days that you determine. 
- In your container where you can see all the files, there is a slider that allows you to show the deleted blobs 

*Tracking/versioning* -> You can track versioning = track all changes done to the file. 
- Different from snapshots. Snapshots are taken manually, tracking is done automatically. You can revert to older versions of the file. 
- *Does this cost?*
- You have to manually delete the old versions of the file if you want to completely delete the file 

 *soft delete + versioning* -> To fully delete a file when doing versioning + soft delete, you have to 1) delete all versions 2) wait after the threshold has crossed for soft delete -> then the file will be fully deleted 

## Turn on blob change feed
any time a change is made in the blob, it will be tracked inside the container in a $blobchangefeed item 

## Point in time restore for containers
for this feature, you need to have versioning, change feed and blob soft delete enabled. And you choose the maximum restore point in days 

## Leased containers
This can be enabled on blobs or containers 

Deletion of containers is disabled. If you want to delete the container you need to pass the lease id or breaking the lease 

#### Benefit of a lease
You can apply it to blobs or containers 

prevent accidental deletion

if multiple people want to modify the file, then which ever application acquires the lease first, that app only can modify the file 

# Access Keys
keys have full permission of storage accounts 
- Even deleting the storage account
- They are very powerful
- The professor recommends not even using them 

You can regenerate another key at any moment in case you think it's compromised 

*connection string* is used to get access to any data in the storage account
## Allow shared key access - enable or disable
turns on or off the key 

This needs to be enabled if you plan to use *shared access signature*

# Shared Access Signature (SAS Token)
Limited rights key 

at the storage account level, at container level, at individual file level 

### Creating a SAS - file level
Temporary access. 

You go into the file/blob and in the settings, you will find a tab that says *Generate SAS*. Here you define what permissions you want to give. 

Inside this settings window you define the start and expire dates 

You can define what IP addresses have access 

You can also determine the protocols for allowed  

You need the blob SAS URL to access the file, this is a URL that combines the key and the URL 

### Creating a SAS - Storage account level
You can determine to what storage service you want to give permission 

You also define what permissions 

Resource types -> service, container, object 

You give access to all the containers 

Same expiration settings from file level are available 

## SAS Token
Once generated, you can't see how many you have generated and to who you have given them

### Controlling SAS Tokens -> Stored Access policies
You control time frame and permissions of SAS keys

*For example* -> you give 100 and are linked to one policy. You can delete the policy and then all the tokens will be invalid

gives the ability to manage SAS Tokens

# Access Tiers
Where you want to store the data? Depending on the tier, is how fast you can get your data. 

*Hot Storage Tier* -> fast storage, data is cached. read and write frequently. Latency is milliseconds. Storage is costly, but access and transaction cost is low.
- *RA-GRS* (Read access GRS) -> 99.99% availability, very low downtime 

If a file is not being used after x amount of time you can move it to Cool tier to lower the storage cost.
- Physical movement of the file 

*Cool Storage Tier* -> Lower storage cost, higher access and transaction cost 
- minimum storage duration - 30 days. If you move data before 30 days, you pay for the days that you don't use. 
	- Example -> if you move a file after 5 days, you pay for 25 days.
- 99.9% availability, there could be a day where there is downtime 

*Archive Storage Tier* -> You can move from hot to archive directly, but the file becomes offline. Microsoft stores it in an offline data center. If you want to see the file, you will request a Blob rehydration from Microsoft and it will be moved to cool or hot storage. IT can take up to 15 hours to get the file. 
- Highest access and transaction cost. But storage cost is the lowest. 
- 1/10 the cost of Hot storage 


# Setting up Access Tier
Inside the storage account you choose the blob access tier 
### Default Upload 
You determine the Access Tier inside the storage account, this will act as the default setting. 
### When uploading a file
In the upload setting you can choose where to upload it. 
### Moving a file
To move files into a different tier, you choose the file in your container, there is an option of *change tier*, once you save the change it will be moved to a different storage. 
### Uploading bulk files
Inside the storage account, there is a *life cycle management* section where you can write rules to move files between tiers  

You want to apply to block blobs or append blobs? You can change this

Do you want to apply to main file (base blob), snapshots or versions? You can choose to which to apply. 

#### Building rules - life cycle
These work like if statements, for example you can move to cool storage after 30 days

You determine the rules for *Base blobs, snapshots and versions*. 

#### Filter set 
you can specify the name of the container and the prefix, for example:
- Container1/Test -> all files that start with 'Test' in container 1 will have the rules applied to them. 

Rules are evaluated every 24 hours. 

## Blob Inventory 
Inventory report made up of the metadata of your blobs in a specific container 

## Object Replication
Copy data to another storage account. You can define the replication rules. 

You choose the destination storage account to which you want to copy. If you do this, you are paying twice. 

You can define certain filters to choose which data to copy. 

### Replication - Inside Storage Account Settings
Defined when creating a storage account but can also be changed after creation. 

This is about **How your data is replicated to a different location**.

# Redundancy Options
## LRS - Local Redundant Storage
![[Pasted image 20251015175814.png]]

3 copies within same data center with sync copy 

*sync copy* -> you upload the file and it creates 3 copies 

prevents against server rack failure. 

If the data center fails, your data could be lost. One point of failure

## Zone redundant storage (ZRS)
![[Pasted image 20251015175921.png]]

1 copy across 3 data centers/availability zones.

sync copy 

prevents against data center failure 

## Geo redundant storage - GRS
![[Pasted image 20251015180305.png]]

You upload the file, 3 copies get created and then another set of 3 copies are created in another data center/availability zone

primary -> sync copy
secondary -> async copy -> happens in the background 

prevents against regional failures 

cost increases because you are using 2 regions 

*problem with this approach* -> if region 1 goes down, data is safe in the secondary region, but you can't access this. So to access this you have to wait for region 1 to be back up. You can also perform a *fail over* -> region 2 becomes the primary and you can access your data 

Prevents against regional failure
## Read Access Geo Redundant Storage (RA-GRS)
![[Pasted image 20251015180947.png]]

Same as GRS, but your data is has read access in the secondary availability zone. 

This gives higher availability 

## Geo Zone Redundant Storage (GZRS)
![[Pasted image 20251015181544.png]]

3 copies in each data center in one region, then the secondary has 3 copies of your data in one data center

primary does sync copies and on the secondary its async 

Prevents against regional and data center failure 


## Read Access Geo Zone Redundant Storage (RA-GZRS)
![[Pasted image 20251015181807.png]]

Same as RA-GRS but has read access in the secondary availability zone

prevents against regional and data center failures + higher availability 

## Setting up the Redundancy Options
There is something called *Regional Pairs*, if you choose region x, azure pairs it to region y. 
- example -> East US is always paired with West US, Hong Kong is always paired with Singapore,etc. 
	- You have to be aware of the policies. Maybe you can't take data from your country and store it somewhere else. 

### Failover
This is triggered from the Geo Replication set up section in the Storage Account 

After you do this, all your data will be transferred to the secondary AZ and become LRS

# Performance Tiers

*standard* -> tiers to store data: hot, cool and archive. Supports redundancy options and is great for most use cases

*Premium* -> a lot of read and write ops. Data is stored in SSDs, no tiers available. Supports only LRS and ZRS. Great for cases with high transaction and low latency 
- Big Data projects for example 

This setting in storage account CAN'T be modified after creation.

## Encryption
Inside storage account, there is an option for encryption. By default everything is encrypted with Microsoft managed keys 
- Data is encrypted at rest by Microsoft. 

You can also provide your own key and store it in key vault inside azure. 

