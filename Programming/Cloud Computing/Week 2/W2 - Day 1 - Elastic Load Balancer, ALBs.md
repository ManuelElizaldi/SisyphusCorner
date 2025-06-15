
## AWS Elastic Load Balancer (ELB)

A way to look at load balancers is -> when you arrive at a restaurant, the host will lead you to your table. In the same manner, you distribute users to the according servers. 

Traffic distribution algorithms

Scale is very important. 

### Features

Distributes traffic among your EC2 instances among other target types.

Instances can be in multiple availability zones. 

Elastic, so it doesn't have a point of failure

Health check configuration -> The load balancer needs to know where to direct traffic to avoid a server crash

Internet or internal -> Basic categories of service. Internal load balancer? -> If you have an application that interacts with another online application, you will need to be able to direct traffic as well.

### From a deployment perspective:
You get a highly resilient application. But the resilience comes from the topology, not the service it self. 

You determine the traffic distribution rules

Canary deployment -> lets say you want to test a new feature, you can direct a certain group of users to that instance. 

It supports 3rd party applications and support identity provider integrations (security)
- You can analyze individual packets that are incoming to the server to avoid malware

The load balancer can also help with Oauth authentication

#### Practice Quiz Question: Primary purpose of AWS Elastic Load Balancer is to:
Distribute incoming traffic across multiple EC2 instances

### ELB is the umbrella concept, types of load balancers:
Application load balancer (ALP)

Network load balancer (NLBB)

Gateway load balancer (GLB)


### Summary 
Load balancers are open source and play a crucial roll in any application. 

Load balancers distribute incoming traffic or client connections to the target server

AWS ELB can send to EC2 instances and other targets 


#### Practice Quiz Question: Types of load balancers:
Application, network and gate

## Application Load Balancers (ALB)

Looks at the contents of the request (HTTP Header, urls, cookies), makes intelligent routing decisions based on application data (what's inside the request).

The application load balancer can route to different parts of your website to different servers. 
- *if you have a downloadable object on your website that is accessed through a hyperlink, the application load balancer will send this request to the storage layer and return the file the user requested*


[[Load Balancer Diagram]]

![[Pasted image 20250610175336.png]]

It can handle HTTP and HTTPs Traffic 

The load balancer has components:

Nodes -> Each node has a listener, the listener monitors incoming *connection requests* with designated protocol and port
- Definition -> server among a group of servers, receiving and handling network traffic. It evenly distributes traffic to a target application 

*Port* -> serves as network communication endpoint, it enables data exchange.
- If you set up port 80 and a request comes from another port, the load balancer will not allow access

Target -> EC2 instances. When the incoming request comes in through port 80 (for example), evaluate rule, and then distribute to the corresponding target. 

Target group requires a health check configuration

Each of this target groups (group of EC2 instances) is in a different availability zone. So load balancers force you to deploy best practices

ENI 
              A                                  B 
![[Pasted image 20250610180416.png]]

In the environment A, there is not a proper distribution of servers. If the node 2 goes down, there will be a great outage and Node 1 will be under a lot of stress

For this, there's *Cross Zone Load Balancing* -> Each node can distribute on its own AZ, but also on other AZs
- But it does not solve the problem of a AZ going down, but it gives a little bit more resilience. 

Doing a homogeneous deployment is not always the best solution, but it could work for some organizations. 

*Cross Zone Load Balancing is always enabled* 

#### Practice Quiz Question: The OSI (Open System Interconnection) model is a conceptual framework that standardizes the functions of a communication system. It consists of seven layers, each responsible for a specific aspect of network communication. Which layer of the OSI model does an Application Load Balancer operate at

Layer 7 - Application Layer


Status 200 -> returns data 

Status 204 -> acknowledgement of successful request

Status 500 -> Internal server error

Health check can be configured on the target group and the ALB can use this to determine where to direct traffic
- The target group contains the configuration for the balancer to know the health of each instance
- But the health check service runs inside the EC2 
- Health checks are status codes 

*Back Pressure* -> Mechanism that prevents overloading backend servers by regulating the flow of incoming requests. Dynamically route traffic to other instances. An instance can ask the load balancer to not send traffic to protect itself
- even if the instance is healthy, it can send back a 'not available code' so that the load balancer can let it finish its tasks. Once its done, it will stop sending the code and it will start receiving traffic/requests 


#### Practice Quiz Question: The primary feature of an application load balancer includes load balancing based on:

HTTP or HTTPs requests 

## ALB - Authentication Flow

You can configure a load balancer to securely authenticate users

This enables you to offload the work of authenticating users to your load balancer so that applications can focus on business logic

OAuth -> Sing in with google when opening a web app. 
- The load balancer sends the user to another target - the Sign in application of your choice. 
- Tokens 

![[Pasted image 20250610182235.png]]


### Summary
ALB Operate at the OSI models application layer 7

ALB direct traffic to specific groups of backend targets, allowing for different routing rules and health check for each group

Application load balancers are critical to modern application architectures, allowing for efficient, scalable and reliable traffic distribution in cloud environments


![[Pasted image 20250610182456.png]]

Rules contain paths 

#### Practice Quiz Question: What are the main components of the ALB? 
A _load balancer_ serves as the single point of contact for clients. You add one or more listeners to your load balancer. A _listener_ checks for connection requests from clients. The rules that you define for a listener determine how the load balancer routes requests to its registered targets. Each _target group_ routes requests to one or more registered targets, such as EC2 instances.


### When to use application load balancer, real life apps:

- Ecommerce
- Multi tenant SaaS

