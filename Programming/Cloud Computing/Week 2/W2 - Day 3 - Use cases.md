[[Load Balancer]] [[Web Dev]] [[Development]] 
## Lift and Shift Scenario
Customer already has an app on prem and they want to move to the cloud

Session affinity is required on the app

Port 80 -> ALB -> 1 target group, 2 instances (2a, 2b)

The client wants to deploy updates in small chunks (canary deployment). You can create a new Target Group to which you can deploy updates without affecting the original Target Group

You do this through path based routing 
![[Pasted image 20250612123712.png]]

*Canary Release* -> Reduces risk of new feature deployment. It deploys new features to a batch of users while maintaining the 'old' version.

Canary release is an application of *parallel change* -> this is when the migration phase lasts until all users have been routed to the new version

You can always roll back to the old version, but it can be hard to do this. So the idle situation is that you test the new version first

Canary Release allows for slow ramping up of load so you can gather metrics about the new version 
![[Pasted image 20250612124258.png]]

Blue Green Deployment -> All users are migrated to the new version

### Disadvantages of Canary Release 

You have to manage two versions of your application or instances. In some cases, you have more than 2 applications

Six EC2 instances in three TGs with ALB, path based routing and traffic distribution:
![[Pasted image 20250612124835.png]]
TG affinity will be needed to deliver consistent behavior of the application
### Hybrid deployment with central session management, private service & data center connectivity

In this build, the organization is trying to take advantage of their existing capital:

![[Pasted image 20250612125012.png]]

Public load balancer that talks to other TGs

In the previous scenario the webapp-tg stored all the user information inside the EC2 instance (shopping cart, user account info, etc.). The organization wants to migrate/transform their application from statefull to stateless. This allows the organization to turn off the session affinity.  *in a statefull environment, if an instance goes down, all the user data is lost. This degrades the user experience* all of this memory is transferred to a cache  

*Question -> how does the cache work? how does it help going from statefull to stateless? why do we want to do this?*
*min 13:45 from use cases [101 to 104]* 

In the webapp-tg, they added another private application, the traffic for this is managed by a internal/private ALB

In this new scenario, the team added a cache 

## Martin Fowler -> Strangler Pattern 
This pattern says that you can grab an existing/older application and build features around it. All the new features start to handle the work load and in a way strangle the old application. At that point you can consider decommissioning the old app. 

#### Practice quiz question: The customer has an existing application in their own data center, and they want to know what components will be necessary on the cloud when the application is migrated. What are the best options to consider?
EC2 instances, load balancers and target groups 