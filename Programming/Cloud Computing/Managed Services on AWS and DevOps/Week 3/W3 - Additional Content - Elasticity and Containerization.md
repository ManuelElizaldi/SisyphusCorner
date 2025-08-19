[[Containers]]

# Containers 
Simple, Repeatable - allow to work in multiple systems, easy to package into simple deployable and easy to maintain. Lastly allow scalability.

## Scaling model
Classic model -> capacity model (determine how many servers you need). This gives you a fixed parallel capacity/utilization line.

A and C is under utilization

B is over utilization -> we are not serving the customers a this point
![[Pasted image 20250811180336.png]]

Incrementing scalability - elasticity - utilization follows the load
Provisioning time - You deploy your resources moments before the load is increased
![[Pasted image 20250811180520.png]]

You have to be careful in planning how are you adding capacity to the cluster. You want to avoid having over utilization 

