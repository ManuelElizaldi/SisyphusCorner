
checkpoint -> Used $5.1 of $50
### A database server in a private subnet needs to communicate via port 3306 but is unable to receive requests from the app server despite ping requests being successful between the servers. What could be the reason for this?
Port 3306 is closed for the server
The required port has to be open on both servers for communication to take place between them. To ensure the security group access is secure, it should include the CIDR of the app server's subnet.


### Under which of the following conditions can VPC peering fail?
VPCs have overlapping CIDR blocks


### Which of the following conditions occur when an Internet Gateway is deleted without editing the corresponding entry in the routing table?
Black Hole
A Black Hole status indicates that a route table entry refers to a resource that does not exist. It can be easily deleted like an entry which is valid.

### Which of the following best describes a NAT?
Traffic Conduit

A NAT instance (or gateway) will neither consume nor produce traffic. Its only job is to forward received traffic.

To quote AWS - "When you create a NAT gateway, you specify one of the following connectivity types:

- **Public** – (Default) Instances in private subnets can connect to the internet through a public NAT gateway, but cannot receive unsolicited inbound connections from the internet. You create a public NAT gateway in a public subnet and must associate an elastic IP address with the NAT gateway at creation. You route traffic from the NAT gateway to the internet gateway for the VPC. Alternatively, you can use a public NAT gateway to connect to other VPCs or your on-premises network. In this case, you route traffic from the NAT gateway through a transit gateway or a virtual private gateway.
    
- **Private** – Instances in private subnets can connect to other VPCs or your on-premises network through a private NAT gateway. You can route traffic from the NAT gateway through a transit gateway or a virtual private gateway. You cannot associate an elastic IP address with a private NAT gateway. You can attach an internet gateway to a VPC with a private NAT gateway, but if you route traffic from the private NAT gateway to the internet gateway, the internet gateway drops the traffic."

### What is the default limit for the number of VPCs per region?
You can have 100s of VPCs per Region for your needs even though the default quota is 5 VPCs per Region. 5 VPCs per region is a soft limit and can be increased by raising a support request with AWS.

### A network administrator needs to create a VPC for 13 EC2 instances and has decided to assign the CIDR block 192.168.5.0/28. Which of the following problem is likely to be encountered here?
Number of IP address will fall short
Number of IP address will be 2(32-28)-5=24-5=16-5=11, which will fall short of the required 13 addresses.


### Which of the following is a difference between NACLs and Security Groups?
NACL is stateless while security group is stateful

### To block traffic from a particular IP, use _________
A _network access control list (ACL)_ is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. You might set up network ACLs with rules similar to your security groups in order to add an additional layer of security to your VPC.

Security group allows traffic from a source but does not have the ability to block requests.

### Which of the following can be used to transfer data securely between two EC2 instances created in separate AWS accounts?
VPC Peering
VPC Peering works between VPCs in AWS across regions and even between different accounts. The peering VPCs should not have overlapping CIDR.

### Which of the following is not true regarding Elastic Network Interfaces.
A secondary interface can be attached to an instance while it is running

### A _________ is a server whose purpose is to provide access to a private network from an external network, such as the Internet. Because of its exposure to potential attack, it must minimize the chances of penetration.
Bastion host

### Which of the following is used for a dedicated and highly secure connection from a private data center to an AWS data center?
DirectConnect
Explanation: DirectConnect is used to create a dedicated physical connection between an on-premises data center to an AWS center for data transfer. VPN is incorrect because it is not as secure as DirectConnect due to the internet service provider it ends up using.

### What is the relationship between the number of regions used and the number of default VPCs in an AWS account?
One-to-many 
Every region will have 1 default VPC created for every user 

### What are the options if a VPC is running out of available IP addresses? The choice must be operationally least intrusive.
Add a secondary CIDR block
According to AWS - Amazon Virtual Private Cloud (VPC) now allows customers to expand their VPCs by adding secondary IPv4 address ranges (CIDRs) to their VPCs. Customers can add the secondary CIDR blocks to the VPC directly from the console or by using the CLI after they have created the VPC with the primary CIDR block. Similar to the primary CIDR block, secondary CIDR blocks are also supported by all the AWS services including Elastic Load Balancing and NAT Gateway.

This feature has two key benefits. First, customers, who are launching more and more resources in their VPCs, can now scale up their VPCs on-demand. Second, customers no longer have to over-allocate private IPv4 space to their VPCs - they can allocate only what is required at the time, and later expand it as needed. With these benefits, this feature can make it significantly easier for customers to manage their private IPv4 address space.

### Which of the following cannot be used to connect on-premise data center to cloud?
Bastion Host
AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS.

Site-to-site or Client VPN - both allow connectivity from VPC to on-premises network.

CloudHub - If you have more than one remote network (for example, multiple branch offices), you can create multiple AWS Site-to-Site VPN connections via your virtual private gateway to enable communication between these networks.

**What is the default setting for DNS hostnames when a new VPC is created? Enabled Disabled Can be set during VPC creation Depends on the Region used**

Disabled - by default, when you create a VPC, EC2 instances do not get a public DNS hostname attached to it 
- Security reasons 

