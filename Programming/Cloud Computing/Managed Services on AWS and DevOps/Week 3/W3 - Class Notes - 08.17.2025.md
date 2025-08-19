[[Container]] [[Virtualization]]

![[Pasted image 20250817093121.png]]

benefits

speed, scalability, portability, efficient, dev ops friendly

![[Pasted image 20250817093710.png]]


## Demo
Docker Desktop (win or mac)

### Building from scratch 
install docker on a server (vm) - there are commands you can follow 

command -> `vi dockerfile` | creates a text file , you then paste this file:

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