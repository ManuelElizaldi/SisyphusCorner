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

