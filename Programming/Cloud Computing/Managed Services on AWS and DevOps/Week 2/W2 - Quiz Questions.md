**What are the typical business benefits of serverless computing assuming it is being used for the correct use case?**
Quickly validate new ideas
Lower cost
Adapt at scale

**What are the main advantages of packaging all the dependencies in an aws lambda function? Select two.**
Simplified deployment: allows for a simpler deployment process. You can deploy the whole package as one single unit, rather than having to deploy each dependency separately.
  
Reduced dependencies: reduces the number of external dependencies you need to manage. This makes it easier to keep track of all the components and ensures that everything is correctly versioned.

**What are the programming languages supported by Lambda?**
Go, python, java, C#

**You have an application that allows the customer to submit insurance claim details. The scope is not processing the claim, just submission of the First Notice Of Loss (FNOL), where the claimant provides the information to the insurer. Assume Lambda powers your backend. Which invocation style will you prefer in this case?**

**Hint: after submitting a claim, should the application provide a confirmation?**
Synchronous
Reason - The application needs to respond to the customer immediately that the claim has been submitted (or not in case of an error).

**You can run JavaScript code with Node.js in AWS Lambda. Lambda provides runtimes for Node.js that run your code to process events. Your code runs in an environment that includes the AWS SDK for JavaScript, with credentials from an AWS Identity and Access Management (IAM) role that you manage.**
True


**S3 events invoke a lambda synchronously.**
False
Several AWS services, such as Amazon Simple Storage Service (Amazon S3) invoke functions asynchronously to process events. When you invoke a function asynchronously, you don't wait for a response from the function. You hand off the event to Lambda and Lambda handles the rest. You can configure how Lambda handles errors.


**You have an application where customers can occasionally upload files that need processing. Such files will be uploaded to cloud storage as a service. The application designer has created an approach where a program wakes every 60 mins to check for new files. Will you agree with this approach?**
No, this is a great case for event based processing approach rather than constant polling at regular intervals.


**Which use cases are a great fit for Lambda?**
web backend, mobile backend, IoT backend etc.


**An application needs a significant amount of memory and time to process some customer data. Your technical lead proposes using an EC2 instance instead of a Lambda function. Will you agree with this approach?**
Yes
AWS Lambda has memory and execution time limits. Long-running or memory-intensive tasks exceed these thresholds, making Lambda inefficient or unusable for such use cases.


**How can you set a Lambda function to run periodically?**
Set up a cloudwatch or event bridge event as the trigger for the lambda function
- alarms can be set up with cloud watch that can trigger a lambda
- event bridge - event bus. Helps build event driven architecture service. Uses events to connect services. Offers event archive  
With these two managed services you can build a cron like lambda function

**A system to catch speeding vehicles uses a camera to take pictures of license plates after a Doppler radar has been triggered. The system needs to store a list of past offenders and pictures of their license plates and has to be able to query if an offender has a history. All this is orchestrated by a Lambda function. Which of the following services would the function need access?**
rekognition, S3 and dynamo db

rekognition -> Used to analyze images

Amazon S3 -> This can be used to store the images of the cars
- cost effective, durable and scalable object storage

DynamoDB -> NoSQL serverless database that can store offender records | pairs well with the lambda serverless architecture

❌ RDS -> This could work, but it is not as fast as DynamoDB. Also RDS requires a server 

❌ comprehend -> is used for natural language processing 

❌ EFS -> can be mounted by lambda, but it's unnecessary, DynamoDB is more efficient for this use case

**Which of the following services allows a Lambda function to receive requests from an "external" source?**
api gateway, application load balancer

For this use case, we need a service that invokes the lambda function in response to an HTTP request (outside internet)

API Gateways are designed to expose lambda functions over HTTPS endpoints - ideal for serverless APIs 

Application load balancer -> You can include lambda functions as a target of the load balancer 