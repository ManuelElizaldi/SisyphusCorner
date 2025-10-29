# Containers vs VMs
[[Intro-Day 3 - Virtualization, Containers, Cloud Service Taxonomy]]

One machine -> multiple VMs sitting on top of it thanks to the hypervisor. Each machine has its own dependencies and libraries 

Containers sit on top of the files and libraries -> virtualize the underlying system 
![[Pasted image 20251025091857.png]]

containers are packages of software, it includes everything necessary to run the application. It does not depend on the underlying system 

*Container Image* -> the recipe 

*Container Registry* -> The repository of recipes 

*Container Instance* -> Using the image, you run an instance of the application 

# Azure Container Services

## Azure Container Registry
The same as docker hub, it's where you place the containers

## Azure Container Instances
Quick deployment of individual containers. You don't need dedicated infrastructure to use this. 

You can specify exact CPU and memory requirements for a container 

Run windows or linux containers 

## Azure App Services
Deploy containers on app services plan 

if you simply want to deploy containers, why deploy a VM? it will only  take time and effort to manage VMs

## Azure Container Groups 
Deploy multiple containers on the same host = the same as kubernetes pods 

## Azure Kubernetes Service
managed kubernetes service in azure 

### Azure Container Groups vs Azure Kubernetes Service


## Azure Service Fabric 
Managed service fabric cluster on azure
### Service Fabric


# Creating a Container Registry
Provide subscription, resource group and registry name 

Steps - package application as container 
1) Create application
2) build application as container image (docker file) 
3) build the container image (docker build command) and Push local container image to azure registry

*Docker file* -> instructions to create the image. There is a VS Code tool to do so

Docker Image is stored locally in the machine running it 

*tagging image* -> from local image to the remote location (Azure Container Registry). `Docker Tag` command

*Pushing image* -> `docker push` command 

`ducker build . -t glfristdocker:v1`

`docker images`

## Logging into the Azure Container Registry 
`docker login --username username_here server` then enter password

you get the info from the management console inside *Azure Container Registry*:
![[Pasted image 20251025174554.png]]

## Running an instance
![[Pasted image 20251026163853.png]]

After you clean run instance, it will create an instance and Azure will ask you the name, subscription, container image that it will use, memory, cores, OS type, etc. 
- Note: If you created a linux container image, you will have to choose linux in this menu. Same for windows, if you don't choose the right one the deployment will fail. 
- **When it asks you for port number -> you have to choose the same as the front end, there is currently no port mapping like in docker** 

## Deploying Container From App Service
When you create an app service you can choose to publish from docker container 

In a app service plan you can only deploy container or code, but not both. 

You can choose from various image sources (registries)


## Container Groups
Collection of containers that are deployed on the same host machine. 

Deploy using ARM template or YAML file 

![[Pasted image 20251026170049.png]]


