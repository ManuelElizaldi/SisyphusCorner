[[Service Isolation]]
##### What happens if an auto-scaled instance is terminated manually? Assume the following -
- Upper CPU bound check is at 80%
- Lower CPU bound check is at 20%
- Auto scaling group Min = Desired instance = 10
- Auto scaling group Max instances = 45
- Target group size is 10 instances
- Current average CPU utilization = 15%

Answer -> Another instance will be launched automatically 
Breakdown -> Since the number of instances in the target group is the same as minimum instances specification in the autoscaling group, any degredation below 10 instances will mean it needs to be replaced irrespective of the CPU utilization. The terminated instance has to be replaced to ensure the minimum instances criteria is not breached.

##### For a sensor network which transmits daily data to be collected by an application server at predictable intervals, which of the following autoscaling policies would be a better fit to meet this type of workload?

Answer -> Set to a fixed value
Breakdown -> For predictable workloads, a fixed number of servers is desirable. The auto scaling group can "maintain" the capacity. If this workload remains the same for long periods of time then perhaps either reserved instances or savings plan can reduce costs.


##### As a corporation with a large number of developers using the AWS CLI tool, which of the following would be the best way to store their access credentials as a backup?

*Answer* -> Stored on dedicated encrypted drives on the company server
*Breakdown* -> Access credentials need to be protected with the utmost secrecy and care should be taken that they are not misplaced or easily retrievable by unauthorized individuals. Hardware security modules (HSM) are also a great way in which these credentials can be stored on-prem as well as on the cloud.

##### A bundled package of OS along with applications installed on it is called ______________ in AWS.

AMI

##### Assume the following deployment specification -

- 5 manually created EC2 instances already exists
- Load balancer and a target group (TG) with the 5 instances
- The TG is attached with an autoscaling group (ASG) and scaling policy is based on CPU
- The ASG has been created with "minimum" instance of 2

What is the minimum number of EC2 instances that will be active at any point of time in the TG even if CPU thresholds are not breached?

Answer & breakdown -> 7, Total number of instances = 5 (Manually created) + 2 (Minimum contribution from the autoscaling group) = 7

##### Snapshots can be used for _
Answer -> boot able image, data migration across regions, back ups

###### Can services/instances talk to each other across regions? 
yes and no. You have to set it up manually and its not as seamless as resources talking to each other within one region. Services are isolated within regions. 

*Service isolation* -> provides fault tolerance, disaster recovery and data sovereignty. 

There are different ways in which 
