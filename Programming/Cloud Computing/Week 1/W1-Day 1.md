2025-05-18
[[Concepts]] [[Cloud Computing]] [[Integrations]]

# Definitions, Stories & Business Concerns - Video

There is no such thing as Cloud Computing -> its only someone else computer/data center *kind of saying this jokingly*

## Services

*Infrastructure IaaS* -> give you compute, networking and storage. Focuses on infrastructure management
- AWS, Google, Microsoft Azure
- The provider is responsible for the networking infrastructure

*Platform Vendors PaaS* -> Abstracts things you need to be responsible of, software updates, packages, etc. 
- The primary purpose of PaaS is to deliver a development and deployment platform 
- Simplifies application development

*Software as a service SaaS* -> broad definition. Apps, APIs, etc. You are producing something and someone else is consuming it. The consumer does not care about infrastructure or platform, he just wants the app/product. 
- Software distribution model where applications are hosted and maintained by a third party provider, accessible to users over the internet. It could be offered through a subscription model. 
- The user does not need to worry about local installations and upkeep
- Ready to use software

*System Integrators* -> Person or organization that focuses on making different software and hardware work together in a cohesive and functional system. This can become a complex technological system
- Building the cloud system 

## Why Cloud Computing - Is it for me?

Why cloud computing -> capital expenditure to operational expenditure
- Capital Expenditure -> Money spent by a company in long term use objects. Usually one time cost. Buildings, equipment, vehicles, etc. 

- Operational expenditure -> Day to day costs. Money spent on regular things that is needed for everyday operations

Cloud Computing is not for everyone, you have to evaluate the technological landscape of your organization. Sometimes its not worth the investment

*Big Bang Transition* -> moving the entire IT infrastructure of a company in one big significant move. Typically replacing the on-premise system entirely
- Usually this strategy does not work 

### Capacity Planning 

Determining the optimal resources, including hardware, software and network infrastructure, required to meet the current and future demands while maintaining cost-efficiency and performance

### Stories

World of Warcraft not having enough servers 

Instagram outages 

Flipkart - Indian retailer, billion day sale. Sometimes in high demand days, the servers are not ready for that spike in demand 

note:
ASP -> Application Service Provider in early 2000s, this term evolved into SaaS. 

_ASP_ was also a company popular in the early 2000s, that offered a place to keep all your hardware. They would take care of it and you could log in from your enterprise via the network. They offered primary power supply, secondary power and networking. They made sure everything was running. This was a primitive version of IaaS

_SETI@HOME_ -> Search for extra-terrestrial intelligence at home, software that allowed you to download audio recording from space to search for meaningful information. Mid 90s
- So, is distributed computing a cloud invention? It is not. It's been around for some time now 

_Distributed computing_: Involves a network of interconnected computers collaborating to tackle problems 

### What does Enterprise worry about

_Service availability_ -> I want my end user to be able to consume my product.
- User growth is hard to determine. 

_Elasticity_ -> Elasticity is the automatic adaption and allocation of computing resources like servers and storage to match fluctuating workloads and needs. 
- This ensures cost-efficiency and performance scaling

_Virtualization_ -> Technology that enables multiple virtual instances of operating systems, servers or networks to run on a single physical hardware system. 

_Redundancy_ -> Duplicates servers, storage and network infrastructure to ensure seamless operation and resilience against failures. Minimizing data loss 
- Very important and basic. All data centers need something like this
- Preferably, you create this in different geographies 

_IT refresh_ -> 3 year life span for hardware. Every 3 years you get new hardware. 
- Do you want to do this every 3 years? As an enterprise you need to take this into consideration. Businesses rather focus on their main objective/product

_Lock-in_ -> When a customer becomes too dependent on one cloud service ecosystem, making it difficult and costly to switch 

Is the data safe in the cloud?

_Public Cloud Computing Services_ -> Offered by third party providers, grant the general public internet-based access to a range of computing resources, including virtual machines, storage and applications. 
- This is a huge concern for financial institutions

 _Audit Trial_ -> Who, how why? -> is a digital record that tracks and logs all activities, access and changes within a cloud environment. 
- Essentially, everything gets logged for security purposes. 
- Compliance
- Very important to understand why and how something happened -> if something breaks, you check this

_Licensing Fee_ -> Everything you pay for, human capital, software, machines, support, maintenance, adds up. This cost is fixed/remains constant but goes up every year, regardless of your sales. 


#### Practice Quiz Question: Building Blocks of Cloud Infrastructure Service (IaaS)

Compute, Storage, Networking 


# Classical Enterprise, Why Cloud & Evolution of Cloud - Video

### IT Landscape in a Typical Enterprise Environment 

This are all business components that an enterprise needs to maintain and care for. It is a lot of work and money. In some cases (if the fitment analysis approves) its better to off load some of this to the cloud provider. 

As the instructor mentioned, its better to focus on building the jet plane engine instead of worrying about hardware and software limitations.

*Portals* -> Networking
- Intranet -> private network restricted to a specific organization, used for internal communication and sharing of information

*Search* -> When you have a huge dataset, they need to be able to find information fast

*Content Management* -> Creating, organizing and maintaining digital content such as text, images, and multimedia to ensure its accessibility, relevance and efficient publication on websites or other digital platforms. Structured and unstructured. 
- Many sources of data that needs to be managed. 

*Middleware/ESB (Enterprise Service Bus)* -> Helps connect diverse systems within the enterprise to enable communication and data management between them.
- interaction between business units. 
	- Example, an order comes in, another business needs to receive it and then prepare the order to be shipped. 

*BPM (Business Process Management or Business Process Engine)* -> Software tool used to design, model, automate and manage complex business processes. 
- Visually mapping the business process, visualize the steps of the business. Here you can find opportunities for optimization.

*Database farm* -> Multiple database types/flavors in an enterprise. Operating as a cluster to distribute workloads, ensure high availability and boost performance. 
- Structured, non structured, open source and not open source, some homegrown. 
- Databases need to be managed, they require a lot of baby sitting 
- OLTP -> Online Transaction Processing -> type of database that manages and records transactions in real time. Frequently used in order processing. 

*Warehousing* -> When you have a farm of databases, information scattered across many sources, you want a centralized place to find information. You create ETL pipelines to then store processed data inside the warehouse. 
- Warehouses serve as the foundation for business intelligence 

*BI/Reporting* -> Find insights within the data, you can go open source or other type

*CSR Product* -> To take care of the customer you need Customer Service Representative and any software that can help with this task

*ERP Products* -> Enterprise Resource Planning, integrated software system streamlining business automation and operations like finance, HR, inventory, manufacturing.
- Examples: Oracle 

*Contact Center Product* -> Call Center

*Infra Monitoring Tools* -> Infrastructure monitoring tools, you have to capture any failures within the system. Be proactive.

*Code repo/CI/CD Tools* -> Code repository, productivity tools, etc. 
- You still have to set up everything

*Virtualization Software* -> Every enterprise uses virtualization. How do I squeeze more out of my investment -> virtualize more computers. 

*Infrastructure* -> hardware, routers, cable, etc. 

*Networking* 

*Building & Perimeter Security*

*Electricity (primary, secondary)/Cooling/Land*

*Human expertise and capital*

*Ongoing Process of patches and upgrades*

*Procurement* -> You need short procurement times. No time wasted


All of these parts in an enterprise come with a cost and maintaining **cost**
### Why Cloud?

![[Pasted image 20250518155102.png]]

*User Hours* -> Total time a user is utilizing a service 

With the cloud, you remove the utilization from the equation. It makes you more flexible - more business agility

#### Quiz question
![[Pasted image 20250518160418.png]]

# Service Models, Abastraction Levels (v1), SPIDERS

Gartner and Forrester - industry experts

Cloud computing -> IT services offered through the internet. Pay as you go.

## What Cloud Computing is Not - Myths

Cloud Definition -> Remote server network that stores and manages data and applications

There's no one single cloud -> there are multiple providers

Multi-cloud strategy -> using services from multiple cloud providers

All you need is a credit card -> its not that easy, yes, you need money, but you also need to know how to set up the cloud infrastructure

The cloud will save you money -> Another myth, sometimes the cloud is not the right solution for your company. You have to be smart about how you use the services. If not, it will cause more overhead cost

It will reduce work load -> How smart you are? How much automation you are brining? How much work are you offloading to the cloud 

Integration -> Different apps in different places, you need to be able to integrate these applications. It depends on the design and type of apps. 

Security -> When you lock your house, are you guaranteeing security? 100% security is a myth. 
- Security's focus should be -> if there's a breach, how quick can I solve it, recover and learn from it 
- Security is never guaranteed

Virtualization =/= is not cloud computing
- Dedicated instance vs virtualized instance 
	- *Dedicated instance* -> Costs more, but gives you full ownership of the infrastructure, more private
	- *Shared instance* ->  Multiple tenants in one system

Cloud computing is only about technology -> Its about how am I becoming more efficient, how much money am I saving, how secure I am, what operations can i offload to the cloud 

## Service Delivery Models
How the different models stack -> IaaS, PaaS and SaaS

A style of computing where massively scalable IT-enabled capabilities are delivered 'as a service' to external customers using internet technologies

![[Pasted image 20250519174801.png]]

## Spider
SPIDERS stands for A security initiative for protecting critical infrastructure

SaaS, PaaS, IaaS, Big Data, Elastic, Resilient, Subscription -> Spider



### Big Data
In today's world there is a lot of data collection, especially through IoT sensors. You have to be able to store, process and manage this data. 

Going the traditional route: using RBDMs you are going to have scalability issues. These traditional databases can't keep up with the load

Thats where Elasticity comes in:

### Elasticity
You can set an elastic data tier, if data amount goes up, more infrastructure is added and data will be distributed across multiple systems. 

### Resilience
If a part of your infrastructure goes down, you need to be able to continue operations. You wont stop selling because one computer is down. You need to be *resilient*. 

### Subscription
Pay as you go

Finance industry -> main concern is security, they rather use private 

Social application -> they do care about security, but its not their main objective, they rather be resilient, they want to have as many clients as possible 

Big enterprise -> they use multiple applications, some are hosted on the cloud, other are not, so you need a way to integrate them (middleware/ESB)

Big Data concerns -> Three V's, velocity, variety and volume. These 3 categories challenge traditional database tools

### Pizza as a Service
![[Pasted image 20250519180444.png]]

## Degree of Abstraction - Application View

![[Pasted image 20250519181154.png]]


#### Practice Quiz: The Cloud provider is responsible for maintaining the networking infrastructure in a IaaS offering

## Abstraction Levels (v2)

PaaS is a good balance between IaaS and SaaS, due to this, it started evolving to satisfy the business needs. In this note, there's also FaaS and CaaS, there's not a lot of differences between the services:
- *Container as a service* -> run apps on a container and you only manage the application and the data. The only thing needed to run this service is to bundle the app and its dependencies. This bundle is called a *Docker Image*. It operates similarly to a PaaS but instead it will manage a cluster of containers. 

- Function as a service -> You manage functions and data. You write small pieces of code the service can manage everything else. 
	- This service is focused on agility, fail fast and pivot rapidly. AWS lambda functions is a popular example of this. 

Errors will happen, bugs can occur, so being able to fix these quick is important. In a traditional build, when you hit a bug, it is hard and takes time to push a rollback. PaaS, FaaS, CaaS offer the ability to version swap in a heartbeat. 

This innovation has allowed developers to build and test new products fast. This is becoming the preferred application development process - *[[Agile]]*


scale = elasticity

