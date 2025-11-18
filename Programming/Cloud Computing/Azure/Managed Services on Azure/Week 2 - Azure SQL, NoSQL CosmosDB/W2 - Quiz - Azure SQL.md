**Which of the following database hosting options are available in the Azure SQL family of services?**
Managed IaaS, PaaS, IaaS 

Azure SQL is a family of managed, secure, and intelligent products that use the SQL Server database engine in the Azure cloud. These include Azure SQL database, Azure SQL Managed Instance and SQL server on Azure VMs.

**Consider a NoSQL database containing the customer information of an e-commerce site. One of the frequent use-cases is to retrieve the name, address, and account ID of a customer when required, in that order**

**Which of the following is a reason why a column-family database would be used here instead of a graph-based database?**
Related fields can be put in a column family to make retrieval faster

Column-family databases are best used when you have established query patterns. In this case, for example, the name, address, and account ID can be put in a single column family to make access easier.

**Which of the following Azure SQL deployment options should you use when the number of databases to be created is variable.**
Only Azure SQL databases offer elastic pools which can be used to host multiple databases.


**Which of the following Azure SQL deployment options should you use when the number of databases to be created is variable.**
Azure SQL Database

Only Azure SQL databases offer elastic pools which can be used to host multiple databases.

**Which of the following APIs are supported by CosmosDB?**
Gremlin, MongoDB, SQL API

Azure Cosmos DB offers multiple database APIs, which include the Core (SQL) API, API for MongoDB, Cassandra API, Gremlin API, and Table API.

**Azure SQL databases can be transparently encrypted. What is the significance of the term "transparent" in this context?**
Encryption and decryption do not affect any applications connected to the database

Transparent encryption signifies that encryption and decryption are managed by the service, and is invisible to all external applications.

**Which of the following algorithms is used to handle conflict management in CosmosDB by default?**
In Last Write Wins, if two or more items conflict on insert or replace operations, the item with the highest value for the conflict resolution path becomes the winner.

**Data for the compute layer in the standard availability model for Azure SQL is stored in SSDs instead of premium storage. Which of the following is the most logical reason for this?**
The compute layer is stateless and all data is transient.


**Which of the following Azure SQL purchasing models would be more beneficial for BYOL (Bring-Your-Own-License) use-cases?**
vCore based models let you take advantage of Azure Hybrid Benefit on SQL databases and SQL Managed instances by allowing you to bring your existing licenses for discounted rates on these services.
