[[Networking]] [[Protocol]]
# Networking on AWS Overview
## VPC
VPC provides a private and isolated environment within the cloud infrastructure. You deploy services within this VPC while taking advantage of the cloud's benefits - scalability, cost, etc. 

You can also customize aspects of the VPC like access control, security, etc. 

# Overview of Virtual Private Cloud - VPC 
*VPC* -> private networking on cloud. Private partition of the network. 

*Subnet* -> smaller part of VPC, this is where you launch  instances. These are AZ. 

*CIDR Block* -> List of IP Addresses that can be within the VPC. 
- #note There a specific technical method to how the CIDR works, but just think about it as a list of IPs 

*VPC Peering* -> Connecting VPCs

![[Pasted image 20250702184527.png]]

- *Transitive Peering* -> networking allows a network peering connection to be extended across multiple VPCs in a chain like manner. In AWS we don't have that. You have to actually set up *VPC Peering* across the different VPCs 
![[Pasted image 20250702184410.png]]

AWS creates a default VPC with its defined AZs (subnets). 
- n regions -> n default VPCs

#note you can delete the default VPC and set up your own, but its not recommended. If you want it back you have to open a ticket

## Route table
Component of the VPC that defines the rules for routing network traffic within it.
- It determines how traffic is directed between subnets, internet gateways, virtual private gateways and other network resources 

Allows all the subnets to talk to each other

## Internet Gateway
Managed service allows instances to go out to the internet

## NAT Instance/Gateway
Enables multiple devices in a private network to share a single public IP for internet access
- Conceals internal IPs
- Gate keeper 
![[Pasted image 20250702185456.png]]

- The NAT is a great way to take care of back end assets 

## CIDR 
An IP is a.b.c.d -> each letter is 8 bit, so in total 32 bits. 

CIDR notation is -> a.b.c.d/prefix -> 10.0.0.0/16 -> 16 means the potential number of IPs
- ![[Pasted image 20250702185856.png]]
- The above image shows how to calculate how many IP addresses you can have. There could be possibly 65k IP addresses - range

#note CIDR shrunk the subnet mask from a.b.c.d/255.255.255.0 to the one mentioned above with the prefix 

another example of how to interpret CIDR:
![[Pasted image 20250702190148.png]]

the 0 to 255 are possible IP addresses, so you have 192.168.100.0, 192.168.100.1, 192.168.100.2 all the way to 255 so that gives you 256 possible IPs, multiplied by 4 -> 1024
#### Practice quiz question: What are the typical components in a VPC?
One or more subnets, Internet gateway (if internet connectivity is desired), one or more route tables 

There are some IPs that are reserved for AWS use:
![[Pasted image 20250702191505.png]]


Networking is very important, you need to learn this. Have it spot on. 

### Recommendation - Best practice
Never launch a production environment in the default VPC. This is a very liberal connection - meaning it can easily be accessed by someone. The network topology needs to be more protective. 

## Summary
A VPC allows users to create isolated and private virtual networks. It controls network configuration:
- IP ranges, subnets, routing tables and security 

Subnetting in a VPC allows users to create smaller network segments, each with its own IP address range and security policies

*CIDR* (Classless Inter-Domain Routing) is a networking addressing and routing method that allows for more flexible and efficient allocation of IP addresses 

*Internet Gateway* -> horizontally scaled, highly available, redundant VPC component that allows the VPC to access the internet

*NAT gateway* -> allows instances in a private subnet to connect to services outside your VPC but external services cannot initiate a connection with internal instances
- For example, a private EC2 instance can access resources from the internet like a OS patch or use `yum`, `apt` or `pip`

*Route Table* -> Contains a set of rules, called routes, that determine where network traffic from your subnet or gateway is directed 


#### Practice quiz question: What are the minimum components needed in order to deploy an application on AWS using cloud networking principles 
VPC and Subnets 
- A custom VPC allows you to isolate your environment from other AWS users. This means your resources are not shared with unknown parties, reducing the risk of accidental data exposure. With custom VPCs, you can create private subnets, ensuring that certain instances do not have direct access to the internet, which adds an extra layer of security.


# How NAT Gateway/Instances works 

Let's say you want to install new packages on your Ubuntu EC2 instance, so you perform a `sudo apt update` + `sudo apt upgrade` then, a request is sent to `www.ubuntu.com` to get the latest packages. Since this is a private EC2 instance, it has a private IP and no Internet Gateway, which can't be accessed by resources on the internet.

Then, since this EC2 instance is 'hidden' the request:

1) goes to the NAT instance,
2) replaces the source IP (private IP) with its own Elastic IP,
3) sends the request to `www.ubuntu.com`
4) Receives the response 
5) Forwards it back to the original private EC2 instance 

![[Pasted image 20250710090915.png]]


## NAT Gateway vs NAT Instance

So according to Chatgpt, these terms are not the same. I visited the [documentation](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html) for NAT instances and got this warning:

> [!NOTE] NAT Instance -> Migrate to NAT Gateway
> If you use an existing NAT AMI, AWS recommends that you [migrate to a NAT gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html#nat-instance-migrate). NAT gateways provide better availability, higher bandwidth, and requires less administrative effort. For more information, see [Compare NAT gateways and NAT instances](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html).
> 
> If NAT instances are a better match for your use case than NAT gateways, you can create your own NAT AMI from a current version of Amazon Linux as described in [3. Create a NAT AMI](https://docs.aws.amazon.com/vpc/latest/userguide/work-with-nat-instances.html#create-nat-ami).

Here's a comparison table either way, but default to NAT Gateway:

## ✅ Use NAT **instance** when:

- You want more control (e.g. install security tools, use custom firewall).
    
- You have low traffic and want to save money.
    
- You’re experimenting or learning.
    

## ✅ Use NAT **gateway** when:

- You need **high availability**, **simplicity**, and **high bandwidth**.
    
- You don’t want to manage patching, scaling, or failover.
    
- You’re in a production environment.



