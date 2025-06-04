# IaaS, Degree of Abstraction
## Core Building Blocks of Compute

Instance
- CPU
- RAM
- Disk
- OS
- Networking 
- Application Configuration
	- If its a web app, ports to handle traffic

All of this is a VM instance

### Compute - IaaS - EC2 (AWS)

![[Pasted image 20250603164018.png]]

You manage Application, data, runtime, middle ware and OS

Compute is the most important -> CPU & Ram
- This is EC2 (Elastic Compute Cloud)

Storage


Networking

Scaling


## Availability Zone - Regions

Group of data center, isolated from each other. Provides fault tolerance. If there's an outage it wont impact other data centers. 

Data center -> contains components that customers can use 

Availability Zone (AZ) -> One or more discrete  data centers with redundant power. The components of an AZ:

- Environment layer -> Somewhere where there's few natural disasters
- Perimeter layer -> Physical security layer, guards, gates, etc. 
- Infrastructure layer -> Data center building with the necessary equipment to provide support for the operation (back up power, HVAC, fire suppression, etc.)
- Data layer -> The most critical point, the servers/computers

![[Pasted image 20250603165416.png]]

They are separate from each other by a significant distance (100 km/60 mi)

Secure, fault tolerant, highly available and scalable 

Regions can be country, state or city

Multiple availability zones make up a region

## AWS Local Zones

Type of infrastructure that places compute, storage, database and other select AWS services close to a large population or industry. Single digit latency.

## AWS Wavelength Zones
embed AWS compute and storage services within 5G Networks, providing mobile edge computing infrastructure for working with applications at low latency.

Designed for telecommunication workloads 

- Edge computing -> Brings data processing and storage closer to where its generated. Instead of relying on centralized cloud servers. 
	- Reduces latency


Zone's core principle is to be able to deploy applications for specific requirements. Because of this, new zones might emerge in the future. 


# Understanding the Real Cloud


Technology stack can be thought as a burger -> every layer offers something. 

Technological stack -> technology infrastructure and software components that work together to support the application's functionality

## API layer - The Real Cloud 
API layer acts as the interface to the various services that are in the availability zone, such as compute, storage, networking and managed services 

API layer -> is like a bridge that lets customers and programs work with or build on AWS services. 
- It helps developers work with cloud resources through code, and operations engineers can monitor the services.
- THIS is the real cloud 

*Ergonomic APIs* -> They have the ability to manage all the aspects of data management. It's easy to use.
- Although there's debate between developers about if they are truly ergonomic

## How to interact with the API layer:

Management Console Facade -> comprehensive dashboard that provides role based access control for enhanced security

Tools and SDKs -> Developer toolkit comprising tools, libraries, and documentation for crafting software tailored to specific platforms. 
- Toolkit that allows easier building

Command Line Interface -> can also be used to interact with the API layer. Usually the go to option for developers


![[Pasted image 20250603171933.png]]

Usually the 3rd party tools are using the CLI in the background

Cloud provider offers many options to interact with the real cloud - API layer. 


#### Practice quiz question: What is the AWS management console?
Web based interface to manage AWS resources

#### Practice quiz question: If an application is deployed in a region and availability zone as per the user proximity, it will help
in reducing network latency

#### Practice quiz question:According to module "Understanding the real cloud" which of the following statement is TRUE?
CLI & SDKs (over management console) are preferred choice of developers / administrators / cloud engineers as it provides stability and helps in manage large volume of workload.

and

Management Console of any cloud provider may go over UI changes frequently for aesthetic reasons however underlying concepts for the services doesn't change with the same frequency.

g