[[Docker]] [[Containers]] [[Kubernetes]]

# Docker Ecosystem
With Docker you can standardize code, ship it faster and improve resource utilization.

With Docker you get an object that can run anywhere. 

## Creating a Docker Application 

You have your OS and on top Docker (daemon). When you instruct the Docker client to create a container:

1) it checks local disk for the container 
or
2) Checks Docker Hub - a git hub for containers 
	1) Most companies have a private repository

Once it has the container it starts it - this container has CPU, Memory, Network assigned to it. You need to set the upper boundaries to avoid it growing and consuming everything 

Kubernetes set the upper bounds 

## Pods - Kubernetes & Tasks - AWS
You can have 1 or many containers inside a pod. Here you determine how much resources you can use.  

AWS calls it a *task*, works exactly the same

The containers inside a pod/task live and die together. They start together and are terminated together. 

For pods and tasks, its better to have *horizontal scaling* - it's not recommended to have all containers in one pod, its better to have small instances that are fanned out. 

The load balancer can distribute traffic across pod instances

## ECS - Elastic Container Service 
The equivalent of Kubernetes in AWS

Helps you manage the scaling process of pods/tasks 

You save pod templates and then start them. It takes milliseconds to start a docker


