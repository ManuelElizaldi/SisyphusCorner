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

users -> application load balancer -> web -> LB (Internal) -> App -> DB 

### Difference between HA and DR 

(High availability and Disaster recovery)

Disaster recovery -> primary DC and a fail over DC. Annual DR exercise.
- Fail over DC = expensive insurance 
### Cost - ^ Resilient, ^ Cost:
SDLC (Software development life cycle) -> optimize for cost, test, prod. Where are you going to optimize for cost? 
- Single AZ? Smaller Instances? Shut down during weekends? There are multiple ways you can optimize for cost.
- Test your instances, then go into production. But if things go wrong, its easy to revert. 

In cloud there's no up front cost, you have OpEx here (pay as you go). Optimize within this parameter. 
- Where are you chocking? Memory, compute, networking? If you are not chocking you can lower the specs, don't create a large instance if its not needed. 

*1 way door decision -> hard to reverse | 2 way door -> easy to reverse. AWS is a 2 way door*

Use metrics to decide where you are going to optimize. 

Start small, and grow gradually based on metrics

### Scaling 

DC -> Vertical
AWS -> Horizontal


Every application is different, so there's no recipe, but a constant is ->start small. 

## IAM

AuthN -> Who you are? Credentials
- Presenting credentials 

AuthZ -> What can you do? Permissions 
- You can create user groups -> based on themes, tasks, etc. It is easier to manage groups than 1000 different users
- Personas: Appdev, Data Scientist, Net Admin, Sysadmin, each persona has different permissions 

*What is authenticating you when you log in?*
In any app, you are authenticating against a Active Directory or LDAP - Identity Store

In AWS, IAM = Active Directory 

AD Groups -> user id 

Permissions are given by IAM 