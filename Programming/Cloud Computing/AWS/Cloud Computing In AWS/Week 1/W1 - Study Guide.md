# Cloud Computing Services: AWS Fundamentals Study Guide

## I. Quiz (Short Answer)

Answer each question in 2-3 sentences.

1. Explain the primary insight Amazon had that led to the creation of AWS.
2. Describe the initial risk associated with running an e-commerce website on a single EC2 instance, and how this risk can be mitigated.
3. What is the purpose of an Elastic Load Balancer (ELB) in a cloud architecture, and how does it improve user experience?
4. Define an AWS Availability Zone (AZ) and explain its importance in achieving fault tolerance.
5. How do AWS Local Zones and Wavelength Zones differ from standard Availability Zones in their primary purpose?
6. Identify the "real cloud" according to the source material, and name two common methods developers use to interact with it.
7. What is an Amazon Machine Image (AMI), and what essential component does it provide for launching an EC2 instance?
8. Explain the concept of a Security Group in AWS EC2 and what types of traffic it controls.
9. In the context of EC2 instances, differentiate between the "stopped" state and the "terminated" state regarding AWS billing.
10. What is Robotic Process Automation (RPA), and how does its integration with Generative AI (GenAI) enhance its capabilities?

## II. Answer Key (Quiz)

1. Amazon's primary insight was realizing that their internal struggles with scaling and building resilient infrastructure for their e-commerce business were likely shared by other companies. This led them to conclude that they could offer their robust infrastructure as a service to others, which ultimately became AWS.
2. The initial risk of running an e-commerce website on a single EC2 instance is using it for storage, as instances are isolated and cannot share files. This risk can be mitigated by offloading the database to a separate RDS instance and unstructured data like images to an S3 bucket, creating a more resilient and flexible system.
3. An Elastic Load Balancer (ELB) is attached to a network to effectively distribute incoming user traffic across multiple EC2 instances. This ensures that no single instance becomes overloaded, thereby increasing the system's elasticity and improving overall user experience by maintaining performance.
4. An AWS Availability Zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity within an AWS Region. They are isolated from each other by significant distances (e.g., 100km) to provide fault tolerance, meaning an outage in one AZ will not impact others.
5. AWS Local Zones place compute, storage, and other services close to large populations or industries to achieve single-digit latency for general applications. Wavelength Zones, conversely, embed AWS services within 5G networks, specifically designed for telecommunication workloads requiring extremely low latency edge computing.
6. According to the source, the "real cloud" is the API layer, which acts as the interface to the various services within an Availability Zone. Developers commonly interact with this layer using Software Development Kits (SDKs) and the Command Line Interface (CLI).
7. An Amazon Machine Image (AMI) is a template for virtual machines in Amazon's EC2, containing all the information needed to launch an instance. At a minimum, it provides the operating system for the virtual machine.
8. A Security Group in AWS EC2 acts as a virtual firewall that controls incoming (inbound) and outgoing (outbound) traffic for an EC2 instance. It defines rules based on protocol, port, and source/destination to allow or deny specific network access.
9. When an EC2 instance is in a "stopped" state, you are not charged for the compute (CPU and memory) but are still charged for any attached storage (disk). In a "terminated" state, all resources associated with the instance, including compute and storage, are removed, and you are no longer charged.
10. Robotic Process Automation (RPA) uses bots to automate repetitive, rule-based tasks by mimicking human interactions with software interfaces. Its integration with Generative AI (GenAI) enhances its capabilities by allowing RPA bots to process unstructured data, understand context, and make more intelligent, adaptive decisions beyond simple rule-based operations.

## III. Essay Format Questions

1. Discuss the evolution of AWS from Amazon's internal needs to a public cloud computing service. How did Amazon's original business model and challenges influence the design principles of AWS, particularly concerning scalability and resilience?
2. Compare and contrast Infrastructure as a Service (IaaS) with higher levels of abstraction (though not explicitly covered in detail, infer from IaaS definition). Explain why EC2 is considered the "bedrock" of AWS IaaS and detail the essential components (CPU, RAM, Disk, OS, Networking, Application Configuration) required to deploy a simple web application using EC2.
3. Analyze the security and networking features available in AWS (VPC, Security Groups, ELB, Route 53, CloudFront). Explain how these services work together to create a secure, highly available, and performant web application architecture.
4. Evaluate the benefits and drawbacks of Robotic Process Automation (RPA) in an organizational context. Furthermore, explain how the combination of RPA, cloud environments, and Generative AI creates a more advanced and intelligent automation ecosystem, addressing some of RPA's traditional limitations.
5. Discuss the transition from AWS Management Console-based infrastructure management to Infrastructure as Code (IaC). Highlight the challenges organizations face during this migration (e.g., resource interdependencies, state management, specialized resource types) and explain the operational benefits (e.g., governance, disaster recovery, cost management) of adopting an IaC approach.

## IV. Glossary of Key Terms

- **Amazon Web Services (AWS):** A comprehensive, broadly adopted, and rapidly evolving cloud platform provided by Amazon.
- **EC2 (Elastic Compute Cloud):** A web service that provides resizable compute capacity in the cloud, essentially virtual servers or instances. It is the "bedrock" of AWS IaaS.
- **S3 (Simple Storage Service):** An object storage service offering industry-leading scalability, data availability, security, and performance. Used for unstructured data like images and videos.
- **SQS (Simple Queue Service):** A fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications.
- **RDS (Relational Database Service):** A managed relational database service that makes it easy to set up, operate, and scale a relational database in the cloud.
- **IaaS (Infrastructure as a Service):** A type of cloud computing service that provides fundamental computing infrastructure resources like virtual machines, storage, and networks on demand.
- **On-Prem (On-Premise):** Refers to software and technology infrastructure that is physically located and managed within an organization's own facilities.
- **Elasticity:** The ability of a system to grow and shrink resources dynamically to adapt to workload changes.
- **Resilient Systems:** Systems designed to withstand failures and recover quickly, maintaining availability even when components fail.
- **VPC (Virtual Private Cloud):** A logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define.
- **ELB (Elastic Load Balancer):** A service that automatically distributes incoming application traffic across multiple targets, such as EC2 instances.
- **Autoscaling:** A feature that automatically adjusts the number of compute resources in a group based on demand or predefined schedules.
- **DNS (Domain Name System):** A hierarchical and decentralized naming system for computers, services, or other resources connected to the Internet or a private network, translating domain names into IP addresses.
- **Route 53:** A highly available and scalable cloud Domain Name System (DNS) web service provided by AWS.
- **CloudFront:** A fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency.
- **Availability Zone (AZ):** One or more discrete data centers within an AWS Region, designed to be isolated from failures in other AZs and providing redundant power, networking, and connectivity.
- **Region (AWS Region):** A physical location around the world where AWS clusters data centers, made up of multiple Availability Zones.
- **Local Zones:** A type of AWS infrastructure that extends an AWS Region into a specific geographic area, placing compute, storage, database, and other select services closer to end-users for single-digit millisecond latency.
- **Wavelength Zones:** AWS infrastructure deployments that embed AWS compute and storage services within 5G networks, enabling mobile edge computing applications with ultra-low latency.
- **Edge Computing:** A distributed computing paradigm that brings computation and data storage closer to the sources of data, reducing latency and bandwidth usage.
- **API Layer:** The interface through which customers and programs interact with and build upon AWS services; often referred to as "the real cloud."
- **Management Console:** A web-based interface provided by AWS for managing cloud resources and services.
- **SDKs (Software Development Kits):** Toolkits comprising libraries, documentation, and tools that allow developers to interact with AWS services using various programming languages.
- **CLI (Command Line Interface):** A text-based interface used to interact with AWS services and manage resources programmatically.
- **Instance Type:** Determines the hardware configuration (CPU, memory, storage, networking capacity) of an EC2 instance, optimized for different use cases.
- **AMI (Amazon Machine Image):** A template containing the software configuration (operating system, application server, and applications) required to launch an EC2 instance.
- **EBS (Elastic Block Storage):** A high-performance block storage service designed for use with Amazon EC2 for both throughput and transaction-intensive workloads. It acts like a virtual hard disk.
- **Subnet:** A logical subdivision of an IP network, typically within a VPC, associated with a specific Availability Zone.
- **ENI (Elastic Network Interface):** A virtual network card that provides network connectivity for an EC2 instance within a VPC.
- **Security Group:** A virtual firewall for your EC2 instances that controls inbound and outbound traffic.
- **PEM file:** A file format (Privacy Enhanced Mail) used for storing cryptographic keys and certificates, commonly used for secure shell (SSH) access to Linux EC2 instances.
- **SSH (Secure Shell):** A cryptographic network protocol for secure data communication, remote command-line login, remote command execution, and other secure network services between two networked computers.
- **Robotic Process Automation (RPA):** The use of software bots to automate repetitive, rule-based tasks by mimicking human interactions with software interfaces.
- **Generative AI (GenAI):** A type of artificial intelligence that can create new content, such as text, images, or code, and can process unstructured data, understand context, and make intelligent decisions.
- **Infrastructure as Code (IaC):** The practice of managing and provisioning computing infrastructure through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.
- **Configuration Drift:** Inconsistencies that arise when infrastructure environments are manually changed, leading to deviations from the desired state defined in code or templates.
- **AWS CloudFormation:** An AWS service that helps you model and set up your AWS resources, managing them as infrastructure as code.
- **AWS CDK (Cloud Development Kit):** An open-source software development framework to define your cloud application resources using familiar programming languages.
- **Dedicated Host:** An EC2 instance deployment option that provides physical servers dedicated for your use, ensuring that your instances run on hardware solely for your account.
- **Session Affinity (Sticky Sessions):** A feature of load balancers that ensures all requests from a particular user during a session are sent to the same target server, useful for applications that maintain state information.
- **Canary Release:** A deployment strategy where a new version of an application is gradually rolled out to a small subset of users before being deployed to the entire user base, allowing for easy rollback if issues arise.


--- 
#### Source
Notebook LM

