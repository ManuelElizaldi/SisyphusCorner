# Creating an Auto Scaling Group Hands on Video
I have already created on in the previous TIO. But now I am watching the instructor do it

#### Purchase options and instance types:

*Adhere to launch template* -> Auto scaling group uses an Instance Template to create instances. 

*Combine purchase options and instance types* -> this deployment option has more settings, it has more customization parts

#### Instance distribution
*On-demand instances* -> prioritized, launches instances in a given order. Allows for saving plans. 
- Base capacity.
- Order of reserved instances matter.
- Saving plans grant flexibility that allow you to save money. 
- VCPUs

On demand means instances that are going to run no matter what

Order of instance launching:
![[Pasted image 20250619105340.png]]

*On-demand percentage above base* -> Define the percentage split of On-Demand instances and spot instances for your additional capacity beyond the base portion. 
- Here you determine how many on demand and how many spot instances

*Spot Allocation Strategy*
- Capacity optimized -> If you want to retain your instances for longer. This is recommended 
- Lowest price -> If you don't care about duration, it cost less. You specify how many you want. 

Difference between the 2 -> availability is not uniform, the capacity of these spots instances is not guaranteed nor it is constant. 

You can divide your instances in on demand AND spot

#### Networking
Network settings are constant for Auto Scaling Groups:
You select the subnets -> network set up stays the same, its constant

#### How are these instances going to receive traffic?
You can enable load balancing or not. If you DO select the load balancer option, make sure to add a target group

##### Practice Quiz Question: What instance types are compatible with AWS Auto Scaling Groups?
On demand and spot 

#### Enable scaling protection
If you enable this, at no point in time the Auto Scaling Group will remove instances. 

You have to have an observation period -> in cloud you don't guess. You measure everything. Hard numbers justify your decision.

Removing instances = removes data. So how do you handle applications that hold data like a NoSQL database? You enable Auto Scaling Protection

#### Adding notifications
Sends notifications to your phone, email or http server based on what instances where added or removed 

You are notified when an actions happens

You can use notifications to avoid -> Denial of service attacks

#### Practice Quiz Question: In which scenario one should go for Reserved Instance? (H = Hours of observation Window; Z = Hours of zero utilization)
Reserved Instance cost for H hours < Dynamic Instance cost for (H - Z) hours

#### Cloud Watch
You get notifications based on metrics and conditions, you can also get notified for *anomaly detection*.

#### Practice quiz question: What are the scaling options with AWS Auto Scaling Group?
Predictive scaling, schedule based scaling, manually specify all scaling parameters 

# Self Healing
capability to automatically detect and repair any errors and failures that occur. This type of deployment can detect and fix problems without any manual intervention, reducing downtime, and ensuring continuity of service.

Instance replacement if failure occurs 

When you delete a ASG, you only delete the instances that it has created or that are assigned to it. 


#### Practice quiz question: In an autoscaling group during steady state the desired capacity can be lower than minimum capacity.
False

Scaling limits represent the minimum and maximum group size that you want for your Auto Scaling group. You set limits separately for the minimum and maximum size. **Minimum capacity** represents the minimum group size. When scaling policies are set, they cannot decrease the group's desired capacity lower than the minimum capacity.