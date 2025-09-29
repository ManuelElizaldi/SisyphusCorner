            **Class Notes – Cloud Computing on AWS 1**

IaaS, Degree of abstraction

- **Infrastructure as a Service (IaaS)** is a type of cloud computing service that provides businesses with access to **computing infrastructure** such as servers, storage, and networking services. 

- This type of service delivers these resources on-demand and can be scaled up or down as needed. 
- With IaaS, businesses can quickly and easily deploy applications, manage and store data, and create virtual networks without having to purchase and maintain their own hardware. 
- IaaS is a cost-effective and convenient way for businesses to access the computing power they need without having to invest in expensive hardware and software.

  

- **Things you will need to deploy a simple web application** - An Instance which has a CPU, RAM or memory, a disk which will carry an operating system with the application. Instances can have additional disks to store application data. 

- To set the entire application up and to communicate out on the internet, you will need to configure the networking, security groups for the instance and set up the application.
- Once you start the application it becomes live and that's what it takes for you to set up a simple web application environment.

  

Core building blocks of AWS

- **Compute** which are CPU and RAM, in AWS parlance **EC2 (Elastic Compute Cloud)**. **Compute services** are also known as **Infrastructure-as-a-Service (IaaS)**. A generic term used to reference processing power, memory, networking, storage, and other resources required for the computation.

  

- To store our data -  **Storage**, different forms of data storage available in AWS
- With the help of **networking** , applications go out to the Internet and communicate with each other
- For high availability use multiple regions and availability zones.

  

Types of Instances

- **Spot Instances** are unpredictable. You bid and get them but as the price rises and crosses your limit, they will be reclaimed.

- A Spot Instance is an instance that uses spare or excess EC2 capacity that is available in an AZ for less than the On-Demand price. 
- Because Spot Instances enable you to request unused EC2 instances at steep discounts, you can lower your Amazon EC2 costs significantly. 

- **On demand instances** have a fixed price. 

- On-Demand Instances – Pay, by the second, for the instances that you launch.

- **Reserved instances** are significantly cheaper but the number of instances and the period for

which they are taken remains unaltered.

- **Reserved Instances** – Reduce your Amazon EC2 costs by making a commitment to a consistent instance configuration, including instance type and Region, for a term of 1 or 3 years.

- **Dedicated Instances** are EC2 instances that run on hardware that's dedicated to a single customer. 

  

AWS Global infrastructure (Regions and Zones)

- **Global cloud infrastructure** refers to the physical computing and networking resources that deliver cloud services around the world. 

- A cloud provider’s global infrastructure is made up of **data centers**, which are interconnected by a high-speed, reliable global network. 
- These data centers are connected to different ISPs and carriers, allowing them to not only deliver the best performance but also provide the **highest levels of redundancy** and **availability**. 
- The global infrastructure of a cloud provider provides customers with reliable and secure cloud services, no matter where they are located.

  

- The AWS Cloud infrastructure is built around **AWS Regions** and **Availability Zones**. According to Amazon -"AWS has the concept of a **Region**, which is a physical location around the world where we cluster data centers."

- **Availability Zone (AZ)** is one or more discreet data centers with redundant power networking and connectivity in an AWS region.
- These Availability Zones offer you the ability to operate production applications and databases that are more **highly available**, **fault tolerant**, and **scalable** than would be possible from a single data center.
- **AWS Local Zones** & **Wavelength Zones** (for telecommunication workloads) are other options for providing low-latency applications.

  

**Note** - **Regions** can be a country, state or even a city. **Multiple Availability Zones (AZ)** make up a region.

**Local zones** are similar to AZ but deployed in close proximity to a specific location. **Wavelength zones** are specifically designed for **telecommunication** workloads. It is possible other kinds of zones may emerge in the future. A zone's core principle is to be able to deploy applications for specific requirements.

  

Understanding the Real cloud

The cloud represents a set of data centers offering computing and other services. As a customer (Non-technical and Technical), there must be a simple way to access these services. Various options to interact with / use cloud services are:

- Management Console

- Cloud provider specific
- Easy to use UI
- Non technical audience
- Changes frequently

- Software Development Kits (SDKs)

- Cloud provider specific
- Relatively stable
- Good for automation
- Multiple programming languages
- Develop applications
- Complex biz & ops processes
- Deploy apps on cloud or customer DC
- Requires technical knowledge

- Command Line Interface (CLI)

- Cloud provider specific
- Relatively stable
- Good for automation & scripts
- Deploy on cloud or customer DC
- Requires technical knowledge

- 3rd Party tools & applications - which are generally a layer over cloud providers.

- Cloud provider agnostic
- Characteristics may vary

- SDKs and CLI layer.

  

EC2 core features

- **Amazon Elastic Compute Cloud (Amazon EC2)** provides scalable computing capacity in the Amazon Web Services (AWS) Cloud. 

- EC2 is also called **Virtual Machines(VM)** or **Virtual Servers**. These VMs can be launched using tools such as the management console or programmatically using the CLI/SDKs. 
- EC2 is a resource that is in a **specific AZ** within a Region.
- It is a Virtual Machine running the operating system along with your application.
- It connects to a virtual cloud network using a **virtual network interface**.
- It has storage to hold the application data.
- EC2 is the **bedrock of the AWS** cloud and has many features/attributes.

The core set of attributes are: 

- **Name and Tags** - label assigned to the instance.

- Helps in grouping instances by purpose, owner etc.
- Name is a special key that can be used to search for a resource with a specific tag.

- **Application and OS Images (AMI)** - Select the specific OS by selecting the AMI like Linux flavors, windows etc. “**OS + Application**” combination is available by AWS or 3rd party or created by the customer.
- **Instance Types** -  Determines the hardware of the host computer. AWS provides a wide selection of instance types optimized to fit different use cases. 

- Instance types comprise varying combinations of CPU, memory, storage, and networking capacity and give you the flexibility to choose the appropriate mix of resources for your applications.

- **Key pair** - Private key (for Linux instances) to login (secure shell) to the instance. The key is generated when creating the "Key pair".

- Also known as the PEM file (typical for Linux instances)
- You can proceed without creating the PEM file if you want to use EC2 instance connect (not recommended for production environments).

- **Network** - ENI (Elastic network Interface) is the Virtual network card

- ENI attaches the Instance to the VPC, also known as “Network Interface”

- **Security** -  Security group (SG) attached to an ENI to open specific ports

- Controls inbound and outbound traffic from the instance

- **Configure storage, EBS Volume (Disk)**- like the hard disks of the laptop. You can choose the storage you want to attach to your EC2 instance
- **Advanced details** - This can be used to provide user data among other options designed to cater to specific customer needs.

  

Workflow for launching an EC2 instance

1. **Name and tags** - Enter a name under **Name**  for your ec2 instance.
2. **Application and OS Images (Amazon Machine Image)** - Choose an AMI from Quickstart or Recents. Quickstart will have many options from which you can choose the OS flavor.
3. **Instance type** - Choose the instance size which fits your use case from CPU intense /memory/ intense etc. Eg T is general purpose
4. **Key pair -**  You can proceed with or without a key pair. Use an SSH client if proceeding with a Key pair. You can use the EC2 Connect if you are proceeding without the key pair.
5. **Network Settings** - Create a Security group or choose an existing security group. Ports to be available and open. IP restrictions for accessing.
6. **Configure Storage** -  Choose the volume which fits your use case.
7. **Summary** - Specify how many instances need to be launched and **review** the configurations. You can use the EC2 instance connect or an SSH client to login to the server.
8. **Check your instance status** - After you launch an instance, it can take a few minutes for the instance to be ready so that you can connect to it. Check that your instance has passed its status checks. 
9. **Get the public DNS name and user name to connect to your instance** - To find the public DNS name or IP address of your instance and the user name that you should use to connect to your instance
10. **Locate the private key and set the permissions** - Get the fully-qualified path to the location on your computer of the .pem file for the key pair that you specified when you launched the instance.
11. **Install an SSH client on your local computer as needed** - Your local computer might have an SSH client installed by default. You can verify this by typing ssh at the command line. 

12. **Connect to your instance using SSH** - In a terminal window, use the **ssh** command to connect to the instance. You specify the path and file name of the private key (.pem), the username for your instance, and the public DNS name or IPv6 address for your instance.
13. **EC2 Instance Connect** can be used if you don't have a key pair.

  

**Note1**:  ‘**Stop**’ just removes the CPU & memory, disk and storage will remain. ‘**Terminate**’ removes everything. Instances (CPU and Memory) are not charged when they are stopped or terminated.

  

**Note2**:  With time, user interfaces are updated and based on customer feedback, functionality is also reorganized. However, the core principles of a VM/EC2 remain the same. It is essential to focus on the core principles of a cloud service.

  

**Note3**: Various ports can be opened that allow traffic to/from the EC2 instance. 

  

  
----
**References** 

1. Datasheet -[https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_EC2_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_EC2_Datasheet.pdf)
2. AWS Documentation - [https://docs.aws.amazon.com/ec2/](https://docs.aws.amazon.com/ec2/)