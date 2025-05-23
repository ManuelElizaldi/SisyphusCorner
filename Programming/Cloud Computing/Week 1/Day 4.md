2025-5-21 - 2025-5-22

[[Cloud Computing]] [[Economy]]
# Price Economies Data Velocity & Distributed Computing

Profit -> revenue - cost, its important for cloud because cloud is pay as you go

- Cloud helps you monitor the ops costs 

Pricing -> 
- Cost based pricing:
	- cost of building a product 
	- cost of maintaining
	- providing support 
- Valued based
	- Customer perception about the product
	- What values customer derives from the product 
	- Longevity of the product
	- Recognizable name associated with luxury

Price is a function of geography. AWS in Oregon is x, but in another region is Y. The cost of operating a certain region has a certain cost. 

- You can't go for the cheapest option due to *compliance*. HIPAA compliance does not let you store data in places where you are not operating

*Price can't be constant*, how do you maximize margins? You need analytics. You generate this data in the cloud, you need BigData analytics -> managed service in the cloud


## The Golden Data
There is a gap between traditional analytics tools and the business requirements. 

Example:

- By the time the data comes in, goes through batch processing, into a warehouse, then uploaded to a BI tool, propagates into graphs and then analyzed, its probably not significant

*Operation Data* -> needs to be crunched

*Tactical Information* -> Data processed

Then you need to make a decision:

*Strategic Insights*


#### Practice Quiz Question:A school looks to streamline server usage for storing teacher and student records. It has chosen a cloud provider for IaaS. Which of the following is completely eliminated by doing this:
Capital Expenditure

## Real Life Challenges of Distributed Computing & Cloud 

*Heterogeneity* ->  using and managing different types of hardware, software and services within the cloud. It refers to the variety in systems and platforms that work together in a cloud environment

*Microservices* -> Having a monolithic application that is broken into smaller chunks 

Back in the day, you could only learn C++ and be good, but according to the instructor one microservice can be using Java, another one could be using Python and so on...

in microservices, you can grab the best technology from each programming language and they can talk to each other through APIs

*Fault Handling* -> How effectively can you handle fault? Can you handle a container failing? It becomes a norm rather than an exception, you can design architecture 

*Consistency* -> Getting the right data when performing a read operation. 
- Eventual Consistency -> Many enterprises are moving to this way of operating
- Strict Consistency 

*Global Concurrency* -> Common object across distributed systems 

*Upgrades and maintenance*  

*Local resources - file system* 

*Application sessions & transient data*

*Session Affinity/Sticky Session* -> Ensures that a user's requests are directed to the same server or application instance 

*Clock Synchronization* -> NTP time, all times evolve from the first epoch (January 1st 1970)

# Apps for Cloud & Security Model

Evaluate enterprise architecture impact, choice of right service, defining business process and integration points, security fabric, think stateless, adapters, foundation, micro service approach

- The right combination of these factors assure a good cloud

Sense of control? Who is the supreme owner of control of your application? There is not one answer. As well as before, it all depends on your architecture

For most businesses Decentralized Administration is the new reality. 

*Decentralized Administration* -> principle of local autonomy. Each service model retains administrative control over its resources. 

*Secure Distributed Collaboration* -> You don't want to stop service to your customer because your cloud provider is down, you will have to design an application based around this. 
- Overtime you can get to a point where there is no SPOF (single point of failure)

*Credential Federation* -> decentralized single sig-on on mechanism. 

*Placement of Functionality* -> Right provider for the functionality needed in the business process

*Loose Coupling* -> You don't control the life cycle of the services. You have to protect yourself with adapters. Don't get locked-in. 

Build your application with all the above baked in

## Security Fabric for the Architecture with Multiple Providers

The usual model in the cloud is oAuth 2 -> defacto standard when talking about authentication and integration with a third party provider

oAuth -> 1) redirected to provider authorization (google) -> 2) user grants authorization in google 3) redirects user back to application -> 4) exchange for access grant 5) grant access token -> 6) create connection 

- This is a robust security system where your sensitive data does not travel to the application. Its harder to get your data

#### Practice Quiz Question: OAuth stands for:
Open Authorization


## Shared Responsibility Model 

The security of the cloud depends on both the user and the cloud provider. Each has to play its part. 

Security off the cloud -> Anything custom that you have built, your own OS, own ports, that is your responsibility to keep safe. 

Security in the cloud -> The provider takes care of this. 

Some cloud providers offer free services to check your infrastructure to analyze if there's any vulnerabilities. This is a continuous process.

#### Practice Quiz Question: Which is the responsibility of the cloud provider?
Securing the datacenter from unauthorized access

## Diversity of Programming Languages

Machine, procedural, data, object, functional, etc. 

No one can tell you which programming language to use. This depends on you. In terms of the cloud, it does not matter. Its a linux instance you are getting from the cloud. As long as your environments are compatible with the cloud you are good. 

Cloud provider and programming language decision do not intersect, but the most popular programming language is python. The entire open stack is on python. 
- Javascript and Java are also popular. 
- Go is also becoming more popular




