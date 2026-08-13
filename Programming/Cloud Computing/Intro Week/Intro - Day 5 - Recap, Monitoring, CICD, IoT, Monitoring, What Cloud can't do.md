[[Cloud Computing]] [[Infrastructure]] [[IoT]] [[Protocols]] [[CICD]] [[Git]]
# Infra. Automation, Provisioning, Allied Tech

## Infrastructure Automation
Tools that allow the auto-configure, deploy and managed cloud resources, improving scalability, consistency and flexibility. 

Massive scale is hard to set up manually. You can use several options:
 - Chef.io
 - puppet.com -> open source configuration management and automation tool used for managing the configuration of software. 
 - ansible.com

and each cloud provider has their own infrastructure automation tool. 

Your choice depends on your particular context 

## CICD - Continuous Integration and Code Deployment 

Automates the development, testing, and deployment of applications in the cloud

Central code repositories

auto build process -> container images

Several options to set this up but a popular one is Jenkins

Jenkins -> crucial automating software development workflows, enhancing code quality and expediting continuous integration and delivery processes. Corner stone of modern devops

A cloud service is never my way or the high way, you can mix and match. 


![[Pasted image 20250523154129.png]]

The moment you do git push -> the pipeline starts in this current setup (screenshot)

## Internet of Things

Bunch of devices, equipment, machines or even devices that humans have all around them. All this devices are communicating back to a central service

Cloud has services/framework for IoT
- Amazon greengrass 
- Google Brillo

TCP -> provides a reliable and connection-oriented communication method for transmitting data between devices 

#### Practice Quiz Question: What is a network of physical objects enhanced with electronics, sensors, and connectivity for exchange of data and information

IoT

## Cloud & MS Impact

![[Pasted image 20250523155421.png]]

DNS look up -> web page

LB V1 & V2 (Microservice 1) -> redundant servers running at the same time, you can send customer group x to LV1 and group y to LV2, This is called AB Testing. Sitting on top of the inventory.

LB = Load Balancing

This servers are running on a self owned/hosted RDBMs 

LB - Redundant VMs (Microservice 2) -> Shopping cart integrated with queuing -> makes sure there's inventory and it can perform the operation. 

Containers (Microservice 3) -> Another application that handles the orders through a NoSQL database because you are working with Big Data

The Container Image Registry CICD -> Contains all the dependencies in order for the application to run, this is stored in a GitHub repo where the cloud customer can push the code into the pipeline


Serverless architecture -> you just write code and send it to the cloud and the cloud is responsible for it to work (how the fuck?)

API Gateway -> Expose the same service to web and mobile applications. Sits in front of the application to handle the security. You communicate with the server, authenticate and if successful the back end will communicate back

Console -> monitors the infrastructure

Heterogeneity at play

## The flipside - what cloud computing can't do

Progressive architecture development -> Develop your app in cloud overtime

There are many cloud providers, but there are only a few that are mature. You have really take a look at your strategy and determine whats best for you.

Enterprises have a lot of legacy applications and its hard to migrate to the cloud

Lock in might be an issue 

There are risks - legal, regulatory, business:
- HIPAA
- Data collection laws - European union demands organizations that collect data to store it inside the European union

Availability -> will the service be always online?

Unclear ROI

#### Practice Quiz Question: Legacy applications can be easily migrated to the cloud:
False

#### Practice Quiz Question: __ is where the overall architecture vision is broken into pieces and developed over a period of time 
Progressive Architecture development


# A quick recap on key aspects of IaaS, PaaS, SaaS

*Cloud Native Application* -> leverages a bunch of APIs from the cloud. Applications that are specifically designed to operate in cloud environments. 

*AWS Lambda* -> Allows you to deploy code without worrying about hardware

## Key Aspects: IaaS

Delivers on demand virtualized computing resources, such as server, storage and networking via internet

Enterprise infrastructure as service 

No single point of failure 

## Key Aspects - PaaS
simplifies application development by providing a platform and environment for developers to build, deploy and manage applications, abstracting away infrastructure concerns

Managed services

You have a console to monitor and identify application bottlenecks and help debugging 

Cloud APIs allow developers to interact with different cloud services

Runtime -> how fast is your application running 

Billing thresholds to keep tabs on the expenditure

*key point* -> you focus on your code, everything else is left to the cloud provider

Platform as a service should be used as a layer, it contains dos and don'ts

## Key Aspects - SaaS
offers software applications through the internet via subscriptions, providing easy access without requiring installation or upkeep

Allows for hosting and management of applications to a 3rd party provider

3rd party provider is responsible for delivery













