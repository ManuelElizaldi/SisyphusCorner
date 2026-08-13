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

### Creating Instance
Created an instance, user group (config script), AMI mentioned above, security group that allows traffic from http port 80 and ssh from port 22.

```bash
#!/bin/bash yum update -y yum install httpd -y service httpd start chkconfig httpd on IP_ADDR=$(TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` \ && curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/public-ipv4) echo "ASG instance with IP $IP_ADDR" > /var/www/html/index.html echo "ok" > /var/www/html/health.html
```

### Creating Instance Template 
Important note -> I selected the checkbox Auto Scaling Guidance.

This is the description of the Auto Scaling Guidance button:
```md
Select this if you intend to use this template with EC2 Auto Scaling
```

It provides guidance to best setup the EC2 instance for Auto Scaling 

Selected this AMI:
![[Pasted image 20250618164652.png]]


### Creating an Auto Scaling Group (ASG)
![[Pasted image 20250618165321.png]]

The [[Autoscaling]] group is given a template to use as base to create the additional instances when needed. You have to choose the availability zones as well. We selected all AZs

We attached a load balancer

In health checks I selected 'Turn on Amazon ESB Health Checks' -> The EC2 Auto Scaling group replaces any unhealthy instances

We also turned on Elastic Load Balancing Health checks -> similar to the ESB Health Checks. It determines if instances are ready to receive requests. 

*Health check grace period* -> Instances take some time to initialize, you don't want to terminate an instance that has not started. The grace period is the time the Health Check waits before checking if its ready to receive requests. You usually set this to the time it takes to initialize an instance. Remember that User Data scripts can delay the initialization of an instance. 

##### Configure group size and scaling

You determine your group size -> how many instances the ASG is going to initialize 

Here's where you determine the Auto Scaling policy, there's different metrics that can be used by Cloud Watch to determine if its time to add instances:
![[Pasted image 20250618171741.png]]

After I finished setting the ASG I entered the Load Balancer's DNS into my web browser and I refreshed to visit the different instances:

![[Pasted image 20250618172215.png]]

![[Pasted image 20250618172224.png]]

you can choose the version of the ASG to deploy new versions of an application
### Hands-On: Scaling policy and scheduled action creation

After selecting our ASG, we go into the Automatic Scaling tab and create a new Dynamic Scaling Policy. For this TIO we chose Step Scaling and then created a Cloud Watch Alarm. 

From what I gather, there is multiple Metrics you can set up. You can monitor instances and other services. For this TIO we selected a EC2 instance and by NetworkIn:
![[Pasted image 20250618173522.png]]

For your metric you can choose the conditions, in this case we choose a static threshold -> we use a fixed value and it should be > 

The red line at 5,000,000 marks the threshold we created:
![[Pasted image 20250618174135.png]]

After creating the Cloud Watch alarm, you go back to Create Dynamic Scaling Policy and now you are able to Select a Cloud Watch Alarm:
![[Pasted image 20250618174917.png]]

Here we can see the step scale in action -> there's an increment in instances once said thresholds are crossed. 

You can customize notifications, if it goes from 1 to 10, notify me, then from 5 to 20 notify the boss and then if it goes above 20 notify the CEO... 
 
##### Creating a Scheduled Action:
![[Pasted image 20250618175230.png]]

This feature allows you to create automatic scaling based on predictable loads. Example -> black Friday sale, etc. 


Dynamic scaling -> based on conditions
Scheduled actions -> based on known patterns 

# Launch Templates - On hands video 
From the video where the instructor is walking us through the process of declaring a launch template. 

*Auto Scaling Guidance* -> The check box we selected when creating a template. This button allows the template to start even if we didn't select some mandatory fields. 
- Best practice: **Always select "Auto Scaling guidance"** if your launch template will be used with ASGs.

When a new instance is being created but you forgot or didn't select an AMI intentionally, AWS will tell you to select one. But if the instance is being ran at 3:00 am it would be hard to select one.

So this field "Auto Scaling Guidance" helps us avoid failures to open new instances. 

*Tagging* is important, according to this video, if no appropriate tag is set, AWS will terminate it. 

Only one NIC - *Network interface card*. One IP address per network interface card 

Make sure the right *permissions/roles* are set when creating a template

Also *licensing* is required if you application needs a specific license 

*Configuration Drift* -> when the instances have different settings. 
- This is why you can't change a template once its created. 
	- if you want to modify it, you create a new one. 

We could use templates to start TIO quicker. You can access templates from the 'Launch Instance button'.

#### Practice Quiz Question -> In a launch template certain parameters are mandatory and are validated to ensure services like ASG can use it without errors. 
True, but always select Auto Scaling Guidance 

##### Ask professor about this

# Types of Scaling

| Scaling Type           | Triggered By             | Best For                          |
| ---------------------- | ------------------------ | --------------------------------- |
| **Dynamic Scaling**    | Real-time metrics        | Variable workloads                |
| **Scheduled Scaling**  | Predefined time schedule | Predictable, recurring patterns   |
| **Predictive Scaling** | ML-based predictions     | Automatically anticipating demand |