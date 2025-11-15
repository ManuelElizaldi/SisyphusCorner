[[NoSQL]] 
# Azure CosmosDB
Cosmos DB is not a NoSQL database, CosmosDB is a *NoSQL platform*. This means it supports different types of databases on top of it. 

Supports NoSQL features -> distributed, replication, horizontal scaling, high availability, low latency 

Fully managed => you don't need to manage infrastructure

Multi API support 
- supports five APIs

Supports any type of NoSQL stores

Supports global distribution
- You can keep data in multiple regions
- you can have a read region and a write region 
- multiple write regions 

automatic expiration of documents using time to live feature 
- You determine how long documents live

# CosmosDB APIs
## Table API
*Key value store*, similar to azure table storage.
- instead of using table storage, use Table API 

It can have global distribution 

## Core (SQL) API
*Based on Document store NoSQL database *

Stores data in json format 

It supports SQL syntax to query data 

Stored procedures, user defined functions and triggers in JavaScript is only supported on Core (SQL) API
- You have to use JavaScript to use functions and triggers 

## MongoDB API
*Document store*

MongoDB service in Azure, powered by CosmosDB 

 Use existing MongoDB libraries, tools and applications

You can migrate easily from on prem MondoDB to azure MongoDB and keep the same functionality. 

## Cassandra API
*Columnar store *

developed by FB, you can use Cassandra services in Azure powered by CosmosDB. Your on prem data can be migrated to Azure CosmosDB.

You can still use Cassandra libraries and functionality 

## Gremlin API
Graph store

Based on open source Apache Gremlin. 


# Setting up CosmosDB
## Creating CosmosDB Account
First you have to create an account. Account name needs to be unique, same as other resources in Azure. 

You choose the API  type you are going to use. **You can't change the API type after creation**

*Capacity Mode*

While creating the account you choose if you want geo-redundancy, multi region writers and availability zones. 
- This you can change after creation.

There is backup policy 

data is encrypted at rest 

# Resource Model
![[Pasted image 20251114174715.png]]

*Cosmos DB account* is where you specify the account

Within one account you can create *multiple databases *

Within each database you can have *containers*. Compared to SQL Relational databases, containers in NoSQL act as servers in RelationalDB.

*Container is just a table* where you can store data. Within tables, you store *items*.  

**Cosmos DB Account -> Database -> Container -> Items** 

## Some notes on implementation 
There are record attributes added automatically to the CosmosDB data

If you don't provide an ID when entering data in a NoSQL database, the database will provide the ID itself. 

## Queries
You can use regular SQL to query NoSQL databases in Azure 

If you use a where statement and the column you are using to filter does not exist, the document/table will be ignored


# Resource Model API
Terminology:
![[Pasted image 20251115134657.png]]

# Connecting Azure Function to CosmosDB - Output binding 
Inside CosmosDB you will have a `keys` section. Inside the keys you can find the URL, Primary key, Secondary key and connection strings
- You need the primary and secondary keys to connect 

Now inside your function app, in the output binding you decide the output -> CosmosDB. 
- when you are entering the output, you type in the database name, collection name and enter the connection string 

Once you reference the connection string in the function, you will be able to connect both resources.



