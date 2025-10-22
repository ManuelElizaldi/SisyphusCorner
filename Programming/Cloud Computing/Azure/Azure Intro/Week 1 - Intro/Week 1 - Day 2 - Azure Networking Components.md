[[Network]] [[Cloud Computing]] [[Azure]]

# Networking Components
3 tier architecture - 3 different layers 

presentation layer -> web app 

middle -> business logic

data layer -> data storage 

*Based on this tier architecture you can understand the components*

![[Pasted image 20250923170709.png]]

## Azure Virtual Network
Allows you to create a private network to deploy resources. Provides isolation. You can communicate with outside resources but this needs to be set up. 

This handles the inbound and outbound traffic. 
## Creating a Virtual Network
Create a range of IPs - 10.0.0.0 - 10.0.0.255
- You can create 1000s of IP address ranges in a subscription

Each resource goes inside a subnet 
- Each subnet has its own range, but this range must be within the private network range i.e. 10.0.0.0 - 10.0.0.255
- You could assign 10.0.0.0 - 10.0.0.63 for example to subnet 1 
- Then subnet 2 -> 10.0.0.64 - 10.0.0.127 
	- Each subnet has its own range 

Azure reserves 4 IPs to do their set ups. 

Each resource, within the subnet has its own IP from the range determined for the subnet. 
### NIC - Network interface card 
Part inside your computer that lets you communicate with the outside world. When you deploy a VM the IP is not assigned to the VM but to the network interface card. 
- **You can assign multiple NIC to a VM, this will allow it to have multiple IPs**

## Load Balancer
Accepts request from user and then its traffic is diverted to VM1 or VM2.  

Sits within the subnet and can be public or private. 
### Internal load balancer - private
The VM1 and VM2 inside the first subnet that is serving the web app  can communicate with another set of VMs that are controlling the middle layer and the middle layer can communicate with the data layer as shown in the picture above. 

This load balancers are private so only explicitly set IPs can access them. 

### Load Balancer options
Load Balancer, Application, Traffic Manager, Front Door

## Firewall
Connects to the public load balancer and traffic to the Virtual Network goes through there

## Network Security Group 
At the subnet or NIC level, handles inbound and outbound traffic. It determines which IPs can access

VM = NIC (network interface card)
4 Different combinations: 
- NSG at the subnet level and VM level
- NSG at the subnet level and no VM level
- NSG at the VM level no subnet level
- No NSG 

### Pros and cons of the different NSG settings
At both levels - NIC and Subnet:
inbound -> firewall -> NSG at subnet level -> NSG at NIC
NSG at NIC -> NSG at subnet -> firewall -> outbound 
- Requires more maintenance but you have more control over the traffic. 

NSG at subnet level controls traffic for all VMs -> lower maintenance issues, one SG controls all of the VM settings. 

NSG at VM level -> also requires a lot of maintenance since you have one at each VM but will give you more control over each VM 

![[Pasted image 20250924153637.png]]