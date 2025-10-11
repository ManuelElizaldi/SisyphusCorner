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

