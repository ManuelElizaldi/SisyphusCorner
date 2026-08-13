[[Lambda Functions]]

The goal The following are the goals of this hands-on: 
1. Create the lambda function and deploy the python code 
2. Create a security group 
3. Create an instance of TG 
4. Create the ALB 
5. Access the ALB DNS in a browser tab

## Creating Lambda Function
We select *Author from scratch* - running on python

We also selected the *execution role* -> LabRole 
- #note I am assuming this role was created for my educational account

I opened the Lambda Function lab on my Vscode with the AWS extension

this is the python code used for the TIO:
#note there is some html inside the code which obsidian is rendering and is not being displayed:
```
def lambda_handler(event, context): response = { "statusCode": 200, "statusDescription": "200 OK", "isBase64Encoded": False, "headers": { "Content-Type": "text/html; charset=utf-8" } } response['body'] = """ 

Hello from Lambda!

""" return response
```

we pasted this code in the *code source* section but you can also upload files or select one from S3

inside the lambda function, I clicked on test and performed a small test:
![[Pasted image 20250805183344.png]]

To perform a test you only need to name your event and click on test

After testing I deployed the function from the Code Source Deploy button

## Creating security group
We create a security group that has inbound rules to allow HTTP on port 80 from anywhere 

## Creating a Target Group
The target is a lambda function -> in the next page you select which lambda function

Healthy threshold -> 2 

Then we create the Target Group

## Creating an Application Load Balancer 
Important to note here: we selected all AZs

Selected the *Security Group* we created earlier to allow HTTP communication

In *Listener and Routing* we selected the *Target Group* *lambda target group* we created as well 

## Result
![[Pasted image 20250805190418.png]]

When we open the Load Balancer DNS we get the above result, the web page is the python code we inserted into the lambda function

## Conclusion
Lambda function + HTML → Target group → Application Load Balancer (ALB) → Browser

### Event Architecture:

When you open the **DNS name of the ALB** in your browser:

1. Your browser sends an **HTTP request** to the ALB.
    
2. The **ALB** is configured with a **target group of type "Lambda"**.
    
3. The ALB **forwards the request** to the Lambda function.
    
4. The Lambda function receives the **HTTP request event** and returns an **HTTP response** — e.g., with HTML content.
    
5. The ALB passes the response **back to the browser**.

The **event** is an **HTTP request from ALB to Lambda**
- The trigger is **automatically fired** when the ALB receives a browser request.

