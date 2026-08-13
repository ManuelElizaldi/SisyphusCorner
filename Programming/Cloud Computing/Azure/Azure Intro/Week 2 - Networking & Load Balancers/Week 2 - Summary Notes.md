**Microsoft Azure - 2**

  

- **Configuring Network Security Groups**
    

- Azure network security group filters network traffic to and from Azure resources in an Azure virtual network.
    
- Applied at subnet or NIC level
    
- A network security group contains security rules that allow or deny inbound network traffic to, or outbound network traffic from, several types of Azure resources.
    


![[Pasted image 20251008182830.png]]

- For each rule, you can specify source and destination, port, and protocol.
    
- A network security group contains zero, or as many rules as desired, within Azure subscription limits.
    
- Default security rules are created by Azure in each network security group that you create.
    

  

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview#default-security-rules](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview#default-security-rules)

  

  

  

  

- **Network Security Group flow** logs is a feature of Azure Network Watcher that allows you to log information about IP traffic flowing through an NSG.
    

- Flow data is sent to Azure Storage accounts from where you can access it as well as export it to any visualization tool, SIEM, or IDS of your choice.
    

  

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview#introduction](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview#introduction)

  

  

- **Virtual Network Security** could be defined as the process of protecting resources from unauthorized access or attack by applying controls to network traffic.
    

- The goal is to ensure that only legitimate traffic is allowed.
    
- Azure includes a robust networking infrastructure to support your application and service connectivity requirements.
    
- Network connectivity is possible between resources located in Azure, between on-premises and Azure hosted resources, and to and from the internet and Azure.
    

  

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/security/fundamentals/network-overview](https://docs.microsoft.com/en-us/azure/security/fundamentals/network-overview)

  

  

- **Azure Bastion** is a service you deploy that lets you connect to a virtual machine using your browser and the Azure portal. The Azure Bastion service is a fully platform-managed PaaS service that you provision inside your virtual network.
    

- It provides secure and seamless RDP/SSH connectivity to your virtual machines directly from the Azure portal over TLS.
    
- When you connect via Azure Bastion, your virtual machines don't need a public IP address, agent, or special client software.
    

![[Pasted image 20251008182846.png]]

  

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/bastion/bastion-overview](https://docs.microsoft.com/en-us/azure/bastion/bastion-overview)

  

- **Azure Firewall** is a cloud-native and intelligent network firewall security service that provides the best of breed threat protection for your cloud workloads running in Azure.
    

  

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/firewall/overview](https://docs.microsoft.com/en-us/azure/firewall/overview)

  

- **Distributed denial of service (DDoS)** attacks are some of the largest availability and security concerns facing customers that are moving their applications to the cloud.
    

- A DDoS attack attempts to exhaust an application's resources, making the application unavailable to legitimate users.
    
- DDoS attacks can be targeted at any endpoint that is publicly reachable through the internet.
    

  

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/ddos-protection/ddos-protection-overview](https://docs.microsoft.com/en-us/azure/ddos-protection/ddos-protection-overview)

- **Connectivity between different networks**
    

- **A Point-to-Site VPN** gateway connection lets you create a secure connection to your virtual network from an individual client computer.
    

- A P2S connection is established by starting it from the client computer.
    
- This solution is useful for telecommuters who want to connect to Azure VNets from a remote location, such as from home or a conference.
    
- P2S VPN is also a useful solution to use instead of S2S VPN when you have only a few clients that need to connect to a VNet.
    

  

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/vpn-gateway/point-to-site-about](https://docs.microsoft.com/en-us/azure/vpn-gateway/point-to-site-about)

  

- **A Site-to-Site VPN** gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.
    

- This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.
    

![](file:///tmp/lu23077481uvk7k.tmp/lu23077481uvkci_tmp_9e6bd143.png)

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal)

  

- **VNet-to-VNet VPN** connection is a simple way to connect VNets**.**When you connect a virtual network to another virtual network with a VNet-to-VNet connection type (VNet2VNet), it's similar to creating a Site-to-Site IPsec connection to an on-premises location.
    

![[Pasted image 20251008182854.png]]

  

- Both connection types use a VPN gateway to provide a secure tunnel with IPsec/IKE and function the same way when communicating.
    
- When you create a VNet-to-VNet connection, the local network gateway address space is automatically created and populated.
    
- If you update the address space for one VNet, the other VNet automatically routes to the updated address space.
    
- It's typically faster and easier to create a VNet-to-VNet connection than a Site-to-Site connection.
    
- However, the local network gateway is not visible in this configuration.
    

  

Please refer to the given link for more information

https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal

  

- **VNet Peering** enables you to seamlessly connect two or more Virtual Networks in Azure. The virtual networks appear as one for connectivity purposes.
    

  

![[Pasted image 20251008182923.png]]

  

- The traffic between virtual machines in peered virtual networks uses the Microsoft backbone infrastructure.
    
- Like traffic between virtual machines in the same network, traffic is routed through Microsoft's _private_ network only.
    
- Azure supports the following types of peering
    

- **Virtual network peering** connects virtual networks within the same Azure region.
    
- **Global virtual network peering** connects virtual networks across Azure regions.
    

  

Please refer to the given link for more information

[https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-peering-overview](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-peering-overview)

# Create, change, or delete a virtual network peering [https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-peering](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-peering)

[https://docs.microsoft.com/en-us/azure/virtual-network/tutorial-connect-virtual-networks-portal](https://docs.microsoft.com/en-us/azure/virtual-network/tutorial-connect-virtual-networks-portal)

  

- **ExpressRoute** lets you extend your on-premises networks into the Microsoft cloud over a private connection with the help of a connectivity provider.
    

- With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure and Microsoft 365.
    

  

![[Pasted image 20251008182935.png]]

  

Please refer to the given link for more information

https://docs.microsoft.com/en-au/azure/expressroute/expressroute-introduction

  

- # **Hub-spoke network topology in Azure**
    

  

- The hub virtual network acts as a central point of connectivity to many spoken virtual networks. The hub can also be used as the connectivity point to your on-premises networks. The spoke virtual networks peer with the hub and can be used to isolate workloads.
    
- The benefits of using a hub and spoke configuration include cost savings, overcoming subscription limits, and workload isolation.
    

  

![[Pasted image 20251008182943.png]]

  

- **Azure Load Balancer** operates at layer 4 of the Open Systems Interconnection (OSI) model.
    

- Distributes inbound traffic to backend VMs for scalability and HA
    
- Works at Layer 4 of OSI stack
    
- TCP and UDP protocols
    
- Can be used for internet facing (public) and internal applications
    
- Supports multiple applications using multiple IP addresses and ports
    
- Backend VMs must be in the same Virtual Network
    

- VMs can be in different Availability Zones
    

- Supports both inbound and outbound scenarios
    

- Can configure NAT and SNAT rules
    

- Supports IPv6 addresses
    
- Load Balancer types
    

- Public Load Balancer
    

- Public IP address must be specified for Load Balancer
    
- Handles traffic from internet to backend VMs
    
- Backend VMs do not require Public IP addresses
    
- Outbound traffic from VM is translated from private IP of VM to public IP of Load Balancer
    

  

- Internal Load Balancer
    

- Deployed inside Virtual Network
    
- It can be accessed over a private IP address
    

  

![[Pasted image 20251008182952.png]]

Please refer to the given links for more information - [https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview)

https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview#:~:text=With%20Azure%20Load%20Balancer%2C%20you,all%20TCP%20and%20UDP%20applications.

  

- **N-Tier Architecture**
    

  

![[Pasted image 20251008183016.png]]

  

- An N-tier architecture divides an application into logical layers and physical tiers.
    
- Consider an N-tier architecture for
    

- Simple web applications.
    
- Migrating an on-premises application to Azure with minimal refactoring.
    
- Unified development of on-premises and cloud applications.
    

  

- N-tier architectures are very common in traditional on-premises applications, so it's a natural fit for migrating existing workloads to Azure.
    

  

Please refer to the given links for more information -

https://docs.microsoft.com/en-us/azure/architecture/guide/architecture-styles/n-tier

  

- **Inbound NAT Rules** are used to forward traffic from a load balancer frontend to one or more instances in the backend pool.
    

- There are two types of inbound NAT rule available for Azure Load Balancer, single virtual machine and multiple virtual machines.
    

  

Please refer to the given links for more information -

[https://docs.microsoft.com/en-us/azure/load-balancer/inbound-nat-rules](https://docs.microsoft.com/en-us/azure/load-balancer/inbound-nat-rules)

  

- # **Floating IP** Some application scenarios prefer or require the same port to be used by multiple application instances on a single VM in the backend pool. Common examples of port reuse include:
    

- # clustering for high availability
    
- # network virtual appliances
    
- # exposing multiple TLS endpoints without re-encryption.
    

Please refer to the given links for more information -

https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-floating-ip

  

#   

- # **Outbound rules** allow you to explicitly define SNAT(source network address translation) for a public standard load balancer. This configuration allows you to use the public IP(s) of your load balancer to provide outbound internet connectivity for your backend instances.
    

- This configuration enables:
    

- IP masquerading
    
- Simplifying your allowlists.
    
- Reduces the number of public IP resources for deployment.
    

  

Please refer to the given links for more information -

[https://docs.microsoft.com/en-gb/azure/load-balancer/outbound-rules](https://docs.microsoft.com/en-gb/azure/load-balancer/outbound-rules)

  

- # **Azure Load Balancer SKUs**
    

# Azure Load Balancer has three SKUs - Basic, Standard, and Gateway. Each SKU is catered towards a specific scenario and has differences in scale, features, and pricing.

  

  

![[Pasted image 20251008183046.png]]

  

Please refer to the given links for more information -

[https://docs.microsoft.com/en-us/azure/load-balancer/skus](https://docs.microsoft.com/en-us/azure/load-balancer/skus)

#   

- # **Azure Application Gateway** is a web traffic load balancer that enables you to manage traffic to your web applications.
    

- Web traffic load balancer to handle traffic for web applications
    
- Works at Layer 7 of OSI stack
    
- HTTP and HTTPS protocols
    
- Can be used for internet facing (public) and internal applications
    
- Application layer routing
    
- route traffic based on URL
    
- Redirect traffic to backend VMs / VM Scale Sets / Azure App Services
    
- / external sites
    
- Web Application Firewall (WAF) to protect apps from web
    
- vulnerabilities
    
- Use it together with other Load Balancing services
    
- **Features**
    

- Zone redundancy
    
- Autoscaling support
    
- Static Frontend IP
    
- Multiple backend resource types–VM, VMSS, App Services, IP Address
    
- Session affinity and connection draining
    
- Multiple listeners and multiple-site support
    
- Redirection support
    
- Path-based routing
    
- Rewrite HTTP headers and URL
    
- Custom error pages
    
- SSL/TLS termination and end-to-end SSL/TLS support
    
- Web Application Firewall (WAF) support
    

  

Please refer to the given link for more information -

[https://docs.microsoft.com/en-us/azure/application-gateway/overview](https://docs.microsoft.com/en-us/azure/application-gateway/overview)

  

- # **load-balancing services in Azure** provide global DNS load balancing. It looks at incoming DNS requests and responds with a healthy endpoint, in accordance with the routing policy the customer has selected. Options for routing methods are:
    

- **Traffic Manager** provides global DNS load balancing. It looks at incoming DNS requests and responds with a healthy endpoint, in accordance with the routing policy the customer has selected.
    
- **Application Gateway** provides application delivery controller (ADC) as a service, offering various Layer 7 load-balancing capabilities for your application.
    

- It allows customers to optimize web farm productivity by offloading CPU-intensive TLS termination to the application gateway.
    
- Other Layer 7 routing capabilities include round-robin distribution of incoming traffic, cookie-based session affinity, URL path-based routing, and the ability to host multiple websites behind a single application gateway.
    
- Application Gateway can be configured as an Internet-facing gateway, an internal-only gateway, or a combination of both.
    
- Application Gateway is fully Azure managed, scalable, and highly available. It provides a rich set of diagnostics and logging capabilities for better manageability.
    

- **Load Balancer** is an integral part of the Azure SDN stack, providing high-performance, low-latency Layer 4 load-balancing services for all UDP and TCP protocols. It manages inbound and outbound connections.
    

  

Please refer to the given links for more information -

[https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-load-balancing-azure](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-load-balancing-azure)

https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-how-it-works#how-clients-connect-using-traffic-manager

  

- **Routing Methods**
    

- Azure Traffic Manager supports six traffic-routing methods to determine how to route network traffic to the various service endpoints.
    
- For any profile, Traffic Manager applies the traffic-routing method associated with it to each DNS query it receives.
    
- The traffic-routing method determines which endpoint is returned in the DNS response.
    
- The following traffic routing methods
    

- [**Priority**](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-routing-methods#priority-traffic-routing-method) **:** Select Priority routing when you want to have a primary service endpoint for all traffic.
    

- You can provide multiple backup endpoints in case the primary or one of the backup endpoints is unavailable.
    

![](file:///tmp/lu23077481uvk7k.tmp/lu23077481uvkci_tmp_7d2de918.png)

- [**Weighted**](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-routing-methods#weighted) **:** Select Weighted routing when you want to distribute traffic across a set of endpoints based on their weight.
    

- Set the weight the same to distribute evenly across all endpoints.
    

![](file:///tmp/lu23077481uvk7k.tmp/lu23077481uvkci_tmp_7aa6a886.png)

- [**Performance**](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-routing-methods#performance) **:** Select Performance routing when you have endpoints in different geographic locations and you want end users to use the "closest" endpoint for the lowest network latency.
    

![](file:///tmp/lu23077481uvk7k.tmp/lu23077481uvkci_tmp_aaf0b807.png)

- [**Geographic**](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-routing-methods#geographic) **:** Select Geographic routing to direct users to specific endpoints (Azure, External, or Nested) based on where their DNS queries originate from geographically.
    

- With this routing method, it enables you to be in compliance with scenarios such as data sovereignty mandates, localization of content & user experience and measuring traffic from different regions.
    

![](file:///tmp/lu23077481uvk7k.tmp/lu23077481uvkci_tmp_f8faf18d.png)

- [**Multivalue**](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-routing-methods#multivalue) **:** Select MultiValue for Traffic Manager profiles that can only have IPv4/IPv6 addresses as endpoints.
    

- When a query is received for this profile, all healthy endpoints are returned.
    

- [**Subnet**](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-routing-methods#subnet) **:** Select Subnet traffic-routing method to map sets of end-user IP address ranges to a specific endpoint.
    

- When a request is received, the endpoint returned will be the one mapped for that request’s source IP address.
    

  

  

#   

#