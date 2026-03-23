Static IP not change - network load balancer, elastic IP

Elastic Beanstalk 

Transit Gateway - centralize multiple services together. Specially where you go beyond a number of services. 
- CIDRs overlapping 
- *VPC Peering not transitive* 

Resource Access Manager - 

Direct Connect 

vCPU limit-based on demand instances per region 

On demand instances in pending state are billed because services are being allocated 

You will be billed when your on-demand instance is preparing to hibernate with a stopping state

# RedShift 
Fully managed cloud data warehouse, this is used for analytics and reporting, rather than day to day transactions. 

||**RDS (Operational DB)**    |    **Redshift (Data Warehouse)**|
|---|---|---|
|**Purpose**|Day-to-day transactions|Analytics & reporting|
|**Query type**|Many small, fast queries|Few massive, complex queries|
|**Data volume**|GBs|TBs to PBs|
|**Example**|"Save this order"|"What were total sales by region last year?"|

Think of RDS as your **cash register** and Redshift as your **accounting department** that analyzes all the receipts.

Data warehouse system. When redshift stores data in its nodes, it uses distribution style to decide how rows are spread around. 
- this is related to query performance. 

| Style    | How it works                                                                       | Best for                                                 |
| -------- | ---------------------------------------------------------------------------------- | -------------------------------------------------------- |
| **EVEN** | Rows distributed round-robin across all nodes                                      | Large tables with no clear join key                      |
| **ALL**  | **Entire table copied to every node**                                              | Small/medium dimension tables that are frequently joined |
| **KEY**  | Rows distributed based on values in one column — matching values land on same node | Large tables frequently joined on a specific column      |
| **AUTO** | Redshift decides automatically based on table size                                 | Default — let AWS optimize                               |
## Why ALL makes sense 
When doing a join between tables data does not travel between nodes, increasing performance. Every node has the tables locally. 

### SAA Exam tip:
Redshift distribution styles come down to the nature of the data you are storing.

- Frequently joined -> ALL
- Large tables with a clear/common key -> KEY
- No clear pattern -> EVEN or AUTO 

## How data usually gets to Redshift

```
Operational DBs (RDS) ─┐
S3 Data Lake          ─┤→ ETL/ELT → Redshift → BI Tools (Tableau, QuickSight)
Streaming (Kinesis)   ─┘
```


# Prometheus server on EC2 
Prometheus -> Monitoring for containers 

Created a Prometheus server first, then we create a role to add a policy -> `AmazonPrometheusRemoteWriteAccess`. This policy allows EC2s to use Prometheus. 

Through the instance EC2 we run a couple of commands to install go and prometheus. 

