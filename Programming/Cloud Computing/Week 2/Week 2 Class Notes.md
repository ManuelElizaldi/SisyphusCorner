**Class Notes – Cloud Computing on AWS** **2**

##### Elastic Load Balancer

- Load balancers are an essential component of modern application landscape, providing an efficient way to **distribute network traffic across multiple servers**.
    
    - Load balancers help to ensure **high availability** and **scalability of applications**, allowing websites and services to stay online even if **one server fails** or **experiences high** **load****.**
        
    - Load balancers work by routing incoming requests to the appropriate server and distributing the load among the servers in a way that **maximizes efficiency** and **performance**.
        
- Primary functions of a load balancer are:
    
    - Distribute incoming user traffic or client connections to the **target servers**
        
    - Support **traffic distribution algorithms**
        
    - Support **registration of target servers**
        
    - Be scalable without any single point of failure
        
- Capabilities of AWS Elastic Load Balancer (AWS ELB) are:
    
    - Send traffic to EC2 instances (in multiple AZs) among other target types
        
    - Monitor instance health & route traffic accordingly
        
    - It is elastic, means does not have single point of failure
        
    - Can be Internet facing or internal
        
- Types of AWS ELB are:
    
    - **Application Load Balancer (ALB)**
        
    - **Network Load Balancer (NLB)**
        
    - **Gateway Load Balancer (GLB)**
        
    - For legacy applications or EC2 instances running on classic network (not VPC) the classic load balancer can be used. However, migrating these use cases is recommended to take advantage of the latest features and capabilitites of the ALB, NLB and GLB.
        

  

##### Application Load Balancer

- A load balancer serves as the **single point of contact for clients**. The load balancer distributes incoming application traffic across multiple targets, such as **EC2 instances**, in **multiple Availability Zones**.
    
    - Application load balancer (ALB) operates at Layer 7 of OSI Network model; supports **HTTP**, **HTTPs** traffic.
        
    - **By default**, an Application Load Balancer routes each request independently to a registered target based on the **chosen load-balancing algorithm**.
        
    - However, you can use the **sticky session feature** (also known as **session affinity**) to enable the **load balancer to bind a user's session to a specific target**. This ensures that all requests from the user during the **session are sent to the same target**.
        

  

##### Network Load balancer

- A Network Load Balancer can **handle millions of requests per second**. After the load balancer receives a connection request, it selects a target from the target group for the default rule.
    
    - Network load balancer (NLB) operates at Layer 4 of OSI Network Model; supports **TCP**, **UDP** traffic.
        
    - To increase the **fault tolerance** of your applications, you can enable **multiple Availability Zones for your load balancer** and ensure that each target group has **at least one target in each enabled Availability Zone**.
        
    - ##### Gateway Load balancer
        
- **Gateway load balancer (GLB)** provides a filter between **Internet Gateway** and the **server**.
    
    - Also known as the “Bump in the wire” checking using an appliance designed for network traffic inspection. Once the network packet is deemed safe it is sent to the desired target.
        
    - It maintains **stickiness** of flows **to a specific appliance**.
        
    - It listens for all **IP packets across all ports** and forwards traffic to the target group that's specified in the listener rule.
        
    - The Gateway Load Balancer and its registered virtual appliance instances exchange application traffic using the **GENEVE protocol on port 6081**.
        

  

**Feature and cost analysis**

- Two core areas are -
    
    - The technical team has different levers to configure and fine-tune the load balancer and the associated components to derive the desired outcome in terms of performance, availability, etc.
        
    - The cost dimensions should be well understood to factor in cloud budgeting and forecasting.
        
- **LCU Details**
    
    - **Application Load Balancer**
        
        - You are charged for each hour or partial hour that an Application Load Balancer is running, and the number of **Load Balancer Capacity Units (LCU)** used per hour.
            
    - **Network Load Balancer**
        
        - You are charged for each hour or partial hour that a Network Load Balancer is running, and the number of **Network Load Balancer Capacity Units (NLCU)** used by Network Load Balancer per hour.
            
    - **Gateway Load Balancer**
        
        - You are charged for each hour or partial hour that a Gateway Load Balancer is running, and the number of **Gateway Load Balancer Capacity Units (GLCU)** used by Gateway Load Balancer per hour.
            

  

For more information on **Load Balancer Capacity Units(LCU)** , please refer to the Datasheet.

  

##### Canary release

**Canary release** is a technique to reduce the **risk of introducing a new software version** in production by slowly rolling out the change to a small subset of users **before rolling it out to the entire infrastructure and making it available to everybody**.

- Similar to a BlueGreenDeployment, you start by deploying the new version of your software to a subset of your infrastructure, to which no users are routed
    
- When you are happy with the new version, you can start routing a few selected users to it.
    

  



- There are **different strategies** to choose which users will see the new version: a simple strategy is to use a random sample; some companies choose to release the new version to their internal users and employees before releasing to the world; another more sophisticated approach is to **choose users based on their profile and other demographics**.
    
- Canary release is an application of **ParallelChange**, where the migrate phase lasts until all the users have been routed to the new version. At that point, you can decommission the old infrastructure. If you find any problems with the new version, **the rollback strategy is simply to reroute users back to the old version** until you have fixed the problem.
    
  

##### Use cases and scenario analysis

Multi-staged migration process of a complex business application from on-prem to cloud using cloud IaaS services.

  

**Lift-and-shift cloud adoption strategy** is a great way for businesses to transition their existing IT infrastructure to the cloud quickly and cost-effectively.

- This strategy allows businesses to move existing applications, storage, and databases to the cloud, with minimal changes being necessary.
    
- This approach helps businesses reduce their operational costs, increase scalability, and improve performance.
    
- Additionally, this strategy can be used to quickly test and assess the benefits of cloud computing while reducing the risk associated with any new technology implementations.
    

  

- **Two EC2 instances in a TG with ALB**
    
    - **"Lift and shift" scenario** - the first stage of cloud adoption that leverages existing IT investments such as applications that are currently catering to the business needs
        
    - This will ensure the existing IT assets are migrated over without rocking the boat too much and yet take advantage of cloud resources and maybe shutting down data centers owned by the organization.
        

- Need for session affinity, typical for legacy applications, maintaining user context on a specific server (like an EC2 instance)
    

  

- **Four EC2 instances in two TGs with ALB with path based routing.**
    
    - Business has realized significant cloud benefits; they want to consider deploying the updates in smaller chunks and not necessarily update the existing application.
        
    - They are comfortable with infra as a service. So, the team sets out to create the updated service as a different project and deploys on a different set of ec2 instances, groups them together and calls it orderservice1-tg.
        
    - Using path-based routing of the LB we can now direct specific traffic to this newly deployed service and does not go to the lift/shift app (represented by webapp-tg).
        

![](file:///tmp/lu20072872uyefr.tmp/lu20072872uyemr_tmp_9d3e8322.png)

  

- **Six EC2 instances in three TGs with ALB, path-based routing and traffic distribution**
    
    - The business requires the newly deployed service needs to be updated based on market and customer reaction and feedback.
        
    - The business however is reluctant to release this new feature to all the customers in a big bang approach.
        


- Instead, they want to gradually release it to the customers. So both versions need to serve customer traffic, they want "canary release".
    
- Here TG affinity will be needed to deliver consistent behavior of the application.
    

  

- **Hybrid deployment with central session management, private service & datacenter connectivity**
    
    - To put together, the various capabilities from many services including the situation where an enterprise takes advantage of existing investments which are still hosted in their corporate data center.
        
    - In the Architecture, we have got a public application load balancer with port 80 is open, pathway is routing. They are still experimenting with canary release on order service 1 and 2.
        
    - The existing application was a monolith which had the session management in ec2 instance memory, now they are trying to migrate the application to stateless instead of being stateful.
        


  

  

**Windows EC2 Instance, Instance Pricing**

- **Install an RDP client** and **locate the private key** - Windows includes an RDP client by default.
    
    - Get the fully-qualified path to the location on your computer of the .pem file for the key pair that you specified when you launched the instance.
        
- **Enable inbound RDP traffic from your IP address to your instance** - Ensure that the security group associated with your instance allows incoming RDP traffic (port 3389) from your IP address.
    

  

- **Connect to your Windows instance using RDP**
    
    - To connect to a Windows instance, you must retrieve the initial **administrator password** and then enter this password when you connect to your instance using Remote Desktop.
        
    - The name of the administrator account depends on the language of the operating system.
        
    - It converts the **pem file to windows password** using which we can login to windows server via **RDP access**.
        
- Reserved instances with discount cost - upto 75% compared to on-demand
    
- Spot instances 90% discount
    
- Dedicated instance cost more than the on-demand instances
    

  

##### Identity & Access Management

**AWS Identity and Access Management (IAM)** is a web service that helps you securely control access to AWS resources.

- With IAM, you can centrally manage permissions **that control which AWS resources users can access**. You use **IAM to control who is authenticated (signed in)** and **authorized (has permissions) to use resources**.
    
- When you create an AWS account, you begin with **one sign-in identity** that has complete access to all AWS services and resources in the account. This identity is called the **AWS account root user** and is accessed by signing in with the email address and password that you used to create the account. It is recommended that you don't use the root user for your everyday tasks.
    
- AWS roles can be **assigned to an EC2 instance**, allowing access to the applications deployed on the instance to other AWS services.
    
- An **IAM role** is a great way to ensure no access keys or secrets are embedded in the application code or configuration files. Such embedded key/secret can reduce the overall security posture of the deployment.
    
- **A policy** is an object in AWS that, when associated with an identity or resource, defines their permissions. AWS evaluates these policies when a principal uses an IAM entity (user or role) to make a request.
    
- **Permissions** in the policies determine whether the request is allowed or denied.
    
- Most policies are stored in AWS as **JSON** documents. **Policy is a JSON** - which defines the access to a particular resource. Hence, policy allows and restricts access for a user/service to whomever the IAM is assigned to.
    
- Policy generator can be used to create policy(JSON)
    
- Set of policies makes up a ‘**Role**’ and is assigned to **a user or service(EC2)** created inside the AWS account to whom we can assign the roles.
    

  

**AWS pricing calculator**

**AWS Pricing Calculator** is a web-based planning tool that you can use to create estimates for your AWS use cases.

- You can use it to model your solutions before building them, explore the AWS service price points, and review the calculations behind your estimates.
    
- You can use it to help you plan how you spend, find cost saving opportunities, and make informed decisions when using Amazon Web Services.
    
- With AWS Pricing Calculator, you can do the following tasks:
    
    - **View transparent prices** – See the calculations behind the estimated prices for your service configurations. You can view price estimates by service or by groups of services to analyze your architecture costs.
        
    - **Use groups for hierarchical estimates** – Sort your estimates into groups to align with your architecture for clear service cost analysis.
        
    - **Share your estimates** – Save the link to each estimate to share or revisit at a later time. Estimates are saved to the AWS public servers.
        
    - **Export your estimates** – Export your estimates in CSV or PDF format to share locally with your stakeholders.
        

  

**References**

1. Datasheet -[https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_EC2_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_EC2_Datasheet.pdf)
    
2. AWS Documentation - [https://docs.aws.amazon.com/ec2/](https://docs.aws.amazon.com/ec2/)