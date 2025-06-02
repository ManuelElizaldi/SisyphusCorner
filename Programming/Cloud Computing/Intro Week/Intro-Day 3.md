2025-5-21
[[Virtualization]] [[Cloud Computing]] 
# Introduction to Virtualization

*Virtualization* -> Break down a part of your server into smaller chunks. You virtualize the computing resources, servers, networks and storage. This is a dynamic flexibility.

Virtualization lets you improve the utilization of the current hardware

*Hypervisor/VMM* -> Is the software used to monitor the VM instances

Create more from limited resources

Virtualization stack:

![[Screenshot from 2025-05-21 12-02-57.png]]

## Characteristics
*Business perspective *
- More computing resources on demand
- Elimination of upfront monetary commitment
- Ability to pay for computing resources

*Technology perspective*
- Partitioning -> one physical machine becomes multiple VM instances
- Isolation between virtual instances -> Improves security and stability
- Encapsulation -> a virtual machine can be represented and stored as a single file, making them easy to copy and move 
- Flexible -> You can configure and reconfigure to match business needs


#### Practice Quiz Question: The primary goal of virtualization in the cloud is to:
Optimize resource utilization and flexibility

### Drawbacks

Amplified physical failures -> if the host goes down, it brings everything done.

Virtualization is hard, you need to have certain skills to set up this system

Complex *Root Cause Analysis* -> systematic process used to identify and address the fundamental reason for a problem 

How do you know you want x amount of virtual machines? It is hard to determine the exact number.
- It always starts with a guesstimate

Each layer impacts performance 

Some apps don't work well in a virtualized environment 

Licensing fee

Does virtualization guarantees more utilization?

#### Practice Quiz Question: Which of the following is NOT a drawback of virtualization?

Supporting multiple applications and operating systems in a single physical system by partitioning the available resources

## Evolving from IaaS to PaaS

If you are looking to increase utilization, creating a virtualized/partition does not guarantee this. In the middle section of the screenshot, you have 4 VMs that are currently not being utilized. Its still a static model (fixed pre-planned capacity). In the middle we have 5 applications and there is no guarantee that all resources will be utilized

What you need is a dynamic model where apps are swapped in and out depending on the demand

![[Screenshot from 2025-05-21 12-41-12.png]]

#### Practice Quiz: Which cloud service model allows users to rent virtualized hardware resources on a pay as you go basis
IaaS

## Next Gen Virtualization

Dynamic swapping needed - Create on demand buckets

Containers -> Application focused bundling. You store all the dependencies inside and deploy. This is faster, has small footprint and can be easily shared. High portability.

# Container vs VMs, PaaS & Service Taxonomy 

## Container vs Virtualization

![[Screenshot from 2025-05-21 12-55-00.png]]


In the VM, there is a lot of duplication, which brings down efficiency - storage, performance.

The containers allow flexibility 

The docker contains an image that has everything you need to run an application. You can inherit all these dependencies and run it 

*PaaS* is essentially a runtime. If all of your apps need the same OS image to run, containers are a better option.

VM can have a choice of OS, if you need windows, linux, etc -> this is a good option for *IaaS*. 

Containers have less isolation among them

VM has a higher isolation

Containers are faster, VMs can be slower 
- If your business needs faster TOT, containers might be a better option

#### Practice Quiz Question: What is the level of isolation between virtual machines in virtualization

Higher isolation

note -> why would you want higher isolation?


Determining which to use is contextual. It all depends on the architecture and the type of application. It also depends on your elasticity rules 

delta t

#### Practice Quiz Question: Which of the following is not an advantage of containers compared to virtual machines?
Enhance isolation

## PaaS Overview

You need underlying infrastructure to be effective. If you need additional hardware, you will need to add hardware to your cluster and this is where the underlying infrastructure comes in to help 

Abstracts the infrastructure layer completely 

Provides monitoring at two levels:
- Infra level (infrastructure)
- Application -> monitor run time 

Node runtime/Node.js -> allows developers to run javascript code on the server

## Cloud Services Taxonomy

Jenkins -> open source automation server, optimizes the CI/CD pipeline. It automates essential tasks such as software building, testing and deployment

![[Pasted image 20250521131846.png]]

Storage as a service -> google drive

Information as a service -> BI tools 

This picture is not complete, you can add even more solutions. 

Business process -> little processes that are needed for your operations, one example could be payment processing 

#### Practice Quiz Question: What is the foundation of cloud service taxonomy, categorizing services into three primary models?

SaaS, PaaS and IaaS 



