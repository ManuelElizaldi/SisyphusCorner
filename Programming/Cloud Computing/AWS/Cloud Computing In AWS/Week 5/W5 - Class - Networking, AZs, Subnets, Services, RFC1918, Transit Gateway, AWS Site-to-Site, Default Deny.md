[[Network]] [[RFC1918]] 

# Regions and Availability Zones
AWS Account -> Region -> Multi AZ 
- We use many AZs for high availability 
- AZ -> data center
- All AZs are connected via fiber optic, this gives it low latency within the Region
![[Pasted image 20250713090811.png]]

Amazon can use inter connectivity within regions with high speed internet 

The data goes through AWS private connections 

![[Pasted image 20250713090946.png]]

*VPC* -> Virtual Private Cloud, its always inside a region. VPCs are regional resources. Within the VPC you deploy your services:
![[Pasted image 20250713091101.png]]

Some services run within the VPC and others run outside. Also there are some services that run outside the region:

![[Pasted image 20250713091214.png]]

### Types of services depending on where they are deployed:
- Zonal

- Regional 

- Global -> you create it once and you use it for your entire regions

From a networking perspective, how do these all services talk to each other

> [!NOTE]
> > Around 250 services inside AWS 

## Subnets and AZs
In general no one uses a default VPC (AWS created). 
![[Pasted image 20250713093020.png]]

One subnet per AZ, each subnet has a CIDR block that does not overlap with the VPC CIDR block.
![[Pasted image 20250713093206.png]]

### Creating a VPC from scratch - Custom VPC
You need a CIDR block - classless inter domain routing. This is made up of different blocks. One you are building a network you have to answer the question:
- Size of network?
	- a.b.c.d/16? a.b.c.d/26? The smallest you can build is /28 and largest /16 

#### Security:
There are *Firewall* settings that you can establish to protect your VPC

##### Caveats
> [!NOTE]
> The CIDR cannot overlap with another CIDR. **You can't have the same IP address repeated**. CIDR cannot overlap with the data center

#### Private vs Public
*RFC1918* -> They declared private IPs. Document that declares internet best practices

### Private IPs from RFC 1918:
![[Pasted image 20250713092453.png]]

##### Home Scenario:
laptop (private IP) -> Verizon router (public IP) -> internet -> google.com
- The router keeps a tab on who's making the request to an endpoint. When the response is sent back, it knows where to send it. 

Data Center -> Internet <- This uses *public IP*

Data Center also talks to DB & Server, etc. but it really does not need to talk to the internet. <- if you are talking internally, you use a *private IP*

### Route Tables
You need to have a route table, every subnet has a route table. Every route table has a **destination** and **target**. 
- If the communication is within the VPC, the target will be set to **local** by default

![[Pasted image 20250713093504.png]]

![[Pasted image 20250713093530.png]]

### Internet Gateway
#### If you want to send information outside the VPC 
You will need an **Internet Gateway**. You only need 1 internet gateway per VPC, you can't create more than 1. 
![[Pasted image 20250713093716.png]]

*VPC to internet*
1) Create a Internet Gateway
2) Attach Internet Gateway to VPC
3) Create route table entry (target & destination) - Explicit route
	- quad 0 rule 
![[Pasted image 20250713094111.png]]

## Public vs Private Subnet - VPC DHCP & VPC DNS 
![[Pasted image 20250713094553.png]]

Instances can have a public and private IP address. VPC DHCP service will add a private IP, the public IP 

VPC DNS -> new resource provisioned, it will automatically assign a public and private DNS 

![[Pasted image 20250713094841.png]]

## Internet Access for Private Subnets - NAT Gateway (Network Access Translation)
If you want to talk to the internet via a private connection. For example if you want to patch an instance. 

NAT gateway does the same thing as a home router. Your private IP is translated into a public IP 
![[Pasted image 20250713095549.png]]

NAT gateway interacts with the internet via the internet gateway. 

You also need to add a rule to the route table so that the private instance can talk to the NAT gateway. You have to be careful when you set up this rule, you don't want to add as a target the internet gateway because that would make your private instance public. 

#### Another example
![[Pasted image 20250713095938.png]]

## VPC Peering - Transit Gateway & Direct Connect Gateway
![[Pasted image 20250713100324.png]]

This approach is good for 2 or 3 VPCs, but for many VPCs you need to use: 
![[Pasted image 20250713100345.png]]

The advantage of this is that you don't do much heavy lifting. Also Peering does not allow *transitive routing*. 

![[Pasted image 20250713100633.png]]

## Connecting VPC to Data Center (on prem)
Using *AWS Site-to-Site*, goes through internet, its secure because its encrypted, but this makes it slower. 

To resolve the latency, they created *direct connect*. With direct connect you go to a third party data center and connect your router there. AWS does the same. You sign an agreement that you don't touch AWS router 
![[Pasted image 20250713101004.png]]


## Security
##### AWS security policy: Default Deny With Explicit Allow
for example if you have a SG that allows http TCP port 80, and a NACL that denies HTTP, the ACL will win because *Default Deny With Explicit Allow*


Most data centers (on prem) are flat, meaning, once you breach one point everything will be accessible. Cloud is more robust on their security. You have route tables, IAM, firewalls, security groups (stateful) NACL (stateless), there are many ways they are protected. 
- This does not mean that on prem is not safe, but sometimes they have more vulnerabilities, its hard to build these robust systems. That's why organizations leverage AWS technology

## DNS - Route 53
Route 53 -> managed service, domain registrar, public and private DNS zones

Route 53 can also do health checks -> if some service is unresponsive, it will stop sending data packets to that service
![[Pasted image 20250713105048.png]]

Once you create a DNS/website you can forward traffic to many AWS services. 
![[Pasted image 20250713105934.png]]

