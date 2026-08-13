[[Serverless Computing]] [[Lambda Functions]] [[Pricing]] [[Containers]] 

# General introduction & step functions basics
## Serverless Computing
Companies don't need to manage and maintain their own servers, they can focus on developing applications instead. Companies don't need to worry about hardware, software and infrastructure. 

You don't need to manage anything 

Serverless - a small unit of work = function

> [!NOTE] Application
>Application - in a bare bones definition is just modules and classes.

## Serverless and cloud computing 
Serverless computing uses *functions* as its main unit of computation. 

Instead of running an entire application on a server, functions are triggered by events such as an API call or a message from a queue ([[W1 - Day 2 - SQS, Pipeline, Deadletter, SQS + SNS]])

Server only runs when its needed and only for the time that is needed


## Serverless AWS offering = Lambda 
**Small unit of work**

Also known as Lambda functions
Units of work 

There are several ways of coding Lambda functions, inside AWS, pushing it through your code repo, CLI for bundling functions

CI/CD processes that can deploy into a lambda function

There are several ways of deploying these functions

## Lambda Function
Small, event driven programs that run in the cloud without needing to manage a server. They automatically execute in response to events like API calls, file uploads or messages. 

x happens y responds 

### Types of Lambda Invocation

*Synchronous* -> Request - wait - response. API Gateways, AWS SDK calls, Lambda calling another lambda

*Asynchronous* -> Fire and forget. SNS, S3 (file upload), EvenBridge, Step Functions, CloudWatch

### Examples of invokations




### Pricing model dimensions
Time it takes to execute your function, memory it consumes and data that it transmits and stores. 
- Managed by containers

## Step Functions
Orchestration of different lambda functions

State machine - transits from state A to B depending on the output of lambda execution

# Packaging a function & dependencies
## Deployment Package 
Before you run a lambda function you need to create your *deployment package*

as a .zip or .jar files with all your dependencies and necessary functions to run your application.

### Permissions
This is an important part of the deployment package. If your files only have -r permissions (read only) the lambda function will fail

you can follow the documentation in order to ensure the right permission settings

## Deployment Package - Python
2 scenarios 

simple - AWS SDK library (all managed services of AWS) if you only plan on using AWS specific services, you don't need to include anything because the runtime environment (container) will have everything for you to run 
- Same for other programming languages 
- You don't have to worry about dependency management in this scenario 

Advanced scenario - this scenario uses other external dependencies. In this case you need to create the Deployment Package .zip or .jar file, then use the CLI to deploy it or upload it to the S3 bucket and point the container to the location of the file 

There's instructions to create this deployment package in the documentation. You need to follow the steps indicated. But as a summary, you take all your app files, upload them, install any dependencies with pip in a created document and then you are set. From the [video](https://olympus.mygreatlearning.com/courses/132234/modules/items/7456664?pb_id=19113) it looks simple 



# Invocation Types - Synchronous and Asynchronous
synchronous and asynchronous invocation - you can control the invocation type only when you invoke a function 

on demand invocation:
- the application invokes the lambda function
- you manually invoke the function (using CLI) for testing purposes

But if you are using a AWS service as the event source, they have the invocation type predefined:
- for example S3 always invokes a lambda function asynchronously 

# Lambda Function Hands on Video

3 options -> 1) author from scratch, 2) blueprint and 3) serverless application repository 

Author Scratch: 

has a runtime -> what programming language is executing this 

Roles are important because without the right ones, the Lambda wont execute - there are templates for policy and roles 

After setting the name, roles and policy settings, the editing console will open

configuration *Designer* window, you can see the current triggers:
![[Pasted image 20250729213545.png]]


These are designed for short term business functions not large scale
- functions have a timeout of between 1 - 5 mins 

Containers happen within a VPC, so you can deploy them within your custom VPC 

Debugging and error handling can happen with [[SNS]] and [[SQS]]

*Throttle* -> stops concurrent calls - this helps avoid DNS attacks. 

There is a *auditing and compliance* setting that helps you track everything that was done with a 'forensic approach'.

# Console demo with JS function

Continuation of the above video

After you create a function you create a *Test Event* 
- Each service has a different payload, the *test event* gives you a template for each service 

AWS charges you by execution time - that's why we use the Test Events, to test without being charged 


your lambda function can create a log into CloudWatch 


## Lambda Function Executed by Trigger
You can create a trigger within the lambda function menu or you can create it within the service that will cause the trigger

S3 properties -> Advanced settings -> events -> you select send to Lambda function
- once you select the lambda function you can choose which function to execute 
![[Pasted image 20250730180449.png]]

After you associate the Lambda function you will see this in your lambda function menu on the left hand side - trigger 
![[Pasted image 20250730180706.png]]


## Test strategies
Triggering the function 'assuming' there was an event in S3 - not uploading a file, but testing as if we did.
- It pretends/recreates the trigger


# Lambda Function
Every lambda function has a trigger and destination 

``