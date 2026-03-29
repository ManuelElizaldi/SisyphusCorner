![[Pasted image 20260329102735.png]]

Step function + lambda function 

## Step Functions
Visual Workflow orchestrator - lets you coordinate a group of AWS resources into a series of steps. It offers error handling, retry and branching logic. 


Serverless function orchestrator that makes it easy to sequence AWS Lambda functions and multiple AWS services into business critical applications. 

The output of a step function acts as the input to the next.

#### Without Step Functions, your code looks like:
```
Your code manually calls:
Lambda A → wait → check result → Lambda B → wait → 
check result → handle errors → retry logic → Lambda C
```
Coding all of this yourself can be messy and error prone. Also, very manual work. 

#### With Step Functions
```
You define a workflow visually:
Step 1 → Step 2 → Step 3
         ↓ (if error)
         Retry or go to Step 4
```
Step functions handles all of the retry logic, waiting, etc. for you. 


## State Machine



