[[Azure]] [[Cloud Computing]]
## Cloud computing models
on prem, private, public and hybrid 

## Delivery models 
![[Pasted image 20250519180444.png]]

## Azure Region
Where you can deploy infrastructure - not a country

You can deploy application into regions 

Azure government - fully compliant with government policies

Inside each region there is a data center, each data center is an *availability zone*
- Each region has 1 **or** 3 availability zones. 


## Types of Services
Very similar to AWS service - if you have a service in AWS, most likely there will be a same service in Azure, although there are some differences. 

Compute, networking, storage, databases, web, IOT, big data, identity, AI, monitoring, DevOps

Azure does not exclude you from using services not made by Microsoft, there are services that can be integrated to Azure. 

You can also use any language of your choice in the Azure cloud.

# Azure Components
![[Pasted image 20250922193730.png]]

## Azure Tenant
When you sing up you become a tenant, tenant means that you onboard to Azure.

You are also assigned a domain -> `.onmicrosoft.com` 

You also get an active directory:
- Users
- Groups
- Identity protection
- Management groups - *Active directories are independent of each other*
	- If you have multiple business units, each can have its management group - based on these groups you create policies. 
		- Nested management group 
	- subscription -> resources under subscription 
- Resource group 
- Resources 

Tenant -> an org 
### Subscriptions
Billing happens at the subscription level, and a best practice is to create multiple subscriptions for a single project, for example:
- ecommerce dev, e commerce-uat (user acceptance testing), e commerce production 

Different subscriptions per environment, that way you'll have billing per environment 
### Resource group
Container where you store the resources 

Why have multiple resource groups? Most companies have micro services, each with its own needs, its a good practice to create on for each 
### Resources 
VMs, permissions, storage, etc. 

## Azure Resource Manager
![[Pasted image 20250922193821.png]]

The only layer in Azure that allows you to deploy resources. 

You can deploy through Azure portal, power shell, CLI or APIs but everything goes through the Azure Resource Management layer 





