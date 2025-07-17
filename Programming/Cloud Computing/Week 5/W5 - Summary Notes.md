**Class Notes – Cloud Computing on AWS 4**

  

# Introduction

Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS.

  

![[Pasted image 20250714182716.png]]

  

**Default VPCs**

When you start using Amazon VPC, you have a default VPC in each AWS Region. A default VPC comes with a public subnet in each Availability Zone, an internet gateway, and settings to enable DNS resolution. Therefore, you can immediately start launching Amazon EC2 instances into a default VPC.

  

The following figure illustrates the key components that we set up for a default VPC.

![[Pasted image 20250714182731.png]]


**Subnet basics**

- **Subnet types**
    
    - Depending on how you configure routing for your subnets, they are considered either public, private, or VPN-only:
        
    - **Public subnet**: The subnet has a direct route to an internet gateway. Resources in a public subnet can access the public internet.
        
    - **Private subnet**: The subnet does not have a direct route to an internet gateway. Resources in a private subnet require a NAT device to access the public internet.
        
    - **VPN-only subnet**: The subnet has a route to a Site-to-Site VPN connection through a virtual private gateway. The subnet does not have a route to an internet gateway.
        
- When you create a subnet, you specify its IP addresses, depending on the configuration of the VPC
    
    - **IPv4 only**: The subnet has an IPv4 CIDR block but does not have an IPv6 CIDR block. Resources in an IPv4-only subnet must communicate over IPv4.
        
    - **Dual stack**: The subnet has both an IPv4 CIDR block and an IPv6 CIDR block. The VPC must have both an IPv4 CIDR block and an IPv6 CIDR block. Resources in a dual-stack subnet can communicate over IPv4 and IPv6.
        
    - **IPv6 only**: The subnet has an IPv6 CIDR block but does not have an IPv4 CIDR block. The VPC must have an IPv6 CIDR block. Resources in an IPv6-only subnet must communicate over IPv6.
        


![[Pasted image 20250714182742.png]]
  
![[Pasted image 20250714182753.png]]


**VPC with public and private subnets (NAT)**

- The configuration for this scenario includes a virtual private cloud (VPC) with a public subnet and a private subnet. recommend this scenario if you want to run a public-facing web application, while maintaining back-end servers that aren't publicly accessible.
    
- A common example is a multi-tier website, with the web servers in a public subnet and the database servers in a private subnet. You can set up security and routing so that the web servers can communicate with the database servers.
    

# Route53

Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service. You can use Route 53 to perform three main functions in any combination: domain registration, DNS routing, and health checking.

  
![[Pasted image 20250714182818.png]]


# Features

- **Route 53 Resolver**
    

Get recursive DNS for your Amazon VPC and on-premises networks. Create conditional forwarding rules and DNS endpoints to resolve custom names mastered in Amazon Route 53 private hosted zones or in your on-premises DNS servers.

- **Route 53 Resolver DNS Firewall**
    

Protect your recursive DNS queries within the Route 53 Resolver. Create domain lists and build firewall rules that filter outbound DNS traffic against these rules.

- **Route 53 Application Recovery Controller: Readiness Check**
    

Ensure that your resources across Availability Zones or Regions are continually audited for recovery readiness.

- **Route 53 Application Recovery Controller: Routing Control**
    

Use simple on/off switches, integrated with DNS records of your top-level resources, to failover traffic.

- **Route 53 Application Recovery Controller: Safety Rules**
    

Make sure that specific rules are followed during failover to protect automated recovery actions from impairing availability.

- **Geo DNS**
    

Route end users to a particular endpoint that you specify based on the end user’s geographic location.

- **Private DNS for Amazon VPC**
    

Manage custom domain names for your internal AWS resources without exposing DNS data to the public Internet.

- **DNS Failover**
    

Automatically route your website visitors to an alternate location to avoid site outages.

- **Health Checks and Monitoring**
    

Amazon Route 53 can monitor the health and performance of your application as well as your web servers and other resources.

- **Domain Registration**
    

Amazon Route 53 offers domain name registration services, where you can search for and register available domain names or transfer existing domain names to be managed by Route 53.

- **DNSSEC**
    

Enable DNSSEC signing for all existing and new public hosted zones, as well as DNSSEC validation for Amazon Route 53 Resolver.

- **CloudFront Zone Apex Support**
    

When using Amazon CloudFront to deliver your website content, visitors to your website can now access your site at the zone apex (or "root domain"). For example, your site can be accessed as example.com instead of www.example.com.

- **S3 Zone Apex Support**
    

Visitors to your website hosted on Amazon S3 can now access your site at the zone apex (or "root domain").

- **Amazon ELB Integration**
    

Amazon Route 53 is integrated with Elastic Load Balancing (ELB).

- **Management Console**
    

Amazon Route 53 works with the AWS Management Console. This web-based, point-and-click, graphical user interface lets you manage Amazon Route 53 without writing any code at all.

# Routing

Easy-to-use and cost-effective global traffic management: route end users to the best endpoint for your application based on geo proximity, latency, health, and other considerations.

- **Simple routing policy** – Use for a single resource that performs a given function for your domain, for example, a web server that serves content for the example.com website. You can use simple routing to create records in a private hosted zone.
    
- **Failover routing policy** – Use when you want to configure active-passive failover. You can use failover routing to create records in a private hosted zone.
    
- **Geolocation routing policy** – Use when you want to route traffic based on the location of your users. You can use geolocation routing to create records in a private hosted zone.
    
- **Geoproximity routing policy** – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.
    
- **Latency routing policy** – Use when you have resources in multiple AWS Regions and you want to route traffic to the region that provides the best latency. You can use latency routing to create records in a private hosted zone.
    
- **IP-based routing policy** – Use when you want to route traffic based on the location of your users, and have the IP addresses that the traffic originates from.
    
- **Weighted routing policy** – Use to route traffic to multiple resources in proportions that you specify. You can use weighted routing to create records in a private hosted zone.
    
- **Multivalue answer routing policy** – Use when you want Route 53 to respond to DNS queries with up to eight healthy records selected at random. You can use multivalue answer routing to create records in a private hosted zone.
    

  

  

**References :**

1. **VPC Documentation -** [**https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html**](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
    
2. **VPC Datasheet -** [**https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_VPC_Datasheet.docx.pdf**](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_VPC_Datasheet.docx.pdf)
    
3. **Route53 Documentation -** [**https://aws.amazon.com/route53/**](https://aws.amazon.com/route53/)
    
4. **Route53 Datasheet -** [**https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_VPC_Datasheet.docx.pdf**](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_VPC_Datasheet.docx.pdf)