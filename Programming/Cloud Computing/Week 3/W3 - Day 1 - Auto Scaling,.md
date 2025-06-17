[[Autoscaling]] [[Elasticity]] [[Monitoring]]
 
# Autoscaling 
self healing 

Ideally instead of having a fixed number of instances inside a target group, you have a number of instances that go up or down based on demand -> autoscaling group

*Autoscaling group* -> has the ability to monitor utilization, and when a certain threshold is reached, it takes an action. This is based on 'ifs'. Examples:
- If CPU > 80% + 2 instances -> upper limit 
- If CPU < 80% - 2 instances -> lower limit
- Min size -> minimum contribution to target group -> 1 instance for example, at any point in time the auto scaling group will contribute 1 instance 

This depends on *Cloud Watch* -> Monitoring capabilities that raise an alarm. Rules for the autoscaling group are set in the Cloud Watch.

Alarm -> Cloud Watch
Adding instances -> Auto Scaling Group

## Adding your application to the new instances

*Custom AMI* -> Building your own OS
#### Launch Configuration:
*Bootstrap scripts/User data* -> runs with root privileges. It gives the instance a template of all the requirements and dependencies/settings 

The Autoscaling group takes in this config file script. 







