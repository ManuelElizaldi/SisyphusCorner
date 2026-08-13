**How can you set a Lambda function to run periodically? Lambda should not be used for cron jobs Set up a cloudwatch or event bridge event as the trigger for the lambda function set up an application in elastic bean stalk to trigger the lambda function set up a local cron script to send a request to the function**
Set up a CloudWatch or EventBridge event as the trigger for the Lambda function

To run a Lambda function on a **schedule (like a cron job)**, you should use: **Amazon EventBridge**

- It supports cron expressions and rate-based expressions
- You define a **rule** that triggers the Lambda function periodically 


---

### Why not the others?

- ❌ **"Lambda should not be used for cron jobs"**  
    → Incorrect. **Lambda _can_ be used for cron jobs** when triggered by EventBridge.
    
- ❌ **"Set up an application in Elastic Beanstalk to trigger the Lambda function"**  
    → Overkill and unnecessary for a simple scheduled task.
    
- ❌ **"Set up a local cron script to send a request to the function"**  
    → Not reliable or scalable. Also defeats the purpose of serverless architecture.
    

---

Let me know if you want an example cron expression or how to set it up in the AWS console or with Terraform/CDK.

##### You said:

A system to catch speeding vehicles uses a camera to take pictures of license plates after a Doppler radar has been triggered. The system needs to store a list of past offenders and pictures of their license plates and has to be able to query if an offender has a history. All this is orchestrated by a Lambda function. Which of the following services would the function need access? RDS, rekognition, s3 Comprehendm, EBS and S3 rekognition, S3 and dynamo db rekognition, S3 and EFS

###### ChatGPT said:

The **correct answer** is:

> ✅ **Rekognition, S3, and DynamoDB**

---

### Here's why:

#### ✅ **Amazon Rekognition**

- Used to **analyze images**, such as **extracting license plate numbers** from the photos taken by the camera.
    

#### ✅ **Amazon S3 (Simple Storage Service)**

- Ideal for **storing the images** of the license plates.
    
- Cost-effective, durable, and scalable object storage.
    

#### ✅ **Amazon DynamoDB**

- NoSQL database that's well-suited for **storing and quickly querying** offender records.
    
- Allows querying if a vehicle has a history of offenses.
    

---

### Why the others are incorrect:

- ❌ **RDS, Rekognition, S3**
    
    - RDS (Relational Database Service) could work, but DynamoDB is a **better fit for fast, scalable lookups** in a serverless environment like Lambda.
        
- ❌ **Comprehend, EBS, S3**
    
    - Comprehend is for **natural language processing**, not image analysis.
        
    - EBS (Elastic Block Store) is not used with Lambda functions.
        
- ❌ **Rekognition, S3, and EFS**
    
    - EFS (Elastic File System) can be mounted by Lambda, but it’s unnecessary here.
        
    - DynamoDB is more efficient for this use case than a filesystem.
        

---

Let me know if you want to sketch out the architecture or IAM permissions!

##### You said:

Which of the following services allows a Lambda function to receive requests from an "external" source? VPC, route 53 cloud front, s3 api gateway, application load balancer route 53, application load balancer

###### ChatGPT said:

The **correct answer** is:

> ✅ **API Gateway, Application Load Balancer**

---

### Explanation:

To allow a **Lambda function to receive requests from an external source (e.g., the public internet)**, you need a service that can **invoke** the Lambda function **in response to HTTP requests**.

#### ✅ **API Gateway**

- Specifically designed to expose **Lambda functions over HTTPS endpoints**.
    
- Ideal for **serverless APIs**.
    
- You can define RESTful or HTTP APIs with authentication, throttling, etc.
    

#### ✅ **Application Load Balancer (ALB)**

- Can **trigger Lambda functions** directly as of recent AWS updates.
    
- Useful if you're already using an ALB and want to include Lambda targets in the architecture.
    

---

### Why the others are incorrect:

- ❌ **VPC, Route 53**
    
    - **VPC** is a networking service, not for receiving external HTTP requests.
        
    - **Route 53** is a **DNS service**, which just maps domain names to IPs—it doesn't directly route to Lambda.
        
- ❌ **CloudFront, S3**
    
    - CloudFront is a **CDN**, and S3 is for **object storage**.
        
    - Neither can **directly invoke Lambda** from external HTTP requests without another service like API Gateway in the path.
        
- ❌ **Route 53, Application Load Balancer**
    
    - Route 53 still just handles DNS.
        
    - ALB alone can trigger Lambda, but without a domain mapping or DNS, it’s incomplete.
        

---

So:

> **API Gateway** (best for APIs) and **Application Load Balancer** (possible with some setup) both allow Lambda to receive external HTTP requests.