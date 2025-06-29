# Introduction
## Share responsibility model
Division of responsibility between customer and AWS. 

Security is a priority of AWS 

Customer -> responsibility for security *in* the cloud
- Customer data
- Platform, application, identity, access management 
	- access management -> resource access, who can use the instances 


AWS -> responsibility for security *of* the cloud 
- They will make sure the data is secure 
- Software and hardware 

### Diagram:

![[Pasted image 20250613142324.png]]
## IAM

IAM is a core service that helps customer achieve security in the cloud. This service allows admins to create and manage identities, providing them with the necessary tools. This is driven by the enterprise.

*Identity* -> uniquely identify users, granting them permissions defined by the business. 
- Team, department

*Access management* -> Who can do what? What can you access.
- *Principle of least privilege*, grant users with the minimum of permissions needed to perform their job. Don't grant extra permissions. 

#### Practice quiz question -> What does IAM stand for?
Identity and access management 

### Importance of IAM

Some benefits:
- Auditing control, manage, analyze access. 
- Monitor actions taken by users
- Compliance
- Data integrity
- Security guardrails
- Granting the right permissions
- Detect security breach
- Determine level of access 
- Securely manage workload access for agility 

If you are not careful with data integrity and compliance by setting the right permissions you can have financial and legal consequences 

# IAM Concepts & Accessing IAM 

Resource & Service -> Resource is a component within a service. If a car is a service, the engine is a resource. 
- EC2 is a service comprised of many resources. An instance is a resource of EC2 
	- Compute, networking, storage are resources of the EC2 service 

ARN -> Amazon resource name. Used to identify resources 

*Action or Operation* -> What can you do to a resource: editing, creating, deleting, etc. 
- EC2 contain many actions for its resources. 

*You have a service with resources, the resources have actions & operations. The IAM manages the actions you can do. *

IAM Principal -> Entity that can make requests for specific actions in AWS resources. Individual or system that needs permission to interact with resources. 

Request -> When the principal takes action in the Amazon Web Console, like creating a EC2 instance. The request contains info about the principal, like username, permissions, type of request, etc. 
#### Practice Quiz Question -> ARN stands for?
Amazon Resource Name

Authentication -> user validation, credential validation. There's two factor as well. 

Authorized -> determines what resources or actions an authenticated user can access based on their permission

Workload -> Multiple services working together to host an application 
- Specific task, application or process that are hosted and executed within AWS. 
- Single or multiple 
- *Also referred as the IT landscape*

*Bonus note -> AWS Management Console -> Web based interface that allows users to access and manage various AWS services*

# Core Features - IAM 

User groups -> buckets of users with similar permissions. Group users based on their jobs. 

Role management -> digital identity, who or what service can perform what actions. 

#### Practice Quiz Question -> Which IAM component represents an AWS user or application and holds information about permissions 
IAM user

Policies for granular control -> rules and guidelines of what can be performed on AWS resources by user, user group or service 
- Read, write on resources. You can attach this to the IAM user 

Integrated with many AWS services -> makes sure the right people have the correct permissions. Manages user access. Admins don't have to set up different systems 

MFA -> Multi factor authentication 
- MFA is mandatory 

Compliance -> All the security measures to ensure the right use of AWS, least privilege principal, authentication, etc. 

IAM Global and free to use, regardless of region, you can use IAM. 


#### Practice Quiz Question -> What is true about the Shared Responsibility? 
Customer is responsible for security in the cloud
AWS is responsible for security of the cloud 

