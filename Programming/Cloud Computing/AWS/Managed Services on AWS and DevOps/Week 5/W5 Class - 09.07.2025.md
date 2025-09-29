[[DevOps]]
## CI/DI Practices on AWS

SDLC (Software delivery life cycle) personas:
Dev -> App Teams - Code Repo 
UAT -> Unit Testing QA Tester 
Staging ->  Release Management 
Production ->  Operation 

*This is an approach that has been done for the last decades*
*Why CI/DI?*
- An issue with this approach is that there's a lot of miscommunication, pipeline is not as smooth, there's silos. There's also a pace of delivery, for example a quarterly roll out, but issues can arise and delay the production.  Another delay/friction point is caused by upgrading infrastructure 

Sprint Cycle (2 - 3 weeks cycles) 

## DevOps Practices

*Shift left* -> It means about thinking about vulnerabilities, cost optimization, security, reliability and other aspects day 1 of the application, instead of fixing after deployment. 

*DevOps Model* -> Deliver applications and services at high velocity. Prevent silos, there's integrated team (2 pizza team)
- 2 pizza teams -> you can feed the team with 2 pizzas 

If you don't know how to implement something - for example security measures - cloud providers offer AWS [Well - Architected](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html) approach 


[Continuous Delivery and Continuous Deployment](https://aws.amazon.com/devops/continuous-delivery/)

## How to go fast in DevOps
Micro services - breakdown a huge application into smaller apps that take care of services 

Amazon.com:
- UI (1m -> 3m) - You might think you are alright with a certain capacity, but you can receive more users.
- Catalog (constantly updating catalog)
- Shopping Cart (DB scaling)
- Notifications

![[Pasted image 20250907095242.png]]

Avoid monolithic applications -> Everything is compiled together. Everything is on the same programming language. Everyone goes into the same QA testing. 
- Is is better to breakdown into micro services, and each team can handle a different part of the application. 

Important considerations -> Sometimes it is better to use monolith approach. It just depends on the context. 

## CI/CD Hands On
## CodeCommit -> CodeBuild -> CodeDeploy } Code Pipeline 

Code Commit is no longer available for new customers, there is little value for new customers. You have to use Github for this. 
- The professor is still able to create a repo for example. 
- if you use GitHub, you have to authenticate AWS on Github 

1) where are you storing the code 
2) how do you build it
3) how do you deploy it 

Code Build -> 

Code Deploy -> Deployment group, how you want to deploy, service role (required permissions),  

*According to the professor, the most tricky thing is to set up the IAM permissions*

## CloudTrail
API activity tracking 

You have to enable - once you do, it will start recording. It can become costly if you are not careful. 
- There's things you don't know you don't know. 
- *professor's recommendation -> enable in areas where you don't use it. For example, enable in India even though you don't use that region. If someone starts doing bitcoin mining with your resources you want to know. You want to track activity in unusual activities*

---
### Sources
https://aws.amazon.com/devops/what-is-devops/
https://aws.amazon.com/devops/continuous-integration/
https://aws.amazon.com/devops/continuous-delivery/
https://docs.aws.amazon.com/codedeploy/latest/userguide/welcome.html
https://aws.amazon.com/cloudtrail/

