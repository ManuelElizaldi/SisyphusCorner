[[Azure]] [[Load Balancer]] 

# Load Balancer
Distributes inbound traffic between VMs for scalability and high availability 

Works in layer 4 of OSI stack -> supports TCP and UDP protocols 

It can be used for internal or external needs

Support for multiple IPs and ports 

Standard Skew ->  

Basic Skew -> VMs need to be in the same 

Support both inbound and outbound scenarios
- outbound -> VMs in backend want to connect to the internet, you can use the load balancer to set up the outbound 
- inbound Scenarios 

Supports IPv6 addresses 

# Load Balancer Types
*Public load balancer* -> Uses a public IP address because it accepts traffic from outside and distributes this between the back end VMs. Backed VMs don't need public IP address because the public load balancer is the 'lobby' to the internet traffic 

If a backend VM wants to communicate with the internet, the VM can use the application load balancer as bridge. It uses the application load balancer's IP address to communicate. 
- ALB translates the private IP to public 


*Internal load balancer* -> only works on private IP address and it's deployed inside the Virtual Network 

## Creating a load balancer
Basic set up, similar to other resources. You determine the subscription and the resource group. 

You select the type -> internal or public. 
You choose the vnet and subnet 
You also choose the IP address -> static or dynamic 
- static -> you determine the IP | dynamic -> one is given from your subnet range 

*Tier* -> you determine if you want the load balancer to be cross region 
![[Pasted image 20251007165536.png]]
If it's cross regional, the load balancer distributes traffic between regions and their load balancers 
- There are other methods to distribute traffic between regions besides this one. 

### SKU -> basic vs standard 

If you use the Standard Load Balancer SKU -> The public IP address will be Standard
If you choose basic, then it will be basic  

# Rules in Load Balancer
4 components of the load balancer rule:
1) front end IP -> public IP
2) Backend pool -> Group of VMs (target group)
3) Health probe -> checks the health of the VMs 
4) LB Rule 

Rules are set up inside the Load Balancer management console

Your load balancer has a default public IP address (if it was set up as a public LB).

You can set up back end pools as well inside the LB management console
- You decide which VMs are included in the pool, you don't need to add all of them. 

## Health Probe
This is set up inside the load balancer management console. 

The *health probe* monitors the back end pools are running.
- It uses a communication protocol through a specific port and it continuously hits these VMs
	- If you choose the HTML protocol, you choose the path you want to hit
- Frequency is also determined here 

*Unhealthy threshold* -> Consecutive fails. You determine how many consecutive failures are the threshold, if you reach this point actions can be taken.  

# LB Rule Components 
![[Pasted image 20251008180338.png]]

There is an algorithm that decides where the request goes, in the default algorithm the load balancer looks at 5 things -> source IP, Destination IP (front end IP), destination port and protocol. It creates a hash table based on these values and decides where to send the request. 

Any load balancer rule needs the front end IP (where requests first land) and the port (where are these request landing)

Then it will send the request to the backend pool (which is also needed for the rule) and from which port are these requests travelling through. 

You also add a health probe to the rule to ensure the backend pool is working. 

You also need a Front end port and back end port 

*Network Address Translation* -> When the request gets to VM1, the IP get's translated into the IP of VM1:

| source:      | 120.0.0.0:100 |
| ------------ | ------------- |
| Destination: | 10.0.0.0:80   |
*Direct Server Return* -> The response does not need to go through the LB again, that would just slow things down, so the VM1 sends it directly to the user through Direct Server Return. Here another Network Address Translation happens. 

| Destination: | 120.0.0.0:100 |
| ------------ | ------------- |
| Source:      | 130.0.0.0:200 |
Even though it does not go through the load balancer, the response is translated into the Front end IP 

## Network Security Group Modification
Once you create a rule you have to make sure the network security group allows traffic through the port specified in the load balancing rule

*In the video, the professor had not opened the port once he created the rule. So when he accessed the VM, he was not being accepted. Once he opened the port in the network security group it worked.*
- you don't open the front end port number, you open the VM port 
# Load Balancer Algorithms | Session Persistence 
**5 Tuple algorithm** -> The one above in the graph. It uses Source IP, source port, destination port, destination IP, protocol and create a hash. 
- This is the default algorithm

**3 Tuple algorithm** -> useful for instance persistence. It uses source IP, destination IP and protocol

**2 Tuple Algorithm** -> Source IP and destination IP, the request always goes to the same machine. Same as the 3 tuple, it is useful for instance persistence. 
## Session persistence | There's 3 settings:
*none* -> 5 tuple algorithm, users are directed to different VMs

*client IP* -> 2 tuple algorithm, session persistence

*client IP and protocol* -> 3 tuple algorithm, session persistence 

# VM SS (scale set) ARM Template using GenAI
Objective of TIO -> Create a VM scale set and a Azure Resource Manager template
![[Pasted image 20251019184959.png]]

In order for the auto scaling to work I had to go to resource providers and register for `microsoft.insights` once I had that in my account I could enable the auto scaling for my scale set. 

I tried deleting and seeing if the VMs came back up but they didn't, until I registered for microsoft.insights

My VMs are launching with an 'unhealthy tag', troubleshooting I found: that the status was Running and the Provisioning State is succeeded, therefore the Health state: Unhealthy means that there is something wrong with the health check of the application load balancer 

- also when I hit the public ip of the vm get this `**52.146.18.68** refused to connect.`
- A potential issue is that my orchestration mode is flexible inside the auto scale group/scale set
- The load balancer is doing its health probes through port 80 with TCP 
#### According to ChatGPT
My application was not working because Python's default HTTP server listens to port 5000 or 8000 not 80. So when we set up the health probe for port 80 it was not reaching it 

VMs can be running and operational but still marked as unhealthy if the load balancer can't reach them 


**Load balancers will never forward traffic unless the health probe is marked as Healthy**
### Flexible Orchestration
Gives you more control over how the scale set scales. Azure doesn't auto scale, rather you do it through APIs, azure does not auto recreate VMs

