
Workload types:
1. steady state - predictable:
	1. internal applications: HR systems, wiki pages, confluence site, company org apps
2. Spiky - Unpredictable 
	1. Thanks giving sale, Netflix, amazon, etc. 

NFRs - App SLAs (RTO/RPO)

Always design for failure -> everything fail at some point. 

### Steady state set up:
This is predictable demand, you will always keep a minimum of 2 servers 

AZ1: rack -> Physical server -> Hypervisor (VMware / EC2) -> VM (O/S + File system) -> Apache httpd/IIS 

AZ2: rack -> Physical server -> Hypervisor (VMware / EC2) -> VM (O/S + File system) -> Apache httpd/IIS 

*Fleet management* -> You are managing the fleet of servers -> ASG min 2, max 2
- Using launch templates 

## How Autoscaling know when machines fails? When it know when and how to add servers

### Spiky workload setup
Harder to determine how many servers 

DC (data center) -> on prem -> over provision. Always. There are many risks if you fail. Bring extra capacity as insurance. But in a cloud environment you should not over provision. This is just giving free money to AWS

set up:
Users -> API gateway -> LB -> web -> app -> data base

When determining the best strategy, first you have to guesstimate, then use monitoring to determine what would be the best choice. *ASG* allows you to use metrics as triggers to scale up or down. 

![[Pasted image 20250622093631.png]]


### How to build this
Always start with the Architecture diagram before building.
![[Pasted image 20250622093805.png]]
You can have a ASG in the web server and the app server 

![[Pasted image 20250622094640.png]]

Databases only accept traffic incoming from subnet 2 and 5 
###### Make sure to fully understand AZ and subnets:


Tagging is important so you know what is what 

In the ASG *balanced best effort* is a function/feature that allows you to launch instances in a healthy subnet/AZ and also balance the instances between each AZ 


min desired capacity, the least amount. Then you set up the max desired capacity and how it will scale up to that number:
- by CPU usage
- by inbound network 
- etc..
- You can also create your own metrics 

Don't worry too much about the *max desired capacity*, you can always change this quickly 

Don't manually modify instances created by the ASG, let the software do the work, look at the tag value:
![[Pasted image 20250622100704.png]]

if you perform any manual intervention, the ASG will think something went wrong.

## Auto Scaling Policies 
###### make sure to understand the differences between max desired capacity and minimum in the ASG and how it interacts with predictive scaling

## AMIs
Verified providers -> it means it goes through AWS certification process so that you are using a safe OS.


There are also firewall OSs. For example Paloalto firewall can be a virtual appliance that can be attached to your VPC 

![[Pasted image 20250622102119.png]]
In real life, companies create their own Golden Image -> meaning, its your own OS with the necessary customization for you app. 

##### AMIs update 
AMIs don't stay constant, they are constantly being updated. This will cause the instances to update. 

So your *golden image* should also be updated. 

##### Amazon Image Builder
There's an AWS service that allows you to build an image

### Instance Refresh - AMI Software updates  
You can start an instant refresh with different approaches. You can refresh and then terminate, or keep the instance. There are several approaches that you can choose. You can also launch 'new' instance, take one of the old ones and so on until it refreshes everything on your feed. 

Settings from AWS:
![[Pasted image 20250622103222.png]]


1. Rolling updates 
	1. You remove servers from your fleet until all instances are updated. 
	2. This is process intensive

2. Blue green approach 
	1. Allows you to roll back to previous software
	2. You are stopping traffic to once instance 
	3. This is a little more expensive for a short time - it is a bubble cost, but after you go successfully live, you can terminate blue. When to terminate is the big question. 

![[Pasted image 20250622103637.png]]

###### low maintenance window for Microsoft and AWS 
###### Ask Chatgpt about blue green instance refresh 





