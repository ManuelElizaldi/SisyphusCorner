# Cloud Formation Overview

## Infrastructure as Code
IaC -> creating reusable infrastructure, designing the complete specifications. It creates as a template that can be reused and repeated again and again. 

For example, let's say you have an environment with 2 servers each with load balancers, EC2s, etc. Launching this environment again and again can be time consuming, so you create code that lets you deploy automatically. With this approach you also avoid human input errors. 

One readable file in json format as template. This file is placed in *CloudFormation* and the infrastructure is deployed


## CloudFormation
No charge, easy to use way to create and manage a collection of AWS resources. 

The collection of this resources is called *stack*

version control your infrastructure

Template -> CloudFormation -> Stack 
Parameter definition -> creation of resources, error detection, updates, etc. -> Configured AWS resources are created

You can launch and delete +100 resources easily. This becomes very useful when you have a large environment that needs to be managed 

### Json config file
it contains description, parameters, resources, outputs and the template version

*Parameters & Resources* ->This json file is flexible, you can specify an instance version/AMI or not define it so that any user can choose which one to use

Inside resources you specify the type of resource you are creating. Each resource has a *logical name*. You can look up the documentation to determine the name. 
- When building this file, you usually refer to the documentation 

You can specify what *outputs* you want after creation, for example instance ID  

*Ref* is used in parameters and logical name to refer to an object created within the json file which you want to reference inside another section. This is just like variable calling in programming. 


![[Pasted image 20250908182525.png]]

Same as code deploy, there is an artifact that is stored in an S3 bucket and that is referenced to create the infrastructure 

### Other config concepts

*Mapping* -> AMI are regional, so how do you ensure that a config file works in different regions? If you hard code it, the build fails. So with mappings you can create a table that maps values. For example:
- In N.Virginia -> x.2 should be the AMI 
- In Georgia -> x.3 should be the AMI, etc. 

![[Pasted image 20250908185143.png]]

**Example of mapping above, based on the choice of instance type an architecture is chosen.** This is used with conditions to build EC2 instances. 

*Conditions* -> Construct that allows to choose if a resource is created or not.  

*Pseudo Parameter* -> You don't have to define this parameter. This parameters just exist


# Demo
## Continuous Delivery 
Code changes are automatically built, tested and launched. *CloudFormation + Code Build* allows you to do this. 

Parameter 
	- Key name
		- type -> AWS::EC2::
	- Env type 
		- allowed values -> [test, prod]
	- SSH location

Conditions
![[Pasted image 20250908184307.png]]

You create a function that evaluates a section of your infrastructure, here we are evaluating if the environment type is production. In the lesson video, if this evaluation is true, it also launches other production resources like Web Servers

Security Groups are also specified inside the config file 

### Condition example from video
If the its a prod env -> 2 web servers were created 
if the condition is false for prod env -> only 1 web server will be created 

## Cloud Front
When starting, inside Cloud Front, you create a stack 

The templates (json file) can be created from a sample, use the designer tool or upload a file
- uploading a file can be done through S3 or as a file in your machine

Inside the Stack Creation window - These parameters are determined by the parameters inside the config json file:
![[Pasted image 20250909191125.png]]

The permissions created inside cloud formation are the permissions you want your CloudFormation service to assume
- not EC2 IAM role
- Compliant template 

*Stack Policy* -> determines if specific resources can be upgraded or not. With no policy, everything will be updated. 

*SNS* can be set up in CloudFormation
- create a topic that tracks cloud formation

*Rollback configuration* -> If something is stuck or broken, if will roll back the resource. 
- roll back -> revert to a working state. 

*stack creation options* -> roll back on failure enabled means that if 1 thing break, everything gets rolled back, even the successful resources. This is enabled by default 
- Termination protection -> disabled by default. If you enable, it wont let your delete the stack. 
- Timeout -> time it waits if something break to then do a roll back or cancel the creation. 

### After creation
You can track the status of your resources on the Resources tab 

You can check the parameters 

The professor compared the Description values to the Key Pair values to ensure the resources had the right config. He also check the json file to compare with the description. He checked the AMI id in the json and compared it to the EC2 instance that got created. 


## Demo with Custom VPC 
Custom VPC with 4 subnets (2 private, 2 public)


![[Pasted image 20250910155904.png]]


There is a *"Depends on"* filed that can be placed. This means that what ever is inside this filed needs to be created first then the other resource can be created, for example, in a load balancer target group, you first need to create the web servers (target group), then the target group is created

![[Pasted image 20250910160242.png]]

## Designer Interface
This allows you to build the json config file with tools like drag and drop, autocomplete, etc. 

If you paste a json file into the designer tool it will generate a Diagram of your architecture.

From the Designer tool you can create a stack 

# CloudFormation Script Generation using Gen AI TIO
