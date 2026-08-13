
A/B testing is normally conducted to introduce new functionality or UI changes for user feedback. This necessitates the use of multiple application servers in the same target group hosting different versions of the application, one with the new features and one without. How can you make sure that a particular user only receives a certain version of the application and doesn’t switch versions midway?

- Enable session stickiness
- Because session stickiness enables the load balancer to send a particular user to the same instance/server. You might have a group of users or user that you want to send to the test server. 
- In my experience during my job at Tethr, we had customers that were sent to newer version of the software. We used them as our guinea pigs. 

An eCommerce company experiences high traffic during the sale period, however, on other days the traffic is predictable. Which is the most cost-effective solution to run uninterrupted business?
- Use reserved instances for predictable traffic and spot instances for the sale period 
- Spot instances are like stocks, if demand goes up, the price goes up and the inverse is true as well. These instances are short lived, that's why they are a good option for a sale event. If you know that there will be a surge in users, you can have these instances ready to go. The only thing you need to consider here is that AWS will reclaim these instances if they are needed else where, if demand goes down or if a on demand user needs them. So you have to build your architecture based on this consideration. 

Which of the following algorithms can be used by a load balancer for canary deployments?
- Weighted routing in target groups
- In this algorithm you determine what % of users go to the testing environment 

An application Load balancer sends traffic to:
- Target groups
- You can place instances, another load balancer inside a target group, database or any other service.

How many roles can be attached to an EC2 instance?
- One role is allowed
- IAM role is a set of permissions that define what actions are allowed or denied on AWS resources. Not tied to a specific user or group
- Roles are not permanent 

An application developer used 6 EC2 instances, 2 each in London, Mumbai, and Oregon for geographical resilience to host the application and now wants to add the instances to a load balancer. Which of the following problems needs to be dealt with?
- The instance in a target group (attached to the load balancer) cannot span across multiple regions. 
- Remember regions have multiple AZs
- EC2 instances are tied to one AZ 

Let’s consider an EC2 instance with a startup script to install and configure some software regardless of earlier installation. If the user makes manual changes to the software configuration and reboots the instance, which of the following outcome is likely to occur if the script ignores the manual updates? Also, assume the cloud-init is customized to run user data every time.
- The changes will be lost
- The script is ran on boot, so the values inside the script will remain and whatever you did manually will be overwritten by the config script 

