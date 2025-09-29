[[IaC]]

*AWS CloudFormation IaC* -> a way to speed up provisioning infrastructure. You have a template that determines what is provisioned. Reusable, maintainable, extensible and testable infrastructure. 

Two main approaches for writing IaC code

### declarative IaC and Imperative IaC
#### make sure to understand this

![[Pasted image 20250914090950.png]]

CloudFormation will never accept an untested template. 

## Benefits of Treating Infrastructure as Code
![[Pasted image 20250914091650.png]]

From one template you can provision a Development and Production environment. 2 environments from 1 template. Parameters can be added to the template to decide on detailed differences between the two environments. 

When building a template use *order and predictable* provisioning. There is always something that comes first in your architecture -> VPC, subnets, private and public network, internet card,etc. 

Version Control - Git is usually used for code, but infrastructure also has versions. 

Deploy and update stacks using console, command line or API. 
- Some people prefer console over CLI, some prefer CLI. It is just preference. 
- In a work environment, they use an IDE to connect to the cloud platform. Vs code connects to the cloud env and from there use the terminal. 
- Some really nerdy people follow the documentation and use the CLI entirely. 

You only pay for the resources you create

## Components and Technology 
![[Pasted image 20250914092826.png]]

Roll back everything vs only rolling back the block that contains the error. 

The goal is to prepare the template -> you test on a local machine

*Git Sync method* -> that's how pushing changes is actually done. 

## Template Values
Description -> description of your resource

Parameters -> 
- Key pair -> type: String. 
- env type
- instance type
	- default
	- allowed values
- SSH location

Resources -> master block. You can declare as many resources here. 
*example* -> 	- "Ec2Instance" : {
					properties : {image id, instance type, key name}
					}

		- "Type": "AWS::EC2::Instance"

**the type can be grabbed from the AWS documentation**


IAM policies are attached in a resource block 

## Conditions, Mappings, Pseudoparameter, Functions

## Design
Always start with your network infrastructure

![[Pasted image 20250914103418.png]]


## Terraform - Hashi Corp Tool
Not a AWS tool, but still used with AWS. IaC tool. More advanced at managing the source codes. 




Professor will send json for us to troubleshoot - there are some resources that are not health, make them healthy.


