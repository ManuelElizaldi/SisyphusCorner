[[Network]]

*Endpoints* -> EC2 instance can connect to other services without having to go through the internet 

There's two types of EndPoints 1) Interface and 2)Gateway. 

1) Interface -> network interface in your subnet, privately access services. **This is how you use PrivateLink**
2) Gateway -> Adds a route to your route table and is only used for S3 and DynamoDB

Without endpoint:
![[Pasted image 20250708184127.png]]

With end point
![[Pasted image 20250708184202.png]]


## Route 53
#funfact -> its named after the port used in TCP/UDP for DNS

Global service that helps you build resilient multi-geography distributed applications.

Translates domains like -> www.example.com to -> 192.0.2.1

You can buy and manage domain names through Route 53:
Domain management 
- go daddy plus plus 

It routes users to the closest geographically AZ for lower latency 

It can also route to other servers 

Allows you to pick policies 

If a whole region (where you have your servers set up) fails, Route 53 allows you to route to another region that is available 

 
> [!NOTE] Route 53 Traffic Management 
> This is not a load balancer, load balancers distribute traffic in real time and within the region. 
> 
> Route 53 manages traffic through latency. Not real time. US users to the US load balancer and EU users to the EU load balancer. 


##### Ask about this example mentioned in the video:
You're **mostly right**, but let’s clarify the details — your professor is talking about a **high-availability, multi-region setup**, and yes, **Route 53 can help route traffic to another region** _if Singapore goes down_ — **but only if you've set it up that way**.

# Route 53
3 main functions: 
1) Domain registration -> creating your website's name, like -> www.example.com 
2) DNS routing -> domain name system, phone book of the internet. Translates www.example.com into the IP address. It routes users to the correct server 
3) Health checking

## DNS Routing Policies 
Once the hosted zone is created (AZ, server, etc.) you can decide how to route traffic. 

You can send users to a static site hosted on S3

You can send them based on geo-location:
- Servers in games 
- Based on location 
	- You have 2 load balancer in different regions, you send traffic to each and the load balancers then send the users to their corresponding server.

#### Practice quiz question: Which of the following features will you use if you want to transfer data from an EC2 instance in a VPC directly to an S3 bucket without having the data travel through the public Internet?
VPC endpoint




