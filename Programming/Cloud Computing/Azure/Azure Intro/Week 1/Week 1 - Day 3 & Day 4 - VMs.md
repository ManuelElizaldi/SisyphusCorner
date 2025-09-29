[[Virtualization]] [[Azure]] [[Azure Resource Manager]] [[Gen AI]]
# VM Series
There are different types of VMs for your needs

A - entry level, used for development or testing
B - economic, development or testing 
D - general purpose 
E - in memory, hyper threaded - in memory work, very fast 
F - compute optimized - lots of tools, for applications that are CPU intensive 
H - HPC computing - High performance computing
M - Memory optimized 
N - GPU enabled 

You can also choose the VM Size:
- CPU
- Memory
- number of disks
- IOPS

## Pricing options
*Pay as you go* -> pay for what you use

*Reserved VMs* -> upfront purchase in a region, provides cost savings

*Spot VMs* -> Use unused capacity in Azure. Can be taken by Azure, highly discounted. Same as AWS 
- Great for batch work

*Azure Hybrid Benefit* -> Enterprises that already bought licenses and still want to use them you can use them through Azure and have cost savings. 

## VM Images
OS that will be deployed on the VM 
- Same as AMI from AWS 

There are marketplace Images and you can also customize your own. 

## VM Storage
OS hard disk - default hard disk that will always be there because that's where the OS is installed.

Temporary Hard Disk - attached to the VM, if you delete the VM, the data will be deleted - ephemeral data. 

Attach multiple data disks (optional) - block storage. Separate from VM


> [!NOTE] VM Storage
> There will always be 2 storage in your VM, the OS hard disk and the temporary hard disk. 

# Deploying a Virtual Network
1) Create a Virtual Network 
You assign a range of IP addresses (CIDR), you name it, you choose the region

You also need at least one subnet in your VNet

For security you can choose to disable the *DDOS standard protection*, what this does is that it doesn't remove the entire protection but you are left with the basic protection service. If you enable it you will have to pay for it. 

Then you choose to add a firewall and its IP addresses 

2) Creation of Subnet with its IP ranges

3) Create the Security Group 
It's good practice to create the security group before you create the resources. 

You select the subscription and resource group 

4) Attach the security group to the subnet or NIC

 Inside the security group, there's an option for subnet. You choose the subnet that you want to attach the SG to. 

5) Before you create the VM, you need to create the *public IP* address. This step is optional since VMs sometimes remain a private resource
- *Dynamic IP* address -> only assigned when attached to a resource. You only pay for the time it spent attached to the resource. 
- *Static IP* -> You keep this even if you remove the resource it's attached to. 

The IP needs to be in the same region 

# Creating a VM - TIO
First create a resource group - container where you store resources 

Then I created a VM in this resource group, most of the settings where left as is - default. 

Ubuntu image and SSH port open 

Review and create 

NIC is automatically created by Azure and attached to the VM

For storage, 2 disks will be created OS disk and Data disk

### You can upgrade the size of your VM after lunch
but after upgrade, your VM and all of its data will be removed. So make sure you are storing you data in a permanent storage 
### Effective security rules
The default security group created for the VM
#### Topology - it shows all of your resources in a graph 
Visual aid to see what resources are deployed and how they are related 
![[Pasted image 20250926165749.png]]


## Configuring IP address 
Dynamic allocation -> from the subnet range, one will be chosen. 

Multiple private IPs for each application 
- This can also be achieved by having multiple NICs

# VM ARM Template using GenAI
*Azure Resource Manager (ARM)* -> deployment and management service for Azure. Everything in Azure gets created through this layer. It handles all requests regardless of where you are creating from (shell, API, management console)

For this TIO we did create a Virtual Network with CIDR block 10.0.0.0/16. New *public IP* and new *security group* with inbound rules from anywhere SSH 
- The NIC will have the public and private IPs that you create 
- multiple private IPs can be created for one NIC

After the creation of the VM you can go into the Resource Group that we created and all of the resources that were created when we launched the VM will be stored here. For example, the NIC, security group, public IP, SSH public key, etc. 
- Each time you create a VM, there are resources that will be created automatically if you haven't created them yet, for example the public IP or the hard drive. 

You can download the Resource Group template, this will include all of the resources in your group. It downloads a zip file with the tempalate.json, parameters.json and .ps1 or .sh deployment script

*template.json* -> specifies the resources to be built and the relationship between them, as well as the parameters used (type, constraints, but not the actual values). Also expected output after deployment 
- **Declares the what and how, what will be deployed and how they should be configured**

*parameter.json* -> actual parameters for the template, environment specifications and sensitive info 
- **Provides what values - the specific settings needed for your deployment**

This separation allows you to: 1. Reuse the same template for different environments (dev, test, prod) 2. Version control the structure separately from the values 3. Share templates without sharing sensitive configuration details

# Virtual Machine Scale Set 
*VM Scale Set* -> identical and load balanced VMs that are managed together. Easier to maintain everything. This group of VMs also offers scalability, if demand goes up, more VMs are deployed. 
- Just as a ASG in AWS. 

availability set <- scale set inside 

## Extensions
Small applications that provide post-deployment configuration, patches, automation tasks, etc. 




---
### Resources
TIO - https://d6opu47qoi4ee.cloudfront.net/labs/tio/azureessentials/azurevm-tio.pdf


Gen AI TIO - https://d6opu47qoi4ee.cloudfront.net/genAI/aze/vm-arm.pdf

