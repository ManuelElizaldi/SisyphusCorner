[[Azure]]

Consulting firms use cloud computing 

*Virtual Network* -> contains your resources in a private network 
- This needs a CIDR block 

**Think of the virtual network as a house and the CIDR block determines how many rooms are inside the house**

Public subnet and private subnet
- public for front facing to the user
- private for any backend tasks 

users on internet -> load balancer 

Scale set = Autoscaling group. 
### Networking security
NACL = Network Access Control List 
- at the subnet level

Network security group -> at the VM level


### Shared responsability
If an AZ goes down, its the cloud provider's responsibility to bring that AZ back up and its also your responsibility to build highly 
available applications.  



### VNet Peering
You can also create a VPN to communicate between on prem to Vnet, this is a bit slower than Express Route

#### Cloud to Cloud communication question
AWS cloud talk to Azure cloud?  EC2 instance talk to a SQL server on Azure 

**There are clients that have multiple setups in different cloud providers**

*There is no cloud to cloud communication* You need to establish a connection from AWS -> on prem and then from on prem to Azure
- This is a certification exam question 

For this use *Direct Connect* in AWS and Azure has *Express Route*

## Landing zone
Where you applications will land 

Subscriptions have no cost - make subscriptions depending on the business unit. 

## Private endpoint & public endpoint
![[Pasted image 20250928101725.png]]

Endpoints are where traffic flows. If you want to access a private service within your cloud you will want to create a private end point

## Tenant
You can assign users to a specific subscription 

## Express Route
Connects on prem to the Azure cloud 

Connects to one region

## Virtual WAN 
VPC Peering can be slow, so use Virtual WAN 

## Azure Landing Zone






---
### Resources
https://learn.microsoft.com/en-us/azure/architecture/networking/architecture/hub-spoke

https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/