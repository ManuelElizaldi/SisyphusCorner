*Which of the following is not true about local VNET Peering?*
It is transitive
Consider 3 virtual networks, A,B,C. A is peered to B and B is peered to C. This does not imply that A is peered to C; A and C will need to be peered explicitly.

*Which of the following is true of internal load balancers?*
They are deployed in a virtual network

Internal load balancers have to be deployed inside a virtual network, which **has to be chosen at the time of creation.**

*Which of the following qualifies as a destination for inbound NSG rules?*
NIC (Network interface card)
Inbound NSG rules can only have the subnet and NIC as their destinations. In contrast, outbound NSG rules have external points as their destination.

*Which of the following VM pricing options offers the most savings over a long-term basis for an Ubuntu VM?*
Reserved VMs
VMs launched using the Reserved VMs plan offer significantly higher savings as compared to pay-as-you-go plans or spot instances for long term deployments. Since the VM uses Ubuntu, the licensing savings from hybrid plans will not be required.

*Which of the following attributes will allow a VNET to use a VPN Gateway connected to a peered VNET?*
Gateway Transit
Gateway transit is a peering property that lets one virtual network use the VPN gateway in the peered virtual network for cross-premises or VNet-to-VNet connectivity.