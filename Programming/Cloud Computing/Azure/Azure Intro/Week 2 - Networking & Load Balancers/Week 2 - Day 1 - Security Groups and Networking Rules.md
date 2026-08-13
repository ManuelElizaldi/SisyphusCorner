[[Network]] [[Azure]]

# Network Security Groups
Set of rules that handle inbound and outbound traffic 

It can be applied to the instance (NIC) or subnet level 

Any inbound traffic hits the firewall
- Firewall only can live at the subnet level

Work at the layer 4 and supports TCP, UDP and ICMP protocols    

## Setting up a Security Group
After creating a VM, you can go to the Network Security group resource management console. You select the subscription and resource group where it will live. You also name it. 
- **To check the inbound and outbound rules in a VM you can check the Networking section**

After creating the Security Group you have to attach it to a resource.  

The security group will have default rules set up that can't be deleted but you can overwrite them 

For every rule - 5 tuple rule:
- Source 
	- Source port number
- Destination
	- Destination port number 
- Protocol (TCP, UDP, ICMP)

*Priority* -> lower the number, higher the priority. The rule with the highest priority get evaluated first. In the screenshot below, the first rule to be evaluated is the AllowVnetInBound with priority 65000. If all of its conditions are true, the next rule is not evaluated.

### Default Inbound Rules
![[Pasted image 20250929173911.png]]

*Inbound Rule* 
- source -> Who is making the request
- destination -> subnet or NIC  
	- For example in the screenshot above, rule 65000 says that there can be traffic coming from the Virtual Network and the destination is the Virtual Network as well. This means that 1 subnet is communicating with another subnet inside the Vnet 
	- For rule 65001 the source is the Load Balancer and hitting anything is allowed 
	- For rule 65500 if you get traffic coming from anywhere the request will be denied. 
		- So basically, default rules only allow inbound traffic from within the Vnet or the Azure load balancer 

*Outbound Rule*
- Source -> subnet/VM 
- Destination -> Who is getting the response 


### Default Outbound Rules
![[Pasted image 20250929174908.png]]

Communication within the VNet is allowed 

And the resources can communicate with the internet 

## Associating SG to Subnet
Inside the Security Group management console you can select the Subnet menu and there associate the SG to the subnet.   


# NSG Flow Logs
This captures any traffic that flows through the network security groups 

Disabled by default 
- basic info v1 
- more details v2 

All logs are stored in a storage account. The folder structure is automatically set up. The folder structure is structured efficiently to capture all the info generated from the security groups

The output will be in Json format 

**NSG is free of cost, but pay for each Gb that is inside the storage account**

# Creating Inbound Rules
In *add* button inside the Inbound Rules. 

You need to define Source and the port ranges

Then you have to define destination and destination port ranges 
- The destination will be VM or subnet depending on where you attach it 
- Bellow destination, you can also choose Service instead of defining a port range. The Service drop down offers a list of common ports like: HTTP, HTTPS, MySQL, etc. 

You also need to choose the Protocol 

Action -> allow or deny

Priority -> between 100 and 4096  
#### You can restrict a range from IP Addresses 
Useful for restricting access to only your enterprise IPs

## Service Tag
Inside Source:
Pre-defined IPs that come from a specific service. For example the Virtual Network tag includes all IPs coming from the Vnet

You can even filter from a specific region, for example, only storage accounts from east US 