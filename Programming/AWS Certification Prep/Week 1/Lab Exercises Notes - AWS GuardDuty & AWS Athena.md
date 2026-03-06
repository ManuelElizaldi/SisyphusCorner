[[AWS]]

# AWS GuardDuty 

Monitors your work loads for malicious activity and delivers detailed security findings for visibility and remediation 

Using machine learning and anomaly detection it can detect:

- unauthorized activity
- suspicious network activity 
- malware infections
- data ex filtration
- account takeover 

Offer continuous monitoring, account take over, etc. 

## Integration
It can integrate with other AWS monitoring systems like AWS Security Hub and Amazon detective to help you investigate and respond to threats 

## Cost
No upfront cost, you only pay for what you use

## Architecture Diagram
![[Pasted image 20260303150109.png]]


**Detector ID** -> represents the resource GuardDuty 

**Service Roles** -> GuardDuty uses a service role to monitor data for you 

Finding can be automatically exported to CloudWatch or to a S3 bucket 

You can suspend and disable, but when you disable GuardDuty you lose all the custom settings and findings. 

**List Management** -> Inside this setting you can list safe IPs and threat IPs

**Accounts** -> here you invite other AWS accounts into your GuardDuty and you master account can monitor member accounts
- You can only have one master account per region and up to 1000 member accounts 

### Generating Findings
![[Pasted image 20260303155627.png]]

you can generate sample findings like in the screenshot above. 

When you click on a finding, you will see this window pop up detailing the services that are affected, the account, the severity, etc. 

![[Pasted image 20260303160002.png]]


You can investigate further with the 'investigate with Detective' button.

---

# Athena 
Query service that makes it easy to analyze data in S3 using standard SQL. 
- Serverless resource 
- Under the hood it uses Presto 

Pay per query model 

It can easily integrate with AWS Glue for metadata management 

![[Pasted image 20260303165640.png]]


> [!NOTE] Note
> Athena's serverless nature allows users to analyze data stored in S3 without the need for any infrastructure provisioning or management. This means that users can focus solely on querying and analyzing their data without worrying about setting up and maintaining servers or clusters. The pay-per-query pricing model of Amazon Athena ensures cost efficiency, as users are only charged for the actual queries they run. This flexibility and cost-effectiveness make Amazon Athena a powerful and convenient tool for data analysis tasks in AWS.


# Workgroups - Athena feature
Workgroups allow us to separate users, teams, applications, workloads and set limits on amount of data for each query or the entire workgroup process. 

you choose the analytics engine for each workgroup

When setting this up, you can also determine if athena manages the results or if you manage them yourself. 
- S3 query output management 

Inside IAM you can determine what data is visible to each work group 

Workgroups are also used to manage costs. 

# AWS Glue
Serverless data integration service. Helps you prepare data for data analysis and move it into different resources. 

You only pay for the resources used when preparing data. 

ETL service 

**Glue table** ->  Represents the structure and schema of the data stored in the S3 bucket.  
- This need to be associated to a Glue Database
- you decide the source of the data (s3, kinesis, kafka)
- You also need to point to the path of the S3 bucket 

After deciding on the settings of the table you have to create the schema and data format (csv, json, xml, etc.)

# Querying the table with Athena 
Athena console:
![[Pasted image 20260303171600.png]]

On the top right corner you choose the workgroup 
## Lab
We created a workgroup glue database, and a glue table and then we queried the S3 bucket which contained a csv file with expenses 


