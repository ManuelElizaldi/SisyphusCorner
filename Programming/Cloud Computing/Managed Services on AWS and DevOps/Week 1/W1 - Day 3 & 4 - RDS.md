[[RDS]] [[SQL]]

# RDS - Managed Database Service

Managing a database on prem can be time consuming and expensive. RDS managed service offers a solution to this problem. You can connect your application easily to any of the engines. 

If you run a RDS on prem, you need to invest in hardware, software and human capital

**Benefits**:
- Cost saving - pay as you go
- Scalability - encryption, data storage 
- Security 
- Better performance 
- You don't have to worry about routine operations performed on a database, now you only worry about the core business operations

## Supported database engines
Oracle, MySQL, PostgreSQL, Microsoft SQL, IBM DB2, Maria DB

## RDS Terminology
*DB Instance* -> Isolated database environment. This environment can contain multiple databases.

*DB Instance Class* -> Determines the computational capacity of a Amazon RDS DB Instance
- This depends on your application's requirements

*Instance Storage* -> It uses Amazon Elastic Block Store volumes for database and log storage 


## Types of Storage

*General Purpose* -> cost effective and can cover a broad use case scenarios - medium sized DBs

*Provisioned IOPS SSD* -> Designed for intensive I/O workloads. This is used for low latency and consistent I/O through put.

*Magnetic* -> designed for backward compatibility 

## Monitoring and maintenance 
Amazon CloudWatch can be used for alerts and monitoring. Cloudwatch has charts that monitors the health of a DB Instance 


**Security Group** is set up to determine who can access the DB Instance - a range of IPs is given. 

**Maintenance window** -> there is a weekly window of time where maintenance is performed on the DB Instance - patching, updates, etc is applied.
	- This is performed randomly, but you can also determine when this happens. 





