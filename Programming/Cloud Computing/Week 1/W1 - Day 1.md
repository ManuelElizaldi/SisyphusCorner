# Introduction to Cloud Computing Services

[[AWS]]

The concepts are more important than the UI you see on the cloud platform. This is the same as learning a spreadsheet system. Think about the big picture<- Advice from the professor.
## Brief History of AWS
Amazon existed before AWS. Amazon is founded in 1994, it started as ecommerce selling books. It kept growing and the technology staff struggled with this resizing. There was a need to be able to scale quickly depending, this forced amazon to build resilient systems. 

Around 2000 when they were building merchant.com, when they were cleaning up their APIs, infrastructure, etc, they realized that maybe they could offer this as a service. 

So as they were building, they came to the conclusion: if we are having this problem of scaling and building resilient infrastructure, other companies will face the same. This is a brilliant insight (IMO).

2004 they came up with AWS, but this wasn't similar to what we now know as AWS. That came in 2006 when they released EC2. This was released for existing AWS clients. In 2007 this service comes out as a public beta.

2008 EC2 becomes public (out of beta).

EC2 was the first big step into the cloud computing world. So was S3 and SQS

1994 -> Amazon
2000 -> Merchant.com
2006 -> EC2
2007 -> EC2 became public beta
2008 -> EC2 

Amazon is twice as big as Azure, very big and heavy weight

## Moving our Website to the Cloud (IaaS)

In the examples viewed in the lessons we are talking about someone that has an ecommerce website. The server for this website is inside the house computer. Everything from storage to web app is running within the house computer (on prem). This presents a lot of risk. The computer can be damaged, stolen, stop working, etc. Likewise, maintaining this server is expensive and hard. You like to maintain code, but not a hardware/infrastructure. 

To combat this problem, you can get rent a virtual machine from a cloud provider. In this example we get the EC2 service from Amazon. Now you don't have to worry about maintaining the server, that is done by AWS. This offers:
- Increased flexibility. 
- Increased user experience.
	- This is because you are now able to handle more users - elasticity. 

But this architecture still presents a little risk, you want to build resilient and flexible systems. The risk here is that the EC2 instance is being used as storage. To solve this, we can get an additional machine to run the database for our application. So now we have:
- A machine that handles the web app
- Another VM that handles the database
	- This service is called RDS (the professor mentioned that there are around 4 storage services offered by AWS)

![[Pasted image 20250602174146.png]]

If you want to start storing data that changes all the time, images, videos, prices, orders, data that is not very structured, you can get an additional service: S3. 

![[Pasted image 20250602174604.png]]

You can create 'stack able' versions of EC2, one VM on top of the other and each machine can efficiently communicate to the S3 storage and the database. Being able to create replicas of your original VM grants the user with a lot of flexibility. 

Having this system (the one in the screenshot above) allows us to have a resilient system.

One note: You can use a EC2 instance as storage, the issue with this is that a EC2 instance can't share files/storage with another EC2 instance. Each instance is isolated. But both can easily communicate with the database or the S3 storage 

![[Pasted image 20250602181859.png]]

There is also block storage, which can be thought of as external hard drive. This can be plugged to a EC2 instance and then another and so forth just like a SSD.

## Security 

We have a public address in our web app that can be accessed by anybody. This presents a security risk but in order to tackle this we can encapsulate this instance and the database inside a VPC (Virtual Private Cloud). 

This way only us can access the database Essentially this is a virtual private network that allows for secure communication between our systems

You can also put the EC2 instances inside a VPC so that only users can access your web app

![[Pasted image 20250602182709.png]]

*ELB* (Elastic Load Balancer) can be attached to our network to effectively distribute users across our different EC2 instances. That way it doesn't get crowded in one and the user experience is not affected

Then, what happens if we need more EC2 instances? We can add VMs manually but that can be troublesome. For this we have autoscaling. We set rules to determine when to add and remove servers. 

Example:
- Add servers on Thursday to be ready for black Friday. Remove them on Monday
- Add servers when the capacity of server (1) reaches 80%
- Add servers on the weekend, remove them on the weekdays

*Note: AWS manages the autoscaling of the Database and S3 storage but we decide how to scale our EC2s*

All websites have an address - google.com, amazon.com, etc. - and this address needs to be translated into a IP address. This is done by the DNS server. 

Route 53 -> This is a translating mechanism that is offered by Amazon. If you are hosting your website through AWS, you can add Route 53 service so that the translation process happens geographically close to the user, making your app extra efficient. 

- All these services improve the user experience. They make it faster for the client to get to the web app 

![[Pasted image 20250602183130.png]]

Another networking service offered by amazon is a Cloud Front. 

Cloud Front -> Content distribution network. Proxy server that distributes your content geographically through the ISB network. This allows you to deliver content to your users real fast. 

![[Pasted image 20250602183557.png]]

 
How I understand this is -> The server contains all your information needed to offer your web app. This is a web that covers different geographical areas. If you are in Austin, if will process your request in the most nearby server area, for example Dallas. 


