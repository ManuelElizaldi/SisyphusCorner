[[Containers]]
# Introduction

Hypervisor - creates machines and each machine 'thinks' it lives on the OS. The hypervisor pretends its a kernel for the guest OS

You have a Host OS and Guest OS (virtual machines)

![[Pasted image 20250806192510.png]]

You can sit apps on the guest OS - but these apps have dependencies - libraries, software, environment variables. *problem* you can't hand over an app to another machine and expect it to run perfectly. 

*Images* were created - a snapshot of everything needed to run an app in a virtual machine. Very bulky because it contains the OS  and OS utilities. Images capture everything, files, environment variables, profiles, dependencies, anything within that machine is captured. You can hand this over to another machine and run a Virtual Machine based on this. Similar to AWS's AMIs. 

*new problem, these images are bulky* -> Containers are born from this problem. 
### Mutable vs Immutable

*Mutable* -> Designed to be changed after deployment. 

*Immutable* -> Not designed to changed.
- Virtual machine images are expected to be immutable

## Container Images

*Docker* -> Container engine 
- There is another one called rket 
![[Pasted image 20250806193438.png]]

Containers don't have an OS and OS utilities, its design is to be very lean. Docker is a daemon that runs each container as a process. Docker passes the instructions of the application (process) to the Host OS. The only requirement is that the OS of the container must be the same as the Host OS. 

### Process Level Isolation -> Containers
### Machine Level Isolation -> Virtual Machines

A Virtual Machine Images weighs -> ~750 MB
A container weights -> ~50 MB

# What is a Container 
Unit of software that packages all the code and all the dependencies. 
- System tools, libraries, dependencies, everything and anything that allows the unit of software that allows it to be very reliable. Everything that it depends on is inside 

This grants us:
- Reliable
- Quick Deployment - better capacity scaling

This container is built for a specific kernel - the docker engine 

Reliability and quick deployment allows us to *save money*
- reliable - avoiding inefficient developing 

### Why quick deployment allows cost savings? - Capacity Planning

*Capacity Planning* -> You have to choose capacity - how many units are you going to be able to create?
- If you are serving under capacity - you can remain as you are 
- But if you are serving over capacity - it is hard to scale depending on the nature of your business 

If you don't capacity plan properly, your customer will suffer could possible go to the competition. 

Base level capacity - you decide what this is - this level will determine your under and over capacity. 

the objective is to get dollars for every dollar you put it. 

*Provision Time* -> time it takes to fully deploy a service

Containers allows for smaller provisioning times 

the higher the provisioning time the higher the cost 

## Container Layers
scratch layer - 0, nothing

You can build containers that inherit layers from other containers. Like Lego pieces, you grab what you need/want. 

*Docker Hub* contains a 'marketplace' for containers. 

If you want to scale a container, you can pull containers from the Hub/repository and deploy where you want. 
## Docker
Docker is a container and image manager. When you install docker in your host machine you can manage the images and the containers. Docker uses simple CLI commands in order to manage everything. 
# Kubernetes 
Container orchestration

Pod -> stores many containers 

