[[ECS]]
# AWS ECS
Containers are horizontally scaled 

Managed Kubernetes - you give me the container and I can manage everything else

## How it works
Load Balancer is needed + its target group -> inside the target group you have EC2 instances. 

AWS ECS can also create the set up (load balancer + target group)

AWS can access a Private Ducker Repository 
- You create the image from a host PC and push it to the private repo. The host PC needs docker 

You also need to specify the ASG (auto scaling group) -> if CPU > 80% + if CPU < 80% - -> but what capacity is it adding?
- *Added capacity = Task (pod)* -> group of containers. 
	- For example, a pod contains 2 containers (derived from their respective images) they both live and die together.  

So, the ASG is adding tasks/pods

> [!NOTE] Task vs Pod
> Task is refereed to a group of containers in AWS. In Kubernetes this is referred to as a Pod. 

## How many tasks per EC2?
more tasks = larger machine = reduced elasticity - vertical or horizontal scaling? 
- *There is no right or wrong, depends on the application.* 

*If you adopt a horizontal scaling strategy*, then the EC2 instances need to be as small as possible (reduced cost benefit as well) and provide small tasks on each EC2. 
- Try to have a 1 to 1 mapping - 1 EC2 1 task - this is per AWS best practices. If you can do this, then go for 1 to many relationship but this will make the system a bit less resilient 
![[Pasted image 20250820190240.png]]


## Fargate
The new release of ECS - you can specify everything and it will manage it on your behalf 

This managed service can help you set all the above easier 

Fargate allows for code to infrastructure 


# ECS TIO




