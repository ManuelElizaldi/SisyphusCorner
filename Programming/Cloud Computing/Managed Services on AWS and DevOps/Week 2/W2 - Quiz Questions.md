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
