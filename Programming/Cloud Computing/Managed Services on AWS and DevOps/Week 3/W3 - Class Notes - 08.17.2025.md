[[Container]] [[Virtualization]]

# Containers vs VMs

![[Pasted image 20250817093121.png]]

benefits of using a container: speed, scalability, portability, efficient, dev ops friendly.

But as I read in an article, if you want to test how the app interacts with different OS systems, a VM is better.

VMs have a higher resource utilization. Containers use very low resources, that's why you can have multiple in a single machine. 

Since containers don't use much resources, they are better fitted for micro services. 

Boot time is also faster on a container. 

You need to maintain all VMs inside your server. Patch the OS binaries, libraries. Also, you have to make sure the right version of the OS can talk to your app. 
- VMs run on the hypervisor - this emulates the physical resources of your computer 

Containers run on a Container Engine - they share the kernel but are isolated at the process level 

VMs are more isolated since they run on a hypervisor which simulates the kernel

Containers allow you to build once and run anywhere. The container can be ubuntu and run on windows machines

## VMs and Containers Work Together
In any business you will see both working together. Each has its own use cases. 

Containers work together with VMs. 

You can run a container on top of a VM

![[Pasted image 20250817093710.png]]


## Docker and Orchestration
Docker is a Container Engine, here you build, package and deploy your containers based on images 

Kubernetes, ECS (AWS), AKS (Azure), GKE (Google) -> These are orchestration tools, meaning, they help with scheduling, scaling, deployment, load balancing, self healing, etc.
- They help manage your cluster of containers to ensure they are deployed properly and running. 

## Demo
Docker Desktop (win or mac)

### Building from scratch 
install docker on a server (vm) - there are commands you can follow | wget link for example. 

command -> `vi dockerfile` | creates a text file , you then paste this file:

### Docker file


![[Pasted image 20250817095741.png]]

An image is not a full fleshed operating system | only the kernel is installed 

cloud engineer/CCOE + cyber security team -> docker image -> container registry -> app team -> launch stack

AWS Elastic container registry (ECR) -> share and deploy container services 
- allows roll back 

## Pushing a container to a ECR registry 
AWS CLI and Docker are required 

You authenticate from your EC2 to ECR 

tag image - identifier 

image can be in different regions in a matter of seconds | very high availability 

---
*Reference*


[Containers vs VMS](https://cloud.google.com/discover/containers-vs-vms?hl=en)

https://www.bmc.com/blogs/containers-vs-virtual-machines/

https://docs.docker.com/get-started/docker-overview/

https://docs.aws.amazon.com/AmazonECS/latest/developerguide/create-container-image.html