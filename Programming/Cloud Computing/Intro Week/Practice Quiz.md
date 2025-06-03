This is a practice quiz after finishing day 1 - 5

Characteristics of containers do not include: Dedicated host.
- From day 3

Cloud which can be accessed by a set of organizations is called:
- Community cloud 
- from day 2

Which of the following is not true of horizontal vs vertical elasticity:
- Vertical elasticity is resilient to cascading failure

Session Affinity is:
- directs all requests in a session to a specific server

Which of the following components are common in containers?
- I selected system memory but its wrong

Which of the following is the foremost reason why an investment bank would prefer a private cloud over public?
- Security 

Google App Engine can be considered a?
- PaaS
- Google App Engine is a platform that allows you to develop web apps

Legacy applications can be easily migrated to the cloud?
- False
- It takes a lot of effort to translate them to code that can be used in the cloud

The core elements of cloud computing are:
- IaaS, PaaS, SaaS, Managed Services

Which of the following is not a drawback of virtualization?
- Hard partitioning among virtual machines
- *partitioning* -> process of dividing the physical resources of a single machine (server) into multiple VMs

The programming language of choice to build cloud - ready applications is tightly coupled with the cloud provider used?
- false

Which of the following is a benefit of a layered cloud application?
- Customizable elasticity 

Benefits of elasticity?
- It prevents exceeding the required capacity
- Ensures optimum utilization of resources
- Makes applications highly available
- Help overcome under-utilization 

The cloud provider is responsible for maintaining the networking infrastructure in IaaS?
- True

Which is not a characteristic of Cloud VM?
- I selected Encapsulation, but now that I think about it, each VM is its own environment, so it would make sense to call this encapsulation.
- The correct answer is : Disaster Recovery -> VMs can be part of the disaster recovery strategy, but this is not a fundamental characteristic of VMs. They are portable and have snapshot capabilities. 

You are working with a Java environment form a cloud provider to deploy and publish your application. Which of these is the highest layer that will be managed by the provider?
- Runtime -> Execution of the program, essentially the last step in an application

Assume that AWS has a Git-based code repository service called Code Commit which can be integrated with the CI/CD tools on their platform. Which of the following changes will occur from a “developer’s perspective” when an organization transfers their Dev Ops process to AWS from a manual workflow?
- No changes will occur, just the code will have to be pushed to Code Commit instead of the old git repository
- This service was seen on day 5, and you just push your code and the pipeline will initiate 

Key attribute of PaaS is:
- Managed runtime, no need to start, stop
- Managed infrastructure, agnostic on the nature of hardware applications needed to run -> although the user has some control over choosing which one to use

Which security approach seems most popular to integrate user security in application? 
- oauth2

In "cost plus" based pricing, the price is based on:
- Cost + margin

Time interval between request and response is called:
- Latency 

Which of the following job roles will be affected when using a managed service for Map Reduce operations versus installing and manually setting up a Hadoop cluster in a set of provisioned VMs?
- System admin -> when using map reduce, many of the low level tasks - provisioning servers, configuring Hadoop clusters, managing updates, monitoring system health will now be handled by the cloud provider.
- Managed services reduces much of the manual intervention 

An organization offers SaaS based on their product which uses a database as the backend. They decide to perform a lift-and-shift migration to the cloud using the same application, schema and database engine. How will the application architecture be affected by this?
- The database connections will have to be redirected to the new endpoint on the cloud deployment, but everything else will remain the same.

Addition of multiple application servers that work as a single logical unit is called
- Horizontal scalability

Not an advantage of containers over virtual machines?
- Higher isolation

An application deployed on an on-premises setup suddenly receives a huge influx of traffic. To keep up with the load, part of the traffic is diverted to an endpoint of the same application hosted on the cloud. This deployment model is known as
- I selected migrate to cloud -> but was wrong

Which of the following elements is the responsibility of the cloud provider with respect to security?
- Physical security of the servers

Which one is not a cloud deployment model?
- Organization

Cloud provider will guarantee security under all circumstances
- False

Stateful applications are ideal for horizontal elasticity.
- False
- *Stateful applications* -> are applications that remember information (state) about users or processes between sessions or interactions
	- Example:
		- Chat app that remembers chat history
		- Online game 
		- banking app managing transactions
- They are not ideal because its hard to distribute information evenly across multiple instances. Scale out seamlessly and its harder to recover quickly from instance failure. 
- *Stateless applications* -> are ideal for horizontal elasticity because any instance can handle any request. You can easily remove instances based on demand, they scale out efficiently

A school has a set of applications that require a large number of servers to store its teacher and student records. It has chosen a cloud provider for IaaS. Which of the following is it completely eliminating by doing this?
- Capex

Cloud providers are required to follow open standards?
- False, providers and decide how to operate, which makes migrating from one provider to another hard. But there are initiatives to standardize processes

An organization offers SaaS based on their product which uses a database as the backend. They decide to perform a lift-and-shift migration to the cloud using the same application, schema and database engine. How will the application architecture be affected by this?
- The database connections will have to be redirected to the new endpoints on the cloud deployment, but everything else can remain the same

A continuous stream of metrics from a set of sensors is stored in a cloud storage service. Once a suitable size threshold is crossed the data needs to be transferred to an on-premises data center where it is further analyzed. This architecture is an example of

- *Integration as a service* because it enables the integration of data between different systems or environments such as between cloud storage and an on premise data center
- Key aspect -> automated movement of data based on conditions -> threshold of data
- It is not Storage as a service because that is just storing data, not moving it from one place to another or the integration of systems

This is a myth - You must create a basic architecture prior to any cloud implementation.

- False, you do have to have a plan in place in order to determine what to offload to the cloud 