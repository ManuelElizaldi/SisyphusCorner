![[Pasted image 20260330193858.png]]

## S3 Bucket
Created a bucket with private access. Since this is patient data it should be kept private. 

Then we create a folder and inside we place the csv provided. 

## Athena 
Athena - Serverless SQL. 

It requires a separate bucket to store the query results.

Then in Amazon Athena, inside query editor -> query settings -> manage -> select the new bucket we just created:
![[Pasted image 20260330194649.png]]

**IMPORTANT:** When using AWS Athena always configure this first. 

## AWS Glue
Glue is able to crawl your S3 folder and automatically detect the CSV columns and create a table definition in the *Data Catalog*. Without this, Athena does not know your data's structure. 

### Creating IAM Role for Glue
Inside IAM -> Roles and we create a role. 

Inside the role creation page, we select a service -> glue. 

The permission we are attaching to this role `AWSGlueServiceRole` grants AWS Glue permission to access related services like EC2, S3 and CloudWatach Logs. 

We are also Attaching `AmazonS3ReadOnlyAccess` -> why? 
- I suppose this is for security, we don't want glue making any changes to our data, we just want it to read it to create our schema. 

### Creating a Glue Crawler
Inside the Glue menu, on the left hand side you can see the option for Crawler. 

We create one and point it to our S3 bucket with the lab results. You choose the data source in the creation menu. There's multiple you can choose from, right now we point it to the S3 bucket. 

You can choose if it should crawl existing folders, or only new ones that get created. There's also an option to crawl based on events. 
- rely on Amazon S3 events to control what folders to crawl.

Here we attach the permission we created earlier. 

We create a new database to hold the results, this is created within the Crawler creation window. 

Finally we execute the crawler by running it. 

Running state:
![[Pasted image 20260330201200.png]]

Since this is a small dataset, it completed in 44 seconds. 


> [!NOTE] **💡 What just happened:**
> Glue read the CSV header row, inferred the data types for each column and created a table called lab_results in the healthcare_db database in the Glue Data Catalog. Athena can now query it using SQL. 

### Glue Tables
After the crawler ran, inside Tables in AWS glue, we can see the output:
![[Pasted image 20260330201600.png]]

It is good practice to double check the columns. 

## Querying the data 
Inside Athena -> Query Editor -> Select the corresponding data source - Database Healthcare_db

We can run queries here:
![[Pasted image 20260330202121.png]]


# SAA Exam Tip - Cost Optimization
Athena charges per TB scanned. On a 30-row csv, the cost is essentially $0. 

In production with 500GB daily being uploaded to S3, the way to optimize this is to use *parquet format* using a Glue ETL. This will compress the data and reduces Athena scan costs by 60-90%.


## Athena QuickSight 
For this I needed to create a QuickSight account with the same email as my AWS account. 

Now we have to grant permissions to QuickSight to be able to read S3. Inside Quick, in the top right corner in Manage Account you can find the security settings required for this. 

AWS Resources in Security section. 

We grant access to S3 - both buckets. 
![[Pasted image 20260330204448.png]]

I also grant access to Athena. 

### Creating a QuickSight Dataset
On the left hand side menu we select datasets. We create a data set from Athena.

We choose the SPICE import method since this is faster. 


# Exam Connection
Everything you just built maps directly to exam questions. Here's what to remember:

- **Athena + Glue + S3** = the serverless analytics trifecta. If you see "query S3 with SQL, no servers" → this is the answer
- **Glue Data Catalog** = Athena needs this to know your schema. Without it Athena can't query
- **Parquet format** = exam always asks about cost optimization for Athena → convert CSV to Parquet via Glue ETL job → 60-90% cost savings
- **QuickSight** = the BI visualization layer. "Dashboards for business users" → QuickSight. Not Athena, not Glue
- **SPICE** = QuickSight's in-memory engine. Faster queries, doesn't re-query Athena every time
- **S3 Block Public Access** = HIPAA/compliance requirement. Macie detects violations
- **IAM Role for Glue** = services never use access keys — always IAM roles

# Claude Questions:

What happens if there's multiple csvs in a S3, will this create multiple tables? 
- Glue crawler will create one table per folder. 

What if I want all the CSVs to populate 1 table? imagine there's 5 clinics all producing lab results, I want 1 table for all lab results. How does this look in practice?
- In practice, all lab results should be placed in one folder. 
- Also, each CSV should have the same header for all of them. **Consistent Schema**


What is parquet format? 
- Form of columnar storage, it makes queries more efficient. With CSV, Athena looks at all columns, with parquet, it will only look at the mentioned columns in the query. 
- Compresses well.

### AWS Exam Tip -> Reduce Athena Cost -> Parquet format


I accidental saved the table as healthcare_lab_results_meb_2026, can this be changed? 
- I updated the settings in the Crawler, there is a section for table name. Table name prefix - _optional_ Here's where I added lab_results, but now the name is -> lab_resultshealthcare_lab_results_meb_2026 instead of the first -> healthcare_lab_results_meb_2026\
- **The Fix** -> Delete the table and re run the crawler, glue will use the folder name for the table name 

## Subfolders in Glue 
This is the recommended pattern for production data. 
```
S3 bucket/
└── lab-results/
    ├── year=2026/
    │   ├── month=01/
    │   │   ├── day=15/
    │   │   │   └── results.csv
    │   │   ├── day=16/
    │   │   │   └── results.csv
    │   │   └── day=17/
    │   │       └── results.csv
    │   └── month=02/
    │       └── day=01/
    │           └── results.csv
```

Glue can recognize the key = value naming pattern. Creates one table with extra partitions. 

Table will look like this:
```
Table: lab_results
Columns:
├── patient_id
├── test_type
├── result_value
├── status
├── year      ← automatically added as partition column
├── month     ← automatically added as partition column
└── day       ← automatically added as partition column
```

Think about how you will run queries before you generate tables. You want to optimize the reading time of each query. 

```SQL 
-- WITHOUT partitioning:
-- Athena scans ALL data for the entire year
SELECT * FROM lab_results
WHERE lab_date = '2026-01-15'
-> this will scan the entire year. 


-- With partitioning 
-- Athena can read only 15 days. 
SELECT * FROM lab_results
WHERE year = 2026 and month = 01 and day = 15 
-- This is 90% cheaper
```

### Exam Tip
To optimize Athena costs, you can use parquet format + partition by date. 

Use key = value for partitioning

3 levels max deep

