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
A defined set of steps. A state machine can be:
![[Pasted image 20260329160256.png]]

## AWS Resources Interaction with Step Functions
Step functions can interact with most AWS resources:

✅ Lambda functions
✅ ECS/Fargate tasks
✅ DynamoDB (read/write)
✅ S3 (get/put)
✅ SNS/SQS (publish/send)
✅ Glue jobs (ETL)
✅ Athena queries
✅ SageMaker training jobs
✅ API Gateway calls
✅ Human approval tasks (wait for someone to click approve)
## Step Functions vs Lambda 
Lambda functions have a time limit, they are suited for short lived processes. Here's where Step Functions can come into play. 

Also, nesting/chaining lambda functions can be hard to debug. If Lambda function A fails, Lambda function C wont know in a clean manner. 

![[Pasted image 20260329160605.png]]

### Tip
Step functions are a recipe for the cloud, it tells you exact steps. Each step is an instruction and it also tells you what to do when something goes wrong

# Lab
## Creating a lambda function
We create a lambda function and author by scratch with run time python 3.10 

For this lab, there was an execution role already set, with this specifications:

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": [
				"logs:CreateLogStream",
				"logs:CreateLogGroup",
				"logs:PutLogEvents"
			],
			"Resource": [
				"*"
			]
		}
	]
}
```

After creation we have this diagram:
![[Pasted image 20260329162522.png]]

We added the following python code:
```python
import json

def lambda_handler(event, context):

# TODO: Implement your Lambda function logic here

return {

'statusCode': 200,

'body': json.dumps('You have successfully invoked the lambda function from Step Function.')

}
```

And then we click on deploy

**Deploy a Lambda Function** -> You are uploading your code to AWS so that it can be executed on demand. 

And we copy the ARN of the lambda function -> `arn:aws:lambda:us-east-1:194160272763:function:MyStepFunction_lambda`

## Creating a Step Function
We open the management console for Step Functions and click on State Machine (workflow definition).

We create a Step Machine - from blank and standard. 

This is what the State Machine console looks like: 
![[Pasted image 20260329163005.png]]

In the above visualization we click on code and paste the following Json:

```json
{

"Comment": "Sample State machine code to invoke a lambda function",

"StartAt": "invokeLambda",

"States": {

"invokeLambda": {

"Type": "Task",

"Resource": "<YOUR_FUNCTION_ARN>",

"End": true

}

}

}
```

Pasting the ARN from the lambda on the Resource field. 

**What is ARN** -> Amazon Resource Name, essentially an ID for resources. Globally unique for each resource you create.  

The graph now looks like this: 
![[Pasted image 20260329163240.png]]


Then we go into the config menu -> set the corresponding permissions (which were already created for this lab) -> and we finally create. 


## Testing the State Machine / Step Function 
Inside the State Machine dashboard you can click on Actions and click `Start Execution`

#### Successful Execution:
![[Pasted image 20260329163649.png]]

If you click on the InvokeLambda function you can see the details of the function on the Step Details window to the right. 

