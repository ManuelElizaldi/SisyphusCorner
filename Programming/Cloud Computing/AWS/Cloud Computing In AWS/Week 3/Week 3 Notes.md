**Class Notes – Cloud Computing on AWS** **3**

**Auto scaling group**

- An Auto Scaling group starts by launching enough instances to meet its **desired capacity**. It maintains this number of instances by performing **periodic health checks** on the instances in the group.
    
    - The Auto Scaling group continues to maintain a **fixed number of instances** even if an instance becomes unhealthy.
        
    - If an instance becomes **unhealthy**, the group terminates the unhealthy instance and launches another instance to replace it.
        
    - An Auto Scaling group can launch On-Demand Instances, Spot Instances, or both. You can specify multiple purchase options for your Auto Scaling group only when you use a launch template.
        
    - An ASG can be associated with a **target group (TG)** so that the desired number of instances are maintained in that group.
        

  

- The following steps describe how to create the Auto Scaling group:
    
    - Specify the launch template for launching the instances.
        
    - Choose the VPC and subnets to launch your Auto Scaling group in.
        
    - Choose the option to override the existing instance type requirements of the launch template with new requirements.
        
    - Manually choose and prioritize your instance types. For example, you might choose to prioritize instance types that can benefit from Savings Plan or Reserved Instance discount pricing for On-Demand Instances.
        
    - Specify the percentages of On-Demand Instances and Spot Instances to launch.
        
    - Choose allocation strategies that determine how Amazon EC2 Auto Scaling fulfills your On-Demand and Spot capacities from the possible instance types.
        
    - Specify your group size, including your desired capacity, minimum capacity, and maximum capacity.
        

  

- Auto Scaling groups with multiple instance types and purchase options
    
    - **Spot Instances**
        

Amazon EC2 Auto Scaling provides two types of allocation strategies that can be used for Spot Instances:

- **Capacity-optimized** - Amazon EC2 Auto Scaling allocates your instances from the Spot Instance pool with **optimal capacity for the number of instances** that are launching. Deploying in this way helps you make the most efficient use of spare
    
- **EC2 capacity** - With Spot Instances, the pricing changes slowly over time based on long-term trends in **supply and demand**, but capacity fluctuates in real time.
    
    - The **capacity-optimized strategy** automatically launches **Spot Instances** into the **most available pools** by looking at **real-time capacity** data and predicting which are the most available.
        
    - This works well for workloads such as big data and analytics, image and media rendering, and machine learning. It also works well for high performance computing that may have a higher cost of interruption associated with restarting work and checkpointing.
        
    - By offering the possibility of fewer interruptions, the capacity- optimized strategy can lower the overall cost of your workload.
        
- **Lowest-price** - Amazon EC2 Auto Scaling allocates your instances from the **number (N) of Spot Instance pools** that you specify and from the pools with the **lowest price per unit** at the time of fulfillment.
    

For example, if you specify **4 instance types and 4 Availability Zones**, your Auto Scaling group can potentially draw from as many as 16 different Spot Instance pools. If you specify 2 Spot pools (N=2) for the allocation strategy, your Auto Scaling group can fulfill Spot capacity from a minimum of 8 different Spot pools where the price per unit is the lowest.

  

- **On-Demand Instances** - The allocation strategy for On-Demand Instances is **prioritized**. Amazon EC2 Auto Scaling uses the **order of instance types** in the list of launch template overrides to determine which instance type to use first when fulfilling On-Demand capacity.
    

For example, let's say that you specified three launch template overrides in the following order: **c5.jarge**, **c4. large**, and **c3. large**. When your On-Demand Instances are launched, the Auto Scaling group fulfills On-Demand capacity by starting with **e5. large**, then **c4. large**, and then **c3.large**.

  

![](file:///tmp/lu759525408kdr.tmp/lu759525408kjb_tmp_a6e5e879.png)

  

- You can use **scaling policies** to **increase or decrease the number of instances** in your group dynamically to meet changing conditions. When the scaling policy is in effect, the Auto Scaling group adjusts the **desired capacity of the group**, between the **minimum and maximum capacity values** that you specify, and launches or terminates the instances as needed.
    

  

- For example, the following Auto Scaling group has a **minimum size of one instance**, a **desired capacity of two instances**, and a **maximum size of four instances**. The scaling policies that you define adjust the number of instances, within your minimum and maximum number of instances, **based on the criteria** that you specify.
    

![](file:///tmp/lu759525408kdr.tmp/lu759525408kjb_tmp_7c9d7e15.png)

- Desired Capacity will be greater than or equal to minimum size, and cannot be less than minimum size.
    
- Maximum size is an artificial upper limit.
    
- **Observation window** - An observation window **allows users to view the current status of the application**, including the amount of memory being used, CPU utilization, rate of data transfer, number of instances being used and other parameters.
    
    - The observation window also **allows administrators to view the history of the application's performance** such as the number of errors encountered. This helps users identify performance bottlenecks and plan for future performance optimization.
        
    - The duration should be selected such that it factors in the usage patterns the application is likely to experience in production.
        

  

- **Minimum utilization economics** -
    
    - Minimum instances can be arrived only after the observation window.
        
    - During this time we need to simulate all the workload patterns in actual or scaled down if the actual workload numbers are high (eg popular holiday season sale, hard to simulate actual millions of users!)
        
    - It is possible the utilization can hit zero but that does not mean we should not go for reserving instances (RI) and favor only dynamic instances (DI). It is because it may make economical sense to go for RI if the zero utilization time is less than a specific threshold.
        

  

Eg - Assume “x” hours of observation window, and the time of zero utilization is “z” hours

- then it will still make commercial sense to go for RI if (x) times (cost of RI) < (x-z) times (cost of DI)
    

- Cloud providers have different nomenclature for pricing models that allow customers to reduce the costs by giving the cloud provider a long term commitment
    

  

- **Little's Law** - Implement **loosely coupled dependencies**: Dependencies such as queuing systems, streaming systems, workflows, and load balancers are loosely coupled. Loose coupling helps isolate behavior of a component from other components that depend on it, increasing resiliency and agility.
    

![](file:///tmp/lu759525408kdr.tmp/lu759525408kjb_tmp_96d1cc1d.png)

- “Observe your infrastructure” - CloudWatch Logs can be enabled for Load Balancers. Little’s Law helps calculate how many instances of compute (EC2 instances) that you need.
    

L = λW

L = number of instances (or mean concurrency in the system)

λ = mean rate at which requests arrive (req/sec)

W = mean time that each request spends in the system (sec)

  

For example, at 100 rps, if each request takes 0.5 seconds to process, you will need 50 instances to keep up with demand.

  

An ASG can have **multiple scaling triggers**. This provides the flexibility to ensure the application deployment is **elastic** under various load conditions. For predictable workloads, you can also scale on a schedule.According to AWS the following are the scaling options:

  

- **Maintain current instance levels at all times**: You can configure your Auto Scaling group to maintain a **specified number of running instances at all times**. To maintain the current instance levels, EC2 Auto Scaling performs a **periodic health check** on running instances within an Auto Scaling group. When EC2 Auto Scaling finds an **unhealthy instance**, it terminates that instance and launches a new one.
    
- **Scale manually**: Manual scaling is the most basic way to **scale your resources**, where you specify only the change in the **maximum**, **minimum**, or **desired capacity** of your Auto Scaling group. EC2 Auto Scaling manages the process of creating or terminating instances to maintain the updated capacity.
    
- **Scale based on a schedule**: Scaling by schedule means that **scaling actions are performed automatically as a function of time and date**. This is useful when you know exactly when to increase or decrease the number of instances in your group, simply because the need arises on a **predictable schedule**.
    
- **Scale based on demand**: A more advanced way to scale your resources, **using dynamic scaling**, lets you define a scaling policy that dynamically resizes your Auto Scaling group to meet changes in demand. This method is useful for **scaling in response to changing conditions**, when you don't know when those conditions will change. You can set up EC2 Auto Scaling to respond for you.
    
- **Use predictive scaling**: You can also combine **predictive scaling and dynamic scaling** (proactive and reactive approaches, respectively) to scale your EC2 capacity faster. Use predictive scaling to **increase the number of EC2 instances** in your Auto Scaling group in advance of daily and weekly **patterns in traffic flows**.
    

  

  

**Self healing**

- Self-healing deployments have the capability to **automatically detect** and **repair any errors and failures that occur**. This type of deployment can detect and fix problems without any manual intervention, reducing downtime, and ensuring continuity of service.
    
- Self-healing deployments are becoming increasingly popular as they provide increased **reliability**, **scalability**, and **cost-effectiveness**.
    

  

  

**Amazon Machine Image(AMI)**

An Amazon Machine Image (AMI) is a pre-configured template used to **create a virtual server in AWS**. It is used to **launch an EC2 instance**.

- An AMI contains the information necessary to launch an EC2 instance, such as an **operating system**, **application server**, and **application code**.
    
- An AMI can also include scripts that are used to configure the instance when it launches. AMIs provide a convenient way to quickly launch an EC2 instance with a pre-configured application stack. It has the operating system at the **minimum**.
    
- An Amazon Machine Image (AMI) is a supported and maintained image provided by AWS that provides the information required to launch an instance.
    
- You must specify an AMI when you launch an instance.
    
- You can launch **multiple instances from a single AMI when you require multiple instances with the same configuration**.
    
- You can use **different AMIs to launch instances when you require instances with different configurations**.
    
- Customers can create **custom AMIs** depending on their needs
    
- AMI is an effective tool for **lifting an on-prem application and migrating to the cloud**.
    

  

**AWS Command Line Interface**

The AWS Command Line Interface (AWS CLI) is an **open-source** tool that enables you to interact with **AWS services** using commands in your command-line shell.

- The CLI is a convenient tool for operations engineers to write cloud automation scripts for repetitive activities.
    
- It can be installed on cloud servers and machines hosted in the customer's data centres.
    

For example, a customer may use a CLI script to create a testing environment for the developers to test their applications.

- The AWS Command Line Interface (AWS CLI) is a **unified tool to manage your AWS services**.
    
- With CLI, you can control **multiple AWS services from the command line and automate them through scripts**.
    
- For non-technical roles, it is essential to know the nature of the work the engineers will perform using the CLI. This is needed because automation will reduce time to market and will eliminate human errors in addition to being repeatable.
    
- Few commands for reference
    
    - **Describe-instance-attribute** - Describes the specified attribute of the specified instance.
        
    - **Describe-instance-connect-endpoints** - Describes the specified EC2 Instance Connect Endpoints or all EC2 Instance Connect Endpoints.
        
    - **Describe-instance-credit-specifications** - Describes the credit option for CPU usage of the specified burstable performance instances. The credit options are standard and unlimited .
        
    - **Describe-instance-types** - Describes the details of the instance types that are offered in a location. The results can be filtered by the attributes of the instance types.
        
    - **Describe-instances** - Describes the specified instances or all instances.
        

  

  

**References** –

1. Datasheet - [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_EC2_Auto_Scaling_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_EC2_Auto_Scaling_Datasheet.pdf)
    
2. AWS Documentation - [https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html](https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html)