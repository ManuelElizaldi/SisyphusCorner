2025-5-19

# Cloud Attributes, Managed Services & Deployment Models

## Cloud Computing Attributes

Choice of provider -> do a *fitment analysis* -> refers to the process of assessing and determining the suitability or compatibility of something for a specific role.

The architectural decision has to be made right in order to save money with cloud. 

You have to analyze your organization and determine which is the best for you
### Attributes

Agility, OnDemand, Self Service -> is the cloud service available on your region? What about agility -> speed is hugely important on today's operations. 

- Look for the *Turn around time* -> total time taken to complete a task, the goal is to reduce this 

- *Self service* -> not depending on other departments

*Resource pooling* -> Leverage economies of scale for cost reduction. Attribute that involves the aggregation and sharing of computing resources to serve multiple customers. 
- Economies of scale -> refers to the cost advantages that a business can achieve as it increases its production or scale of operation. 
	- If you have multiple clients you can spread the risk across them all
	- This motivates customers to grow

Admin and monitoring -> Being proactive is better than reactive. Constant monitoring of the infrastructure. 
- The cloud offers tools to monitor, but you still have to go out and do the work

Core data center services -> the building, security, electricity, all the infrastructure needed to hold the cloud hardware

Managed services -> Hosted managed services allow developers to focus on core applications with business logic, support services become an API call. 
- The enterprise has to worry about many things, networking portals, data base centers, hardware, middleware, etc. so the cloud comes in and offers all these as a managed service
- The business can focus on the product 

Resilience, Elastic and Subscription ->  Building infrastructure that can sustain failures. 

## Cloud Offerings/Cloud Managed Services

*Cloud offerings* -> all the services that a cloud provider offers

*Team of services* -> the different offerings of a cloud provider

All of them will provide elastic infrastructure 

*Node availability* -> if one computer fails, is there another instance that can take over the operation

*Hadoop* -> cluster computing for big data

*MapReduce* -> operation used by cloud services to process data within the cloud operation 

*Ephemeral Storage* -> it lasts the duration of the session/operation

When you build a big data database, it is very complex, so the cloud comes in and offers a system to help you set everything up

*Cassandra* -> NoSQL database management system designed for high scalability and fault tolerance

*Consistency* -> Data consistency. Ensures that all users see the same data across all nodes/instances/replicas.

You might make a query in one node and by the time its processed in another, the data might be different or not there at all. This creates grate complexity. 

There are two key models of consistency:
1) Strict -> Any read operations returns the most recent write
	- If you write x = 5 in node A, when you read x in node B it will return 5. 
	- This ensures the correctness of data. Important for banking, inventory and management
	- Requires high coordination between nodes, more correctness, lower performance. Less scalable
2) Eventual -> Given enough time all nodes will converge to the same value. 
	- Reads may return reads that are outdated. 
	- Example: Big Query returning the right data after 12:00 am 
	- High availability and performance, but needs to be designed according to handle the temporary inconsistencies 

*Connectivity* -> When you have multiple apps in an operation you need to find a way to connect them all. *ESB* Enterprise service bus 
- Apache ActiveMQ -> open source solution that facilitates the exchange of data between distributed applications. 
	- Clouds can offer something similar or that software

Capex -> The car
Opex -> the fuel to power the engine

	"I consume, I pay"

*Time to market* -> Refers to the time it takes for a product or service to be developed, manufactured and brought to market

*Transaction - based delivery* -> Ensures that a group of operations are treated as a single unit. Either all operations in the transaction succeed or none are applied.
- Example: Ecommerce delivery when a delivery comes in:
	1) Deduct item from inventory
	2) Charge the credit card
	3) Send a confirmation email
	4) Write the order to a message queue for delivery services 
## Cloud Deployment Models

*Hosted Managed Services* -> Outsourced IT solutions where a service provider hosts and maintains applications or infrastructure on behalf of clients, ensuring continuous performance, security and maintenance. 

*Public Cloud* -> Public does not mean that software and hardware can be viewed by everyone, it means that you can rent services if you are a small person or a big organization. It means anybody can rent these services.

In a Public Cloud Model, once you make an account, your data is private to only you. 

*Private Cloud* -> Not very popular. There's two definitions:

1) Something that I own. I own all the data centers and necessary hardware to host a cloud.

2) VPC -> Virtual Private Cloud, private networking. You rent private networks, the traffic is restricted to your instances

*Community Cloud* -> Hypothetical, many organizations come in together and have a common data center.

Hybrid Cloud -> Enterprise having one data center with its own home grown applications but they also use services from a public or private cloud. 

Linking of these two clouds can happen in many ways, direct connect (AWS), direct cables connect to AWS server.
	With this, you can bypass the internet 

# Pricing & Scaling Models

## Subscription Model 

*Pay as you go* -> you pay as much as you consume. In the cloud you get a subscription model, you rent what you need. You rent x capacity, you pay x capacity. 

There is no global standard on how much the provider charges

It is a good idea to review pricing models from time to time because it changes. 

*Scaling Model* -> There are a lot of internal and external inputs that could make you change your infrastructure. Go from state A, to state B. 

- *Classic Scaling Model* -> You for see a change in the future so you buy more infrastructure to be ready. "Anticipated new capacity". Fixed infrastructure
	- This is fixed capacity

![[Pasted image 20250520162600.png]]

In this model, due to the fixed pre planned capacity you have the same cost if you have 1 user or 1000. 

*Over-utilization* -> in cloud, this refers to when you consume more resources beyond the predefined or allocated limits 

- Service outage -> related (point B), refers to a point where you can no longer serve your customer
- This is why capacity planning is important -> calculate where the red line is to plan accordingly. 

*Under-utilization/wastage point* -> in cloud, refers to when you are not using all the resources available


- *Modern/Cloud Scaling Capacity* -> Cherry pick the components you want to scale. Layered architecture. The more layers, the lower the performance, but according to the instructor, the benefits out weigh the cons. 
	- This is Elasticity, its not fixed compared to the classical model. You can grow and reduce. 
	- Might be harder to maintain.

![[Pasted image 20250520162858.png]]


Trying to calculate the right capacity, can become a losing battle. It is hard to determine and if you but it lower that what is required you will have service outage/over-utilization. If you but it way above the required you will have wastage. 

This is where elasticity comes in. 

You want your capacity to follow your utilization. Your cost will change accordingly. 

![[Pasted image 20250520163953.png]]

But having elasticity is not as simple as it seems. You need to gather metrics at the beginning of any operation in order to best calculate when to add the extra capacity. 

Height (h) -> *Determines Horizontal Scalability* -> Adding more machines or nodes. Ability to increase the capacity or performance of a cloud based application or system by adding more resources, such as VMs or servers. 
- Promotes flexibility and cost efficiency 
- Example -> Going from a 4 gb ram and 16 core to 16 gb ram and 36 core, etc. 

*Vertical Scalability* -> Increasing the capacity of a single machine.


#### Practice quiz question: Which advantage does a subscription based cloud model offer to a customer?
Scalability on demand






