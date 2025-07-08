[[Network]] [[Data Transfer]] [[Protocol]]

# Hybrid Cloud & Networking 

Enterprises have already invested in machines and infrastructure. This is built over the years and after some time you start leveraging cloud resources. You can connect both on-prem to cloud infrastructure

Services are integrated through the *VPN*. You have to make sure CIDR blocks don't over lap - between on prem and cloud.

Another option to connect both is *Direct Connect* -> AWS service that enables organizations to establish dedicated network connections from their on prem to AWS cloud services
- direct fiber that by passes the internet
- Traffic is isolated 

Both VPN and Direct Connect are incremental

## Data Transfer
Snowball edge -> suite case device that you use to load your data. This is shipped by AWS and then shipped back to them 

Snowball mobile -> a truck with all the compute infrastructure and you transfer your data through here. The truck will go to your premises and you connect to it 

These two methods are used to migrate data 

## CIDR Blocks 
IP addressing method that enhances IP address allocation by utilizing a single IP address combined with a prefix to represent a range of IPs

IPv4 is running out, so now IPv6 is being used more 

There's internal IPs that are reserved:
![[Pasted image 20250703163434.png]]

Applications bind to internal IPs, you don't want it attached to a public IP

#### Practice quiz question: What is AWS direct connect?
Establishing dedicated network connections to AWS 

## Guidelines - Limitations
Adding a CIDR block to your VPC:
- prefix between /28 and /16
- your CIDR block can't be larger than the route table 

There are are other requirements here -> [documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-cidr-blocks.html)

## Working with networking 
### Network tracing:
Traffic comes through -> gateway -> router -> route tables -> network access control list (filtering) -> security groups -> AWS resource 

The reverse also happens when the response goes back 

#### TCP
IP address and port are required for TCP 

Source port & destination port 

Source port = ephemeral port 
- This changes for each request 
Destination port remains the same 

This has to be set up properly in the ACL (access control list)

#### NACL vs Security Group
ACL -> stateless -> if you state the inbound, the out bound in not automatically set

Security groups -> stateful -> if you determine inbound it also defines outbound 

- ephemeral ports need to be always open in terms of outbound 
- ephemeral ports are also used by UDP

#### Practice quiz question: __ is a characteristic of network access control lists (NACL)
- stateless 


## Amazon VPC Limits
If you know the limits you can properly provision for that 
There are limits to every aspect of networking in AWS, this is just one exmaple:
![[Pasted image 20250703165652.png]]


#### Practice quiz question: Which of the following is used for a dedicated and highly secure connection from a private data center to an AWS data center?
Direct Connect 

# Scenario - Creating Secure Deployments
VPC -> you build all your services here 
- it will have its DRT (default routing table)

Every VPC requires a CIDR block 

Within the VPC there's *subnets*, each with its own CIDR block. 1 public and 2 private

To allow the VPC to communicate with the internet you need the *Internet Gateway*, but the Internet Gateway needs the Route Out/Route Table -> but this needs to be customized to only allow the public subnets to go out. 

If one of the private subnets is a database, it needs to be able to receive traffic from and only from the Public Subnet that was attached to the *custom routing table* that enables internet access. 
- To achieve this you create a security group: You open SSH port (22), for the EC2 instance in the public subnet 

*The Hop* You SSH into a public instance, then into the private from the public. This happens only if you allow it on the security group 
![[Pasted image 20250704110653.png]]

- The public EC2 instance is called the *bastion host* or *jump server* This is the entry point to deeper into the VPC. Using this increases security

*Peering* -> This will be default VPC 
- There's a receiving and a requesting - the one we have been talking about is requesting. You need to accept this request to connect to enable peering
![[Pasted image 20250704111514.png]]

- Also, you need to create *route table entries* 
- *Inside the Route Table of each VPC you will have the CIDR block of the VPCs*
	- In a way you are creating a highway between both VPC 
- You also need to open ports  

*Internet Control Message Protocol* -> Used for error reporting, diagnostics and IP network management 
- Sends pings for diagnostics -> I've done this in the past 

#### Practice quiz question -> Which type of AWS route table is automatically created for each VPC?
- Default (Main) Route Table

### This is the setup up in the video
The details mentioned above are the notes taken from this set up:
![[Pasted image 20250704112653.png]]


## NAT - Network Address Translation

Why a DB needs access to internet? -> Fast updates/patches. You could also build a new AMI with the patch and then deploy that but it would take a lot of time

NAT is like a one way mirror -> it will allow the DB EC2 instance to access internet but no one can access the EC2 instance.
- *This is the power of the NAT*
- Increased security 

### How to Set up NATs
There are 2 ways of setting it up:
1) *NAT instance* -> but this requires a lot of knowledge/experience of IP tables linux utility. 
	- Not a creator nor a consumer of information. NAT is just a pass through. Disable what is called *source destination checking* for it to work. 
	- This is just an instance and it can fail, so it might not be the most reliable 

There's a second option:

2) *NAT Gateway* -> Managed service. Load balance, no single point of failure. 
	- In terms of functionality, it offers the same as NAT instance but its more resilient 


## Summary 
The following components play a critical role in highly secure cloud deployments
- *custom VPC* that is not liberal 
- Its not recommended to use the *default VPC* - this is public, there might be vulnerabilities. Its better to build your own custom VPC 
- *Multiple subnets*, combination of public and private depending on the use of the EC2s
- *Internet Gateway* for external access - if the application is internal, this is not needed - only if you are going to use the internet 
- *Route tables* to configure various routes 
- *NACL* (network access control list) for blocking or allowing traffic from specific IP addresses 
- *NAT* allow private resources to reach out to the internet if required 
- NAT can be implemented in two ways - *gateway* (AWS managed) or *Instance* (customer managed)
- Define specific *security groups* to open only the required ports and from specific IP addresses as needed 
- *Bastion host* to reach the private resources for administrative activities 
- Two VPCs can communicate with each other via *peering* and transitive peering is not allowed

#### Practice quiz question: Which of the following services qualify for private subnet deployments?
Database servers and Financial documents on volumes attached to EC2 

AWS VPC private subnets are well-suited for use cases that require high-security and controlled access to critical resources. Here are some ideal use cases for AWS VPC private subnets:

1. Hosting databases in private subnets is a common use case. These subnets ensure that databases are not directly exposed to the internet, reducing the risk of unauthorized access.

2. Managed application back-end services (such as business logic, microservices, and other application servers) are often deployed in private subnets to ensure they can only be accessed by front-end services or other internal components.

3. Applications or services that are intended for internal use within an organization can be hosted in private subnets to prevent external access entirely.

4. Workloads that involve sensitive data, such as financial transactions and personal information processing, can be secured in private subnets to isolate them from the internet.