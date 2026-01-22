# NoSQL
Where to use NoSQL -> social media, unstructured, all the data produced by automated cars can be stored in a NoSQL

Managed instance -> The infrastructure is updated, patched and maintained for you. You run the newest version of the database.

Many companies use MongoDB for their NoSQL databases. If you client does not want to use MongoDB, that's fine, you can have a NoSQL database in Azure using MongoDB's format. 

NoSQL has strong consistency -> does not matter from where you write the data. You can see if from multiple regions 
- *Session consistency*

*Consistent prefix* -> read order is guaranteed, timing is not 

*Bounded staleness* -> if you choose a cheaper option of NoSQL database, you might encounter some lag 
- Strong consistency - perfect accuracy vs eventual consistency (fastest performance)
## Cosmos DB
This is the NoSQL option in Azure. 

Offers global infrastructure. You preform a write in US, but can read the data from EU. For example:
- If you have IoT or solar panels or oil rigs, you need to capture data in multiple regions, you can use Cosmos DB for this.

# Azure SQL DB
SQL Databases can become expensive on the cloud. You have to determine what is the best option for your project 

# Elastic Pool
This is used for scaling. If you notice that the use of your database goes up and down and you don't need a database constantly running you can use this. 

How it works -> You share your compute power with other users. Azure handles this. 
- Similar to how you share spot instances. 
- **The professor did not recommend using this in production**


### DB Options
SQL DB -> Fast provisioning and scalability - good option. 
Single DB -> For when you are just starting out.

Serverless Single DB -> SaaS model, you don't have to manage a database server or a VM. You just deploy the database. *does not have constant throughput*. You only pay for when it is being used. Scales resources based on demand. 

## SQL Deployment Options

most managed = PaaS & most customizable = IaaS

**Azure SQL Database** -> Fully managed by Microsoft. Backups, updates, etc. Highly available. Since Microsoft manages everything, you don't have access to the underlying OS
- Best for cloud native apps, sporadic workloads - serverless

**Azure SQL Managed Instance** -> PaaS, fully managed, simulates an on prem environment. No access to underlying OS. 
- Good for lift and shift migrations that require on prem compatibility 

**SQL Server on Azure VM** -> You manage the SQL server and the OS (dependencies, libraries, patches, etc.).
- Best for legacy apps requiring OS access or specific SQL versions. 

![[Pasted image 20251116101543.png]]

**Data bricks can present good career opportunities for data engineering **