[[S3]] [[DevOps]]
# Biz Process S3 
Starting from here:
![[Pasted image 20250731191102.png]]

based on what we saw in [[W2 - Day 1, 2 & 3 - Serverless Computing Step Functions, Lambda Functions, Invocation Types]]

Inside the video, the professor created a JS code that grabs the response json that results from the execution of the lambda function. From here he parses it and grabs the id of the file and path that he then uses to send on an email via SES API

The destination of this email is also added to the JS function 

The email is inside the lambda function but also needs to be inside the SES

Lambda has a log managers, but its easier to look at it through CloudWatch

The lambda function will also require permissions to send emails through SES - this is performed through IAM 

lambda functions can use S3 APIs to read files and create an email based on this 

lambda functions as extremely flexible and are capable of many things 

# New Lambda UI - Lambda Containers
inside the lambda functions you can create the container images. In the Lambda aspect, this is deploying a small unit of work - function - inside a container. 

You can deploy all dependencies inside this container 

*Execution Environment* - lambda instance

*Multiple Execution environment* - everything that is executing inside your account

![[Pasted image 20250802202818.png]]


## X Ray


Data Base Proxy 


EFS + lambda

State machine 