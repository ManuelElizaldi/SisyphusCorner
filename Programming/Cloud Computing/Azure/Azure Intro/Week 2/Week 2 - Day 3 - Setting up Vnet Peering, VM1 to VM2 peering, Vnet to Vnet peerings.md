[[Azure]] [[Network]]  

# Creating a Vnet Peering
Connect networks between 2 clouds. Resources in each cloud can connect/ talk to each other through private IPs

> [!NOTE] When doing Vnet to Vnet connection
> You need to establish a connection between two VPN Gateways. So you need to deploy this two resources in each cloud to create the connection. 
> Vnet Peering does not require 2 VPN gateways. 

All traffic flows through the backbone network but all traffic is unencrypted. 

no bandwidth limit 

VNet peering can be done in the same region or different regions. Same for subscription. 

### Hands on: Creating a Peering connection between VM1 and VM2 
ICMP protocol is needed to ping an IP

Open VM1 and VM2, from VM1 ping VM2, but first you need to allow the ICMPv4 protocol 

We also need to make sure these VMs can connect to each other

go to Vnet 1 -> peering -> initiate peering with VM2 -> status *Initiated states 
- No connection established yet
go to Vnet 2 -> peering -> initiate peering with VM2 -> status: *connected*)
- After you initiate both, then you are connected

*Traffic forwarded from remote virtual network* -> This means that if you have a VM3 connected to VM2, and traffic goes from VM3 to VM2 then to VM1: do you want traffic originated from VM3 to be allowed into VM1? 

You set up the peering on both ways 

# Hub and spoke topology 
Transitivity -> Vnet3 -> Vnet2 -> Vnet1. This does not work unless you establish a peering between Vnet 2 and Vnet 3

#### what is a hub and spoke topology:
One Vnet acts as a Hub, spokes Vnet peer to the hub 


**Allow Gateway Transit** -> Vnet peered can use the VPN Gateway.
- This is turned on inside the Hub, which *has a VPN Gateway*
- Vnet 2 and Vnet 3 can use the VPN Gateway as a transit. 
 
**Use Remote Gateways** -> This is enabled in the spoke so that this Vnet can use a VPN Gateway as a transit.
- This Vnet needs to now have a VPN Gateway 
![[Pasted image 20251007161552.png]]

 