2025-6-4
# EC2 Core Features

## Core Features - Introduction - EC2 - Virtual Machine, Instances

Before running a VM you need a *Tag* (name). Tags enable you to categorize your instances, for instance: by purpose or environment. You can filter tags based on your need.

Tags help you group instances 

![[Pasted image 20250604181118.png]]

*Instance Type* determines the hardware of the host computer used for the instance. There's different types based on needs:

![[Pasted image 20250604181207.png]]

Previous generations do not get retired because there's software that depend on them. If AWS retires them, it would affect customers. They usually let you know if they are going to retire something. 

- General purpose -> good for anything, balance of all resources.
- Compute optimized -> great for high performance requirements
- Memory optimized (RAM) -> high storage, used with applications that need to process large amounts of data or maybe you are going to use it for in memory storage database applications
- Storage optimized -> Used for workloads with very high sequential read and write access to a large data set stored locally

*Operating System* (AMI) -> Amazon Machine Image, is a template for virtual machines in Amazon's EC2, it contains all the information needed to launch an instance. It contains an operating system at a minimum. 

Lift and shift strategy/rehosting strategy -> move your application to the cloud without modification. You can create an AMI in your on-prem server and then move it to AWS. Once its moved you can launch VMs in AWS with that AMI

*EBS* (Elastic Block Storage) ->  Virtual hard disk, you can attach it to any VM instance.

Each VM requires at least 1 volume to store the AMI, you can have more, and actually recommended. You can have a dedicated disk for a database inside a volume, separate from the disk/volume that contains your application. 

*VPC* -> VPC is the region, which is made up of smaller components, subcomponents, subnetworks -> subnets. The subnet is the specific availability zone where you intend to launch the VM. 
- *Primary network interface EIN* -> by default, each VM has one 
- You can create additional network interfaces with specific purposes. 
- How many network interfaces can be attached depends on the capabilities of the EC2 machine

*ENI* -> Virtual network card, provides connectivity to your cloud resources. Includes private IP, public IP, MAC address, security groups and source/destination checks. 
- You can have multiple ENIs in a single server, that way you can segment networks
- You can attach, detach the ENI
- You usually set up available ports and IPs before launching the instance


![[Pasted image 20250604182823.png]]

#### Practice Quiz Question: ___ feature helps in grouping instances by purpose, owners, etc.
Tags

*Security* -> AWS offers multiple security options, but here's the basic EC2 instance security features:
- Security group -> virtual firewall, controls incoming and outgoing traffic, this is attached to the networking card. 
	- Inbound rules -> what goes in
	- Outbound rules -> what goes out
	- Type field -> protocol used for communication
	- port -> where it can be accessed
	- Description -> how it works 
	- *PEM file* -> Privacy enhanced mail. File format used for storing and sending cryptographic keys, certificates and other data. It is used in web servers and network communication security. Private 
		- It contains a private and public key, you need both 
![[Pasted image 20250604183228.png]]

## Summary
![[Pasted image 20250604183526.png]]

- Resource that is in a specific AZ within a Region
- VM running OS along with application
- Connects to a virtual cloud network using a virtual network interface
- Storage to hold the application data
- Bedrock of AWS cloud 

#### Practice Quiz Question: In order to configure an EC2 instance you need at the minimum:
Region, availability zone, operating system


Availability Zone is inside a Region