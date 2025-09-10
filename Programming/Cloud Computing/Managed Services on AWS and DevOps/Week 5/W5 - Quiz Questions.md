**Which of these is not recorded by Cloudtrail?**
- VPC Flow Log
- This is captured by a separate feature called Amazon VPC Flow Logs. This feature records IP traffic going in and out of the network 

**For DevOps principles to be applied successfully in an organization, it is essential to have clear guidelines of which of the following?**
- Business and technical process, team collaboration and automation

**Which of these are valid storage gateway type?**
- File gateway, volume gateway & tape gateway

**In order to automate code deployments, which AWS services seem like a good fit? Select two.**
- CodeBuild
- CodePipeline

Analyze the following escalation email from your customer.

_**Subject: Escalation of Feature Release Velocity**_

Dear John Doe,

I am writing to escalate the issue of the feature release velocity of the application. We have released a number of features over the past few months, but the velocity of these releases has been too slow to meet our goals.

The current velocity of feature releases is not acceptable and needs to be improved. We need to create a plan to increase the speed of feature releases, and ensure that this plan is implemented as soon as possible.

We need to ensure that we are able to deliver features to our users in a timely manner. We need to review our processes and identify areas for improvement. We also need to ensure that we are able to allocate the resources needed to meet our goals.

I appreciate your help in this matter. Please let me know if you have any questions or need any additional information.

Sincerely,

Jane Doe

**What types of AWS service seem like a good fit to address this issue very quickly?**
- Managed Git repository ****
- Code build and artifact store service 
- automating the process of build to deploy using a pipeline


**Under which of the following circumstances would a Git push command from an Ubuntu EC2 instance to CodeCommit fail?**
The instance does not have the relevant IAM permissions


**A development team intends to store cloud deployment related documents along with the code on AWS cloud. Which service is the best fit?**
Code Commit

**What are the advantages of creating a local git repository?**
Offline work 

**You have a customer who has built a unique algorithm that works on highly sensitive data. All this is being hosted on the customer's own data centre. In this scenario, is it advisable for the customer to host the algorithm's code on a cloud-based Git repository? Assume none of the customer's IT systems is on the cloud.**
No, maintain the code in the customer's data centred
The customer seems to be in a highly classified business area and it may be better to take a more defensive approach of managing everything in-house.


**Which of the following is true for CodeCommit?**
Fully managed service, On Demand, Out of the box environments



**Assume you are working as a manager in a software development company. You find a DevOps engineer working on a problem where the code seems to compile fine in the code editor, but somehow the build process cannot create the deployment artifact and is throwing errors. What advice will you give?**
Check for errors in the buildspec file, perhaps syntax errors


**You are working for a company and determine that the buildspec file has changed, and since that time, the build has been throwing errors. This has caused a significant disruption in code release, and the customer is unhappy. Which service will you refer to determine when and who changed the buildspec file?**
CloudTrail


**Which one of these is a mutable deployment ?**
In place develoyment
Mutable infrastructure is an IT environment where servers and other components can be altered after their initial setup, allowing for changes and updates. In-place deployment is one of the deployment strategies available for updating applications running on Amazon EC2 instances. It is sometimes preferred for its simplicity and lower resource requirements.


**You have a legacy application being migrated to the cloud with few cloud resource needs. The application does not need elasticity and other high availability principles, to begin with, but can use these in the future. Do you recommend using cloud automation such as Infrastructure as Code (Cloud Formation) in the initial deployment phase?**
No, it sounds like over engineering
Option 1 is incorrect is because we do not know what the future needs of this simple application will be.


**What is the difference between AWS CodeBuild buildspec and AWS CodeDeploy appspec files?**
*AWS CodeDeploy appspec files* are used to configure the deployment process for an application. They specify the deployment scripts, permissions, and other configuration details for the deployment environment.

*AWS CodeBuild buildspec files* are used to configure the build process for a project. They specify the environment variables, build commands, and other configuration details for the build environment.

**What are the automated CodeDeploy monitoring tools?**
CloudWatch alarms
CloudTrail logs
CloudWatch events

**What are the valid actions in CodePipeline? Select two.**
Build
Approval
[reference](Read more here [https://docs.aws.amazon.com/codepipeline/latest/userguide/actions.html](https://docs.aws.amazon.com/codepipeline/latest/userguide/actions.html))


**Instructions for CodeBuild are stored in**
buildspec.yml

**The build environment for CodeBuild can be**
a Docker Image or CodeBuild managed 

**Assume you are using an EC2 instance as the target environment for CodeDeploy. What is the expected outcome if you configure CodeDeploy and push a deployment right after typing the following commands into the instance terminal?**  
  
**_wget https://bucket-name.s3.region-identifier.amazonaws.com/latest/install_****

**_chmod +x ./install_**

**_sudo ./install auto_**

CodeDeploy will not be able to connect to the EC2 instance
Explanation: In the above case, the CodeDeploy agent has not been started as a service before configuring the CodeDeploy service.

**Assume you are using CodeBuild to create a Docker image and push it into ECR. Which of the following will be part of the post-build stage in buildspec.yml?**
Upload the image to ECR
Explanation:The post-build phase is meant for actions to be performed on the generated build artifacts. In this case, the artifact is the Docker image and the action to be performed is the push to ECR. Please refer to the following link to know more: https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ecs-cd-pipeline.html


**Under which of the following circumstances would a Git push command from an Ubuntu EC2 instance to CodeCommit fail?**
The instance does not have the relevant IAM permissions