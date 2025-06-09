![[Pasted image 20250605221102.png]]

![[Pasted image 20250604214603.png]]![[Pasted image 20250604214645.png]]

54.81.23.72

got this error after securing my file:

manu@ManuelDesktop:~/Downloads$ ssh -i pgpcc-key1.pem ubuntu@54.81.23.72
ubuntu@54.81.23.72: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).


![[Pasted image 20250604215841.png]]
![[Pasted image 20250604215905.png]]

![[Pasted image 20250604215943.png]]
![[Pasted image 20250604220017.png]]


# Robotic Process Automation
RPA, uses bots to automate repetitive tasks. 

RPA mimics human interactions with software interfaces allowing orgs to streamline workflows without extensive programming 

RPA solutions can incorporate AI and ML to handle unstructured data and make smart decisions. 

## Benefits 
*Increases efficiency and productivity* -> because it frees employee's time to work on more valuable tasks. 

*Cost saving* -> lowers opex because it lowers excessive manual labor. It can also be implemented without major changes to the existing IT infrastructure.

*Improved accuracy and compliance* -> Ensures consistency and accuracy, repetitive tasks done by humans can have errors. Also, RPAs can help you adhere to regulations. 

*Scalability and Flexibility* -> No need to hire more people, just deploy RPAs, if demand goes down, turn them off. 

*Enhanced employee satisfaction* -> Employees no longer need to work on tedious tasks and can focus on more valuable objectives. 

Faster processing and improved customer experience -> improves response time. 

Competitive advantage -> businesses can optimize their operations. They can offer faster, more reliable and cost effective solutions. Businesses can focus on innovation, rather than tedious tasks. 

Better data management and insights

## Drawbacks

Implementation challenges

*High initial* cost, licenses, infrastructure and consultations. If there's legacy software, there could be integration issues when there's not a proper API.

*Technical debt* -> RPAs are usually used as a work around and not something to address the root issue, this could create problems down the line. 

*Operational limitations*-> if the interface changes, the bot breaks. This requires constant maintenance. RPAs are limited to rule based tasks and can't perform judgmental decisions or complex exceptions that require human intuition. 

- It can also get expensive to maintain a fleet of bots

*Organization impact* -> job displacement, entry level positions will be affected. 

Strategic considerations -> RPA can delay modernization, again, it can be used as a work around instead of addressing a core issue. Also, bots require elevated permissions access data, which increases the surface area for an attack. Lock-in is another potential consideration, they can end up depending on this service. 


## RPAs and Cloud Environments

They complement each other perfectly. You deploy infrastructure and the RPA works on it. It can help you take full advantage of your cloud investment. 

Just as infrastructure, they are elastic. Bots streamline the deployment lifecycle. This automation reduces deployment time from days to hours or even minutes. Eliminates human error in configuration and ensures consistency. 

Organizations can reduce opex by automating routine cloud management tasks, optimizing resource allocation, and implementing automated cost monitoring. RPA bots can identify unused resources, recommend optimizations, and even automatically adjust configurations to maximize cost efficiency.

## How does GenAI play into this?
Cloud environments, RPAs and GenAI is a three way integration that offers more intelligent, adaptive automation ecosystems. 

*GenAI allows RPAs to go from a rule based operation to a more intelligent decision making bot*. GenAI allows RPA to process unstructured data like email, documents and images. It can understand context and extract meaning from the input.

Cloud providers have the necessary hardware to run GenAI models. The elasticity of the cloud is perfect for GenAI since it has variable resource requirements. 

Organizations now can access sophisticated AI capabilities through cloud services, democratizing access to advanced technologies that would be expensive to develop on prem 

Traditional RPA bots often break with interface changes, but GenAI gives it the capability to understand the intent and context of interfaces, making them adaptable to changes. 

# AWS Console to code: Bridging visual and programmatic cloud management


AWS has a couple ways to interact with the cloud's resources. One of them is IaC - Infrastructure as Code.

Console to Code allow organizations to go from point and click operations to automated, version controlled infrastructure management

## Gen AI - A cloud practitioner's perspective

There's two benefits: Self Productivity and Customer Solutions

*Self Productivity* -> Gen AI speeds up the coding process. It can instantly generate infrastructure as code scripts and help with troubleshooting. According to the article, it can even predict possible bottlenecks, future problems or security vulnerabilities.

It can be in charge or repetitive tasks and allows architects and engs to focus on more creative tasks. 

It can help with learning, documentation, diagrams and training docs

Because it lowers cognitive load, it can help coming up with new ideas.

Improved reliability and innovative solution design

*Customer Solutions* -> With Gen AI you can have a cloud infrastructure that is proactive and intelligent that can autonomously generate insights, optimize performance and identify potential operational improvements.

Context aware solutions across various business domains. 
- In Finance it can provide real time fraud detection and adaptive security protocols.
- Manufacturing can benefit from AI by getting detailed reports about the health of their systems and it can even suggest maintenance schedules
- Customer service it can understand complex client queries

Trea AI as a key component of the cloud architecture

## Infrastructure as Code - Code your Cloud
Why use cloud -> Build robust and scalable customer applications and solutions

To make this easier, practitioners have been adopting the approach Infrastructure as Code principles for cloud management. You code/write a machine readable configuration file.  

You bring in the same rigor of code into infrastructure configuration. Consistent and repeatable deployments. 

Automate complex environments -> I imagine that the file can be used for different instances and you just copy and paste it. 

## Two Prominent Faces of AWS Management - AWS Management Console and IaC

### AWS Management Console
Visual interface for cloud resource management. No technical skills, low barrier to entry/use. It offers a intuitive web UI. 

The drawback of this approach is that it requires a lot of manual intervention. 

*I am guessing, that all the services and resources you can manage inside the AWS management console can be set up through a configuration file. That way you just upload this to the server and it creates/manages the resources for you.*

### IaC - Infrastructure as Code
Treats configuration as software. Resources are defined programmatically by code -> Json, YAML, HCL, etc. and stored in repositories, enabling version control 

Repeatable and fault proof resource provisioning. 

*HCL -> Hashi Corp Configuration Language*

## Console-to-Code - Where IaC and GenAI Meet
Generate IaC (config files) with Gen AI

The console workflow makes sure any parameter values specified are valid together

This code can be used as a starting point and then customized to the desired needs/objective

## The Console-to-Code Challenge
