2025-05-18
[[Concepts]] [[Cloud Computing]]

# Definitions, Stories & Business Concerns - Video

There is no such thing as Cloud Computing -> its only someone else computer/data center *kind of saying this jokingly*

## Services

*Infrastructure* -> give you compute, networking and storage.
- AWS, Google, Microsoft Azure 

*Platform Vendors* -> Abstracts things you need to be responsible of, software updates, packages, etc. 

*Software as a service* -> broad definition. Apps, APIs, etc. You are producing something and someone else is consuming it. The consumer does not care about infrastructure or platform, he just wants the app/product. 

*System Integrators* -> Person or organization that focuses on making different software and hardware work together in a cohesive and functional system. This can become a complex technological system
- Building the cloud system 

## Why Cloud Computing - Is it for me?

Why cloud computing -> capital expenditure to operational expenditure

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

*Code repo/CI/CD Tools*

*Virtualization Software*

*Infrastructure*

*Networking*

*Building & Perimeter Security*

*Electricity (primary, secondary)/Cooling/Land*

*Human expertise and capital*

*Ongoing Process of patches and upgrades*

*Procurement* -> You need short procurement times. No time wasted

### Why Cloud?

![[Pasted image 20250518155102.png]]


User Hours -> Total time a user is utilizing a service 

With the cloud, you remove the utilization from the equation. 
