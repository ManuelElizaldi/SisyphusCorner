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

#### Practice Quiz Question: 