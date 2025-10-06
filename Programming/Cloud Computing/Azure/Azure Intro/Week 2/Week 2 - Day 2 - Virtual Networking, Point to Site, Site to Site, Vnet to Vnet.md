[[Point to Site]] [[Virtual Networking]] 
# Point to Site Connection
Connecting to a on prem network from outside. For example, when I connect to CHS via a VPN. 

User connect to the private network:
![[Pasted image 20250930142823.png]]


There are a couple of protocols that can be used to establish this connection: 
- IPSec Tunnel
- SSTP tunnel for Windows machines 
- Open VPN
- Internet with encryption

VPN establishes a connection using the protocols 

# Site to Site Connection 
Connecting the on prem VPN gateway and the cloud virtual network - via the VPN gateways

Creating another VPN Gateway in the cloud that acts as a bridge between the on prem and the cloud.

![[Pasted image 20250930143645.png]]

With this set up you need to be careful **to not exclude** the on prem VPN with a security group.

There is some latency that is introduced with this set up since you are connecting the VPN gateways
- bandwidth is limited
- speed is limited 

This is also very similar to when I access google cloud in CHS. 

## What if both on prem and cloud have same IPs?
IPs need to be mutually exclusive, if there is an IP that is conflicting, the S2S connection wont work. There are work arounds, but directly this wont work. 

# VNET to VNET Connection
Different departments or different organizations that want to connect their clouds.

You can connect two azure clouds together, but not another cloud. 

This connection happens through the VPN Gateway that has a public IP 

In this connection type, traffic is flowing through the *Azure backbone network - Microsoft's own private network*

**In S2S and P2S connection, traffic flows through the internet unless you use another service to route traffic through a private network**

![[Pasted image 20250930145424.png]]

This can also be classified as a S2S connection but if it's set up as that, the traffic will flow through the internet. 

# Vnet peering 
Solution to the limited bandwidth and speed of a Vnet to Vnet. It also goes through the private backbone network. It allows connection between 2 clouds. 

**The only consideration is that this is UNENCRYPTED, but no bandwidth and speed limit.**

**No traffic over the internet**

This acts as one cloud 

Unless you have strict compliance rules, Vnet peering is better than Vnet to Vnet 

![[Pasted image 20250930150940.png]]

# Express Route
On prem connects to Azure cloud but traffic flows through a private network 
![[Pasted image 20250930151006.png]]

This happens through a service provider (internet providers AT&T or Verizon, etc.)

Essentially its a private line between the on prem infrastructure to the cloud. 

Banking or other critical applications that can't have information flow through the internet can use this approach 





