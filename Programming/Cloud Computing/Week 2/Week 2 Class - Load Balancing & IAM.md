Avoid single point of failure -> build resilient systems. 

*Hypervisor* -> software layer that enables multiple VMs to run on a single machine, sharing resources

*OSI (Open Source Interconnection) 7 layer model* 
![[Pasted image 20250615095139.png]]

The instructor talked about how back in the day they had to build 2 VMs hosting the app. The issue here was that there was 2 DNS with the same name (www.example.com) and each had a different IPs, but this is not a proper way of building an app. If one instance went down, there was no way of properly redirecting traffic to the working instance 

### Data Center 

users -> DNS -> VIP (F5 company) -> VM1, VM2
1. Here we do have intelligent load balancing:
	- Different algorithms to distribute traffic
		1. Round robin
		2. least connections 
2. Health probes -> determine what instance is health and which is not 

*We do this to achieve high availability*

### AWS

Regions and AZ's -> inside each regions there's AZ, in average 3 AZ.

AZ is spread across MAN with a radius of ~60 miles, you have 3 availability zones that are spread intentionally to cover a huge area, but also, if there's a natural disaster, you'll have another AZ to rely on. 

When building a high availability (fault tolerant architecture) you have to be intentional in selecting the right AZs

Users -> DNS -> FQDN AWS LB (SD appliance) -> Target group (VM1, VM2)


### Can the load balancer handle a spike in traffic? 
If you delegate this to AWS, you can scale. The only thing you have to worry is having the right amount of instances running.  
- Netflix runs on AWS -> how can Netflix predict the demand? It is really hard to predict for a new show or new season, therefore you need something that can dynamically scale based on inbound traffic 

In regard to how much instances are you going to open -> you have to use *metrics*! Metrics are your friend. 

### Start with backend
Spread instances across AZs

High availability = Multi-AZ, don't develop without this! Design an architecture that takes advantage of AZs
- Subnet = AZ 

### Launch Template 
Reusable template to launch VMs, the availability zone is left out blank so that you can decide where to launch it once you are working on the actual launch.

#### Script as part of the template:
In user data, you can have a script that handles all the bootstrapping.
Bootstrapping = configuration management 

### Health Checks
Make sure you create the right amount of health checks and intervals so that you don't bother the performance of your server. This health checks are constantly being performed by the load balancer. 

You can also add these features in a public facing application to avoid DNS attacks, SQL injections, etc. These features filter out unwanted traffic
![[Pasted image 20250615100119.png]]
### Two Application Load Balancer Architecture

users -> application load balancer -> web -> 

