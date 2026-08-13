[[SQL]] [[Database]] [[NoSQL]] 
# Azure SQL
Set of database services in Azure

You can create a data base where you don't need to set up any server. You don't need to manage any infrastructure

You can use the latest stable release of SQL server. Every time you create a database you will always get the latest release 

It is scalable and highly available - geographic replication and fail over 
- Failover -> automated or manual process where a primary degraded or failed system/resource switches to a secondary or back up system  

# Deployment Model
*SQL Server on VM* -> You deploy the SQL server through a VM.
- Get full control of the VM and SQL server 
- You still need to maintain the VM 


*Azure SQL Databases* -> Fully platform databases. Most features of on-prem SQL server are supported. Cheaper and highly scalable. 
- You don't need to manage the infrastructure, compared to SQL server on VM
- Some features are not available, you need to check which are not so it doesn't affect you. 
****- You can pick a database -> MySQL, PostgreSQL, SQL Server 

*Azure SQL Managed Instance* -> Nearly compatible with on prem SQL server. Managed service, deployed inside virtual network 
- You don't manage infrastructure 
- More costly 
- Good for migrating form on prem to cloud 

# Setting up a Logical SQL Server
Logical server means that it is actually not deploying the server, but it holds the metadata. 

When you create the server, it also generates a URL similar to storage accounts, and other resources in azure. 

You also need to create an admin account. 

In the networking section you can turn on a firewall, by default it is attached. 

Estimated cost per month will be 0 because its a logical server. 

**SQL server is required to deploy any database**

# Creating a SQL database
Inside the logical server we created you can grab the server admin name and server name. 

Then inside the management console of the logical server you can click on *create database*.

From there you choose resource and subscription and name it. 

You can configure the database configurations. 
- the min size is 2 gb -> the creation window will give you the estimated cost per month. In the example the professor gave it was 5 usd. 

*Collation* -> define rules of how data will be stored in the database.  

You also determine the maintenance window time. It will be a preferable window, but it could happen outside the time you decide. 

You can also deploy sample databases for testing

After creating the database you will now see the estimated cost, compared to when we created the SQL server that had an estimated cost of 0. **You don't pay for the server but the databases you deploy**

# Connecting to SQL Database
## Query Editor - Connection Method
To connect there are various options. The professor used *Query Editor*.

Query editor is a client utility. 

Inside *Query Editor* you enter the admin name and the password. But before you connect to the database, you need to unblock the IP address from where you are trying to use the query editor in the database firewall. 

To unblock this IP, you go to the SQL server resource, then in the side of the management console, go to `Firewalls and virutal networks`. By default everything is blocked so you will need to set up the connections. 

## Azure Data Studio - Connection Method
You can use this software in any OS. You will need to download it to your system.

Here you enter the server name and the user. You also choose the authentication type. 

# Common Security Methods

## Transparent Data Encryption
All data you insert will be encrypted at rest. It doesn't affect applications, you don't need to worry about decryption. 

Happens at the database level

If you want to enable this, first you have to go back to the SQL server, from there open Transparent data encryption and decide if you want to use your own key or Microsoft managed key

## Auditing 
Server level and database level 

Tracks database events and writes them to audit logs. 
- The logs can be in azure storage or log analytics workspace or event hub 
- Logs can have expiration, you specify the number of days you want to keep them. Max is ~ 10 years. 
- You can also track the *support operations* performed by Microsoft 


## Dynamic Data Masking
Only at the database level 

Data will show in the xx format - You decide what data is visible to which users 

Masking the data is like when you see a credit card as xxxx-1234. The actual data value has been replaced by xxxx or any other character. 

When you enable data masking you can 


# CosmosDB - NoSQL 
NoSQL database - Non relational database

Schema free - flexible schema

Data is locally distributed amongst multiple nodes 

# Properties
## Flexible Schema
```json
{
	"name":"manuel",
	"address":"zxc",
}

{
	"firstname":"abc",
	"lastname":"def",
	"company":"greatlearning",
	"office_address":"...",
	"travel_options": {
					"option_1":"car",
					"option_2":"bus"
					}
}
```
Based in this example, storing this data in a relational database will prove to be very complicated. But still this is useful info.

## Distributed 
Relational database has all the data together in one set of disks. All of the compute and the data is in one place. 

But in *NoSQL* the data is stored in a set of distributed nodes (hard disks). 

Each record is inside different nodes (disks).
![[Pasted image 20251113190545.png]]

## Replicated 
If you have R1, you have multiple copies of the data inside different nodes. 
![[Pasted image 20251113190802.png]]

The benefit of this, is that you have redundant data. So if one node crashes you have *high availability and disaster recovery*.

If your disk requirements increase, you can easily scale your data through *horizontal scaling*. 
- The physical hardware is the only limiting factor. You can store unlimited amount of data. 

The user can fetch data from any location (if his permissions allows him to).
- compared to a relational database, all the queries go to one place. In NoSQL, there is *higher throughput*. 
	- It doesn't have to run every query in one single place, only in the available and nearest node. 

You can serve millions of requests per second. It will fetch the data from the nearest location. 

*low latency* is provided by having the nearest and available node fetch the data.  

# Use cases
e-commerce sites -> each product has different attributes

Content management -> images, videos, text, etc. 

Personalization

Build a network of entities -> for example, linkedin, different types of connections. 

# NoSQL Database Types
## Key-Value store
Similar to a dictionary. The key needs to be unique and in the value you can store anything you want. You can store an image, video, text, or combination. 

This is how the computer sees it:
![[Pasted image 20251113192905.png]]

The only requirement is a unique key 

Optimized for simple look ups 
## Document stores
Implementation of a *key value store*. You still have a key (needs to be unique). Each key has a value, the value has a type of schema. Still, its a flexible schema, but it does have some structure (flexible structure).

You can query: `give me the documents where prodcut 2010 has been sold.`
- This query takes a bit longer since the schema is flexible. 

For example:
![[Pasted image 20251113193212.png]]

Documents can be different formats, xml, json, yaml, bson, etc. 

## Wide-column/Column family/Column stores
![[Pasted image 20251113193701.png]]

Column families. You create columns based on the nature of the data. 

You can fetch individual categories of data.

Columns also have flexible schemas, for example you can store names for one user, names and suffix for another, and so on. 

One family is identity and another is contact info. 

Keys are unique
## Graph Stores
node and edges 
![[Pasted image 20251114170525.png]]

Each node is related to another one by edges

Good for relationships between entities

query can look like `list of employees that work in marketing`

queries traversing nodes by using relationships 

