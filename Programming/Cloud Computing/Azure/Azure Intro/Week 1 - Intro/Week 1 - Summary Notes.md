  

**Microsoft Azure -1**

  

**What is Cloud Computing-**

Cloud computing is the on-demand availability of computer system resources, especially data storage (cloud storage) and computing power, without direct active management by the user on a pay-per-use basis.

  

**Types of cloud models-**

1. Public Cloud
    

- It is defined as computing services offered by third-party providers over the public Internet, making them available to anyone who wants to use or purchase them.
    
- They may be free or sold on-demand, allowing customers to pay only per usage for the CPU cycles, storage, or bandwidth they consume.
    
- It can save companies from the expensive costs of having to purchase, manage, and maintain on-premises hardware and application infrastructure
    
- It can also be deployed faster than on-premises infrastructures and with an almost infinitely scalable platform.
    

2. Private Cloud
    

- It is defined as computing services offered either over the Internet or a private internal network and only to select users instead of the general public.
    
- Also called an internal or corporate cloud.
    
- Private cloud computing gives businesses many of the benefits of a public cloud (including self-service, scalability, and elasticity) with the additional control and customization available from dedicated resources over a computing infrastructure hosted on-premises.
    
- It delivers a higher level of security and privacy through both company firewalls and internal hosting to ensure operations and sensitive data are not accessible to third-party providers.
    
- The Drawback is that the company’s IT department is held responsible for the cost and accountability of managing the private cloud. So private clouds require the same staffing, management, and maintenance expenses as traditional data center ownership.
    

3. Hybrid Cloud
    

- It is a computing environment that combines an on-premises data center (also called a private cloud) with a public cloud, allowing data and applications to be shared between them.
    
- Higher flexibility to choose where to deploy the resources
    
- Higher control on resources and data
    

  

**Delivery Models-**

![[Pasted image 20250929180629.png]]

- On-Premises
    
    - Users need to manage everything here.
        
    - Users will have full control over the complete infrastructure and have their own data centers and only the users will be responsible for the same.
        
- Infrastructure as a Service (IaaS)
    
    - IaaS gives you a server in the cloud (virtual machine) that you can control completely. With an Azure VM, you are responsible for managing everything from the operating system up to the applications you are running.
        
    - This model is like on-premises virtual machines. It is like connecting to remote servers to manage them instead of physically accessing them. Another example of Azure IaaS is Azure Kubernetes Service (AKS), which is a container orchestration service.
        
    - With this solution, you can easily migrate applications to Azure and deploy and manage Microservices-based applications and IoT devices. If you need a solution that requires multiple applications running on a single machine or custom third-party software, then IaaS might be for you.
        
- Platform as a Service (PaaS)
    
    - PaaS provides a complete cloud framework for development and deployment. Choosing a PaaS solution gives the power to develop simple to complex cloud-based apps.
        
    - It also provides the ability to analyze data and find insights to enhance business decisions. Common examples of Azure PaaS services include Azure Search, App Services, and Azure CDN.
        
    - With Azure PaaS, you are responsible for managing your applications alone. The cloud service provider would manage the development tools, databased management systems, business analytics, middleware, servers and storage, and networking firewalls.
        
    - This model helps you to eliminate the IT costs of software licenses, development tools, and application infrastructure. If you want to create applications using built-in software components with less coding, then PaaS would be the right solution.
        
- Software as a Service (SaaS)
    
    - SaaS provides a complete software solution where you can rent apps for your organization. All the underlying infrastructure, app software, middleware, and app data are in the data center.
        
    - The service provider manages the hardware and software under a service agreement. This always ensures the availability of the app and the security of your data as well. SaaS allows your organization to quickly get things running with apps at minimal upfront cost.
        
    - The advantage of SaaS is no code involved, no deployment hassles, and minimal configuration. Most SaaS applications today are built on a cloud platform due to the low cost of entry and the ability to scale up as your customer base grows. A good example of Azure SaaS model is Azure IoT solution accelerators.
        
    - Here you can leverage ready-to-use templates and customizable solutions for common IoT scenarios. Also, if you want to rent productivity apps and apps like ERP and CRM, then you should choose the SaaS model.
        

  

**Azure Regions and Availability zones**

- The cloud infrastructure is built around Regions and Availability Zones.
    
- Regions are the places that are physical locations around the world where we cluster data centers.
    
- Many Azure regions provide availability zones, which are separated groups of data centers within a region.
    
- Availability zones are close enough to have low-latency connections to other availability zones. They're connected by a high-performance network with a round-trip latency of less than 2ms. However, availability zones are far enough apart to reduce the likelihood that more than one will be affected by local outages or weather.
    
- Availability zones have independent power, cooling, and networking infrastructure. They're designed so that if one zone experiences an outage, then regional services, capacity, and high availability are supported by the remaining zones. They help your data stay synchronized and accessible when things go wrong.
    

  

The following diagram shows an example of Azure regions. Regions 1 and 2 which support availability zones.

![[Pasted image 20250929180647.png]]

  

**What is Azure Government?**

US government agencies or their partners interested in cloud services that meet government security and compliance requirements can be confident that Microsoft Azure Government provides world-class security and compliance. Azure Government delivers a dedicated cloud enabling government agencies and their partners to transform mission-critical workloads to the cloud. Azure Government services can accommodate data that is subject to various US government regulations and requirements.

  

To provide you with the highest level of security and compliance, Azure Government uses physically isolated data centers and networks located in the US only. Compared to Azure global, Azure Government provides an extra layer of protection to customers through contractual commitments regarding the storage of customer data in the US and limiting potential access to systems processing customer data to screened US persons.

  

**Azure Marketplace**

Azure Marketplace is an online store that contains thousands of IT software applications and services built by industry-leading technology companies. In Azure Marketplace you can find, try, buy, and deploy the software and services you need to build new solutions and manage your cloud infrastructure.

There will be no direct support from Azure for the services from Azure Marketplace

  

**Components of Azure**

- Azure tenant
    
    - Tenants represent an organization
        
    - When any organization signs in/onboard to Azure is called an Azure tenant.
        
    - The suffix of the domain name of any tenant will be as **.onmicrosoft.com**
        
- Azure Active Directory
    
    - Azure Active Directory (Azure AD) is an enterprise identity service that provides single sign-on, multifactor authentication, and conditional access to guard against 99.9 percent of cybersecurity attacks.
        
    - Users can set up groups/users/identity protection
        
    - By default, one Azure AD will be associated with an organization
        
    - Organizations can create multiple Azure ADs, but all of them will be isolated from each other
        
- Management Groups
    
    - Management groups are containers that help you manage access, policy, and compliance across multiple subscriptions.
        
    - Management Group ID is the directory unique identifier that is used to submit commands on the management group
        
- Subscriptions
    
    - An Azure subscription links to an Azure account, which in turn is an identity in Azure Active Directory (AD).
        
    - A subscription is an agreement between an organization and Microsoft to use resources, for which charges are either paid on a per-license basis or a cloud-based, resource-consumption basis.
        
    - Billing will happen at the subscription level
        
    - Users only pay for what they use
        
- Resource Group
    
    - A resource group is a logical container into which Azure resources like web apps, databases, and storage accounts are deployed and managed
        
    - Resources can not be created/used without a resource group
        

  

**Hierarchy-**

![[Pasted image 20250929180703.png]]

- Resource Manager
    
    - It is the deployment and management service for Azure.
        
    - It provides a management layer that enables you to create, update, and delete resources in your Azure account.
        
    - When you send a request through any of the Azure APIs, tools, or SDKs, the Resource Manager receives the request. It authenticates and authorizes the request before forwarding it to the appropriate Azure service. Because all requests are handled through the same API, you see consistent results and capabilities in all the different tools.
        

The following image shows the role Azure Resource Manager plays in handling Azure requests.

![[Pasted image 20250929180713.png]]

  

**Azure Networking components**

- Virtual Network
    
    - Azure Virtual Network is a service that provides the fundamental building block for your private network in Azure.
        
    - An instance of the service (a virtual network) enables many types of Azure resources to securely communicate with each other, the internet and on-premises networks. These Azure resources include virtual machines (VMs).
        
    - A virtual network is similar to a traditional network that you'd operate in your own datacenter. However, it brings extra benefits to the Azure infrastructure, such as scale, availability, and isolation.
        
    - Handles inbound and outbound traffic
        
    - Connects to other Azure Vnets and to on-prems networks
        
    - Communicate between Azure resources
        
    - Defines a range of Private IP addresses
        
    - Azure resources communicate securely with each other in one of the following ways:
        
        - **Virtual network:** The users can deploy VMs and other types of Azure resources in a virtual network. Examples of resources include App Service Environments, Azure Kubernetes Service (AKS), and Azure Virtual Machine Scale Sets.
            
        - **Virtual network service endpoint:** The users can extend your virtual network's private address space and the identity of their virtual network to Azure service resources over a direct connection. Examples of resources include Azure Storage accounts and Azure SQL Database. Service endpoints allow you to secure your critical Azure service resources to only a virtual network.
            
        - **Virtual network peering:** You can connect virtual networks to each other by using virtual peering. The resources in either virtual network can then communicate with each other. The virtual networks that you connect can be in the same, or different, Azure regions.
            
- Subnet
    
    - it enables users to segment the virtual network into one or more subnetworks and allocate a portion of the virtual network's address space to each subnet.
        
    - The users can then deploy Azure resources in a specific subnet. Just like in a traditional network, subnets allow you to segment your virtual network address space into segments that are appropriate for the organization's internal network.
        
    - Segmentation improves address allocation efficiency. The users can secure resources within subnets using Network Security Groups.
        
    - Resources deployed in a subnet will be assigned a private IP address from Virtual network Ip range
        
- Network Security Group (NSG)
    
    - Users can use an Azure network security group to filter network traffic between Azure resources in an Azure virtual network.
        
    - A network security group contains security rules that allow or deny inbound network traffic to, or outbound network traffic from, several types of Azure resources.
        
    - For each rule, the user can specify source and destination, port, and protocol.
        
    - A network security group contains as many rules as desired, within Azure subscription limits.
        
    - Security rules are evaluated and applied based on the five-tuple (source, source port, destination, destination port, and protocol) information.
        
    - There are 4 possible combinations for NSG
        
        - At subnet as well as VM level (allows user to have control, maintenance issue)
            
        - Only at subnet level (Controlling traffic for all VMs, no maintenance issue)
            
        - Only at VM level (granular control on VMs, maintenance issue)
            
        - No NSG at all (no security)
            
- Network Interface Card (NIC)
    
    - A NIC is a component that holds the Public IP and the private IP of the VM. Also the users can associate the NSG to the NIC.
        
    - NIC can be deployed in a subnet of the Virtual Network.
        
- Firewall
    
    - It controls the inbound and outbound traffic but only at the Virtual network level
        
- Azure Virtual Machine
    
    - Azure virtual machines are one of several types of on-demand, scalable computing resources that Azure offers.
        
    - Typically, the user chooses a virtual machine when they need more control over the computing environment than the other choices offer.
        
    - An Azure virtual machine gives you the flexibility of virtualization without having to buy and maintain the physical hardware that runs it. However, you still need to maintain the virtual machine by performing tasks, such as configuring, patching, and installing the software that runs on it.
        
    - The users can monitor boot diagnostics for their VMs
        
    - Azure virtual machines can be used in various ways. Some examples are:
        
        - **Development and test** – Azure virtual machines offer a quick and easy way to create a computer with specific configurations required to code and test an application.
            
        - **Applications in the cloud** – Because demand for your application can fluctuate, it might make economic sense to run it on a virtual machine in Azure. You pay for extra virtual machines when you need them and shut them down when you don’t.
            
        - **Extended data center** – virtual machines in an Azure virtual network can easily be connected to your organization’s network.
            

- Azure Load Balancer
    
    - Load balancing refers to efficiently distributing incoming network traffic across a group of backend servers or resources.
        
    - Azure Load Balancer operates at layer 4 of the Open Systems Interconnection (OSI) model. It's the single point of contact for clients.
        
    - Load balancer distributes inbound flows that arrive at the load balancer's front end to backend pool instances.
        
    - These flows are according to configured load-balancing rules and health probes. The backend pool instances can be Azure Virtual Machines or instances in a Virtual Machine Scale Set.
        
    - Types of load balancer-
        
        - A **public load balancer** can provide outbound connections for virtual machines (VMs) inside your virtual network. These connections are accomplished by translating their private IP addresses to public IP addresses. Public Load Balancers are used to load balance internet traffic to your VMs.
            
        - An **internal (or private) load balancer** is used where private IPs are needed at the front end only. Internal load balancers are used to load balance traffic inside a virtual network. A load balancer front end can be accessed from an on-premises network in a hybrid scenario.
            

Figure: Balancing multi-tier applications by using both public and internal Load Balancer

![[Pasted image 20250929180728.png]]

**Different aspects of Azure Virtual Machines**

- **Series**
    

Some examples of different series of Virtual machines-

- **A-Series** (Entry-level VMs for dev/test)- A-series VMs have CPU performance and memory configurations best suited for entry level workloads like development and test, code repositories etc... They are economical and provide a low-cost option to get started with Azure.
    
- **Bs-Series** (Economical burstable VMs)- Bs-series VMs are economical virtual machines that provide a low-cost option for workloads that typically run at a low to moderate baseline CPU utilisation, but sometimes need to burst to significantly higher CPU utilisation when the demand rises. Bs-series VMs are not hyperthreaded.
    
- **D-Series** (General purpose compute)- The D-series Azure VMs offer a combination of vCPUs, memory and temporary storage that are able to meet the requirements associated with most production workloads.
    
- **E-Series** (Optimised for in-memory applications)- The E-series Azure VMs are optimised for heavy in-memory applications such as SAP HANA. These VMs are configured with high memory-to-core ratios, which makes them well-suited for memory-intensive enterprise applications, large relational database servers, in-memory analytics workloads etc.
    
- **F-Series** (Compute optimised virtual machines)- F-series VMs feature a higher CPU-to-memory ratio. They are equipped with 2 GB RAM and 16 GB of local solid state drive (SSD) per CPU core and are optimised for compute intensive workloads.
    
- **H-Series** (High Performance Computing virtual machines)- The HB-series VMs are optimised for HPC applications, such as financial analysis, weather simulation and silicon RTL modelling. HB VMs feature up to 120 AMD EPYC™ 7003-series CPU cores, 448 GB of RAM and no hyperthreading. HB-series VMs also provide 350 GB/sec of memory bandwidth, up to 32 MB of L3 cache per core, up to 7 GB/s of block device SSD performance and clock frequencies up to 3.675 GHz.
    
- **M-Series** (Memory optimised virtual machines)- The M-series family of Azure virtual machines are memory optimised and are ideal for heavy in-memory workloads such as SAP HANA. The M-Series offer up to 4 TB of RAM on a single VM. In addition, these VMs offer a virtual CPU count of up to 128 vCPUs on a single VM to enable high performance parallel processing.
    
- **N-Series** (GPU enabled virtual machines)- The N-series is a family of Azure Virtual Machines with GPU capabilities. GPUs are ideal for compute and graphics-intensive workloads, helping customers to fuel innovation through scenarios like high-end remote visualisation, deep learning and predictive analytics.
    

- **Sizes**
    
    - Each VM series has different sizes of VMs
        
    - The available sizes and options for the Azure virtual machines the users can use to run their apps and workloads. It also provides deployment considerations to be aware of when the users are planning to use these resources.
        

![[Pasted image 20250929180738.png]]

- **Pricing Options**
    
    - Pay as you go- pay for compute capacity by the second, with no long-term commitments or upfront payments. Increase or decrease consumption on demand.
        

  

- Azure savings plan for compute- save money across select compute services globally by committing to spend a fixed hourly amount for 1 or 3 years, unlocking lower prices until you reach your hourly commitment. Suited for dynamic workloads while accommodating for planned or unplanned changes.
    
- Reserved Instances- Azure Reserved Virtual Machine Instances provide significant cost reduction, compared to pay-as-you-go rates, when you commit to one-year or three-year terms. Suited for stable, predictable workloads with no planned changes.
    
- Spot- buy unused Azure compute capacity at deep discounts to run interruptible workloads.
    

- **Virtual Machine Images**
    
    - An image contains a boot loader, an operating system, and a root file system that is necessary for starting a virtual machine .
        
    - It also contains other preloaded softwares
        
    - There are variety of images present in the marketplace which are certified by Microsoft
        
    - User can also build their custom images
        
- **Virtual Machine Storage**
    
    - Azure managed disks are block-level storage volumes that are managed by Azure and used with Azure Virtual Machines
        
    - The available types of disks are ultra disks, premium solid-state drives (SSD), standard SSDs, and standard hard disk drives (HDD).
        
    - Managed disks are like a physical disk in an on-premises server but, virtualized.
        
    - With managed disks, all you have to do is specify the disk size, the disk type, and provision the disk.
        
    - The disk on which operating system of VMs are stored are called OS Hard Disk
        
    - The data stored in the Temporary hard disk will be deleted as soon as VM gets deleted
        
- **Configuring IP addresses**
    
    - **Public IP address**- it enables you to communicate to a VM from the internet. Assign a static public IP address, rather than a dynamic address, to ensure the address never changes.
        
    - **Private IP address-** When you create a virtual machine (VM), it's automatically assigned a private IP address from a range that you specify. This IP address is based on the subnet in which the VM is deployed, and the VM keeps this address until the VM is deleted. Azure dynamically assigns the next available private IP address from the subnet you create a VM in. If you want to assign a specific IP address in this subnet for your VM, use a static IP address.
        
    - An Azure Virtual Machine (VM) has one or more network interfaces (NIC) attached to it. Any NIC can have one or more static or dynamic public and private IP addresses assigned to it.
        
    - Assigning multiple IP addresses to a VM enables the following capabilities:
        
        - Hosting multiple websites or services with different IP addresses and TLS/SSL certificates on a single server.
            
        - Serve as a network virtual appliance, such as a firewall or load balancer.
            
        - The ability to add any of the private IP addresses for any of the NICs to an Azure Load Balancer back-end pool. In the past, only the primary IP address for the primary NIC could be added to a back-end pool.
            
    - Every NIC attached to a VM has one or more IP configurations associated to it. Each configuration is assigned one static or dynamic private IP address. Each configuration may also have one public IP address resource associated to it.
        
    - All IP configurations on a single NIC must be associated to the same subnet. If multiple IPs on different subnets are desired, multiple NICs on a VM can be used.
        
    - When adding a static IP address, you must specify an unused, valid address on the subnet the NIC is connected to.
        

  

**Virtual Machine Scale Sets**

- Azure Virtual Machine Scale Sets let user create and manage a group of load balanced VMs.
    
- The number of VM instances can automatically increase or decrease in response to demand or a defined schedule.
    
- Scale sets provide the following key benefits:
    
    - Easy to create and manage multiple VMs
        
    - Provides high availability and application resiliency by distributing VMs across availability zones or fault domains
        
    - Allows your application to automatically scale as resource demand changes
        
    - Works at large-scale
        

**Creation of Virtual Machine Scale Set (VMSS)**

- Virtual Machine Scale set has to be in same region as the virtual network
    
- By default, the VMs created by Scale Set is launched in different AZs of a region. User can manually select AZ(s)
    
- Maintain consistent configuration across all VMs
    
- User can edit and modify the NIC while creating scale set
    
- User can specify the initial instance counts (no. of VMs to be launched). User can not create more than 1000 VMs
    
- Overprovisioning- With over provisioning turned on, scale set actually spins up more VMs than you asked for, then deletes the extra VMs when the required number of VMs successfully provisioned
    

- **Health and repair**
    
    - user can configure the health monitoring on an application endpoint to update the status of the application on that instance
        
    - Automatic repair-Enabling automatic instance repairs for Azure virtual machine scale sets helps achieve high availability for applications by maintaining a set of healthy instances. If an instance in the scale set is found to be unhealthy as reported by Application Health extension or Load balancer health probes, then this feature automatically performs instance repair by deleting the unhealthy instance and creating a new one to replace it.
        

**Extensions**

- Azure virtual machine (VM) extensions are small applications that provide post-deployment configuration and automation tasks on Azure VMs.
    
- Extension packages are downloaded from the Azure Storage extension repository. Extension status uploads are posted to Azure Storage.
    
- For example, if a virtual machine requires software installation, antivirus protection, or the ability to run a script inside of the VM, you can use a VM extension.
    
- Azure VM extensions run on existing VMs, which is useful when you need to make configuration changes or recover connectivity on an already deployed VM
    
- Options for upgrade policy-
    
    - User needs to upgrade the VMs manually after downloading the extension onto VMSS
        
    - Automatically upgradation takes place in random order
        
    - Upgradation rolls out in batches with optional pause
        
- Users can attach the custom script extension to the VM