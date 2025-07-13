[[VPC]] [[Network]] [[Protocol]]

# VPC TIO
What was achieved in this TIO:
1) created a VPC
2) created a private and public subnet
3) created an internet gateway and NAT gateway 
4) crated a route table and added entries to it 
5) launched an EC2 instance in public and private EC2

# Creating VPC
VPC have their own interface UI where you create the VPC 

There's also a list with the available VPC, in the top right corner I clicked 'Create VPC' just as I created a EC2 instance
- Inside this list you will find the default VPC 

In the VPC settings card is where you define your CIDR block (list of IPs)
![[Pasted image 20250708150850.png]]


Very simple settings card. The above screenshot shows it all. 

# Creating a Subnet 
In the VPC dashboard you can find the UI for subnets 

There's a couple already defined:
![[Pasted image 20250708151117.png]]

In the settings card you define to which VPC this subnet will be attached. 

Also here's where you define the CIDR block for the subnet. If must be within the VPC CIDR block
![[Pasted image 20250708151243.png]]

We also created a private subnet

## Modifying the Public subnet
We enabled the *Auto-assign public IPv4 address*.
- This is turned off on nondefault subnets 

# Creating an Internet Gateway
Again, from the VPC dashboard you select *Internet Gateways*

Another simple settings card:
![[Pasted image 20250708152256.png]]

You need to attach the VPC to the Gateway you created:
![[Pasted image 20250708152414.png]]

# Creating a Route Table
Also selected from the VPC dashboard side menu
![[Pasted image 20250708152809.png]]

In this settings card you attach it to the VPC 

Now inside the Routes table info UI page/manager window you can edit the routes. Like so:
![[Pasted image 20250708153219.png]]

Once inside the edit routes table, you need to define the Destination and the target. *The target is the Internet Gateway we created*
![[Pasted image 20250708153343.png]]

You will also need to define the Subnet association
![[Pasted image 20250708153505.png]]

Since this is a Internet Gateway we selected the public subnet 

# Launching a EC2 instance on the public subnet

Go to the EC2 management console and launch an EC2 instance. The difference from a regular launch that we have done in the past is that in the EC2 launch settings card - network section - you have to select the VPC you created instead of the default 

we also inserted this user data:
```bash
#!/bin/bash yum update -y yum install httpd -y service httpd start chkconfig httpd on IP_ADDR=$(TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` \ && curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/public-ipv4) echo "ASG instance with IP $IP_ADDR" > /var/www/html/index.html
```

some other changes to the EC2 launch:
- We created our own security group that opens port 22 (for ssh) and 80 (for mysql)
	- In the *Source Type* -> custom and the source is the CIDR block `10.0.1.0/24` for the public subnet

This is how it looks:
![[Pasted image 20250708154744.png]]

*All ICMP - IPv4* -> ICMP (Internet Control Message Protocol) is used for network diagnostics and communication, not data transfer

# VPC Peering
When doing VPC peering, there's always a requester and accepter. Here the requester will be the VPC we created and the accepter is the default VPC.

Then you simply accept the request:
![[Pasted image 20250708161645.png]]

You also need to add this to your route tables. To do this, I navigated to the default VPC managment window, I noted down its CIDR block, then navigated to my route table, clicked on edit, and added it:
![[Pasted image 20250708162724.png]]

This is my public subnet with the default VPC CIDR block now available:
![[Pasted image 20250708162744.png]]

We did the same for the default VPC. To be sure we selected the right one, I opened it from the EC2 instance we created 

### I was not able to do step G - Hands-On: SSH and accessing the private EC2 instance
*bastion host*
After watching the VPC TIO video I learned that I had to run the below command in order to add the .pem file from my computer -> public instance -> then from public instance ssh into the private instance

I had to run this 
`scp -i YOUR.pem ./YOUR.pem ec2-user@PUBLIC_IP:/home/ec2-user/YOUR.pem`

I have not done the on hands section yet | as of 07/08/2025

But I saw how it was done in the video, you connect from one instance to another 

# Creating a NAT gateway
Make sure to allow Elastic IP allocation ID 
![[Pasted image 20250708170955.png]]

Create a private route table for this NAT 
![[Pasted image 20250708171158.png]]

And add the corresponding route to the NAT Gateway
![[Pasted image 20250708171228.png]]


# VPC TIO Video 
## Architecture
![[Pasted image 20250708165407.png]]



#### Practice quiz Which of the following can be used to transfer data securely between two EC2 instances created in separate AWS accounts? Select the best fit.
VPC Peering

