[[Autoscaling]] [[Elasticity]] [[Monitoring]]
 
# Autoscaling 
self healing 

Ideally instead of having a fixed number of instances inside a target group, you have a number of instances that go up or down based on demand -> autoscaling group

*Autoscaling group* -> has the ability to monitor utilization, and when a certain threshold is reached, it takes an action. This is based on 'ifs'. Examples:
- If CPU > 80% + 2 instances -> upper limit 
- If CPU < 80% - 2 instances -> lower limit
- Min size -> minimum contribution to target group -> 1 instance for example, at any point in time the auto scaling group will contribute 1 instance 

This depends on *Cloud Watch* -> Monitoring capabilities that raise an alarm. Rules for the autoscaling group are set in the Cloud Watch.

Alarm -> Cloud Watch
Adding instances -> Auto Scaling Group

## Adding your application to the new instances

*Custom AMI* -> Building your own OS
#### Launch Configuration:
*Bootstrap scripts/User data* -> runs with root privileges. It gives the instance a template of all the requirements and dependencies/settings 

The Autoscaling group takes in this config file script. 


### Summary
Autoscaling group is a service that allows you to define a group of identical instances and automatically adjust their number based on the criteria you set

Autoscaling groups are used to ensure your application can handle traffic and maintain availability without manual intervention

Autoscaling groups are valuable for ensuring applications are both highly available and cost effective in dynamic cloud environments 

# Little's Law

*Loose Coupling* -> helps isolate behavior of a component from other components that depend on it, increasing resiliency and agility. 
- Each service depend on each other as little as possible. 

#### Observe your infrastructure

CloudWatch can be enabled for load balancers -> Little's Law can help you determine how many instances of compute (EC2) are needed

$$
L = λW
$$

- L = number of instances (or mean concurrency in the system)
- λ = mean rate at which requests arrive (request/sec)
- W = mean time that each request spends in the system (sec)

Example: At 100 requests per second, if each request takes 0.5 seconds to process, you will need 50 instances to keep up with demand:

$$
(50)L = (0.5)λ * (100)W
$$

# Predictive Scaling 

Predictive Scaling -> Using [[Machine Learning]] to analyze historical traffic and usage patterns to forecast demand for EC2 instances 

#### Critical Aspects of Predictive Scaling:
1. Load forecasting
2. Scheduled scaling actions -> You can schedule when to add or remove instances to meet scaling policies 
3. Dynamic Scaling fallback -> If actual demand exceeds forecasts, dynamic policies can still trigger additional instances 

You preemptively scale resources to match predicted load. You are ready when demand arrives. 

#### Predictive Scaling is good for:

1. Cyclical traffic -> high resource use during business hours and low use of resources during slower days.
2. Recurring on and off workload patterns -> batch processing, testing or periodic data analysis 
3. Applications that take a long time to initialize, causing a noticeable latency impact on application performance during scale out events.


#### Practice quiz question: Self healing is orchestrated by?
EC2 Auto scaling group 

# Cloud Computing on AWS TIO - 3

Getting familiar with *Launch Templates* and *auto scaling groups (ASG)*. Using elasticity tools and setup an application of high availability

![[Pasted image 20250617201839.png]]

using set up from [TIO 1](https://d6opu47qoi4ee.cloudfront.net/labs/tio/ccaws/ccawstio1.pdf) 

using ami -> ami-06d5e0de6baf595ca



