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