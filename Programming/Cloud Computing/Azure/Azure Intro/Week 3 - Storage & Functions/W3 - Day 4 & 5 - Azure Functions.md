[[Azure Functions]] [[Functions]]
# Functions
Runs on serverless environment because you don't need a dedicated infrastructure. You can write a small piece of code and run it.

Multiple language support 

You can run containers inside Azure Functions

True infrastructure scaling 

Each function has an authorization level based on what you want it to do. 
## App Services vs Azure Functions
App services can deploy web apps, APIs and mobile backends in Azure Functions you can only deploy APIs. 

App services does run on a dedicated infrastructure, so you need the subscription. Azure functions is serverless.

## Use Cases
Utility functions -> different projects can consume the same functions
- clean up of storage
- emails
- micro services

Build REST API inside Azure functions

Immediate execution once a file is placed in blob storage 

Automated hourly jobs 

Real time data from IoT devices

## Components of Azure Function
*Trigger* -> starts the function 
- HTTP trigger -> hit a URL and the function triggers 
- Timer trigger -> schedule 
- Blob Storage trigger -> If a file is placed inside the blob storage, the function is triggered 
- Service bus -> every time a message arrives
- IoT hub 

There are many triggers

*Action* -> What code are you running 

*Input Binding* 
- Without IB: you create code to connect to storage account, grab the file and then close the connection
- With IB: without writing much code, I can just provide the conn string & file I want to read. It will read the file and run it as a parameter 
	- Function code will only run when it has picked up the data and processed it 

*Function Code* -> The code that will be executed 

*Output Binding* -> Write the data to a sink without writing much code. You decide where the product/output of the function will be stored. Message, email, file, etc. 

# Creating a Function - PaaS
*Function App* When creating a function app, it will ask you to choose a code or a container 

it asks you for what *run time* you want to use, version and in which region it will be executed
- The function app will be configured to run apps for this run time, so it will only support that language 

**You also always need a storage account to keep files produced by the function or config files needed to run the function**

OS -> windows or linux

*Hosting option*:
- consumption (serverless)

*Application insights* -> monitoring 

**You can create multiple functions inside the function app

You choose where the input comes from and where to send the output 

Each function has a security level

### Editing a trigger
![[Pasted image 20251011140953.png]]

**trigger parameter name and  the name of the parameter in the code should match** 

*Route Template* -> parameters in the URL: /api/todo/{id}. Route template allows you to change the URL of the request. 

*Input binding* -> Read a file and use that as input. The function reads the file before executing. You have to choose the binding type: blob storage, cosmos DB, etc. Then you choose your storage account, this will produce a connection string stored in your function configurations
- You also have to give it the path to the file 
- You declare the name of the input name to be used inside the code 

*Output binding* -> Where do you want to store the data produced by the function. In the lesson video, the professor set up a queue to store the output there. 
- With this set up, there's two outputs, the HTTPS page and the queue message 

### Template 
You can use a template to create a function based on the trigger. 
### Payment
you pay for each execution - there is an option to limit these

There's an option to enable only HTTPS
### Development portal
You can choose the IDE to develop your code
- vs code
- in portal, etc. 

### Authorizations
*Anonymous* -> anybody can run | no security

*App Keys | Admin* -> key for admin. You can give this key to multiple admins and they can view, modify and run **all the functions**

*Function Key* -> At the function level. Only if you have this key you can run the function:
#### Function Key
Authorization level -> Key = only people with the function key can trigger the function 
- For a single function
![[Pasted image 20251011150358.png]]
The section 'code =' is where you insert the function key

## Scheduled Function | Timer Trigger | CRON expression
Timer Trigger 
CRON Expression syntax:
{second} {minute} {hour} {day} {month} {dayofweek}
- day of week starts in Monday = 1 

*example* -> 0 0 4 * * * = 4 am

0 {*/4} * * * = */4 every 4 minutes. The / means every x amount 

## Azure Blob Storage Trigger
You point the function to the path (container) of the blob and the file name will become a parameter in the function

as soon as a new file lands in the container, the function will trigger 
- *can you track a specific file?*

 
# Hosting Plans
When you create a function, you must choose how this is hosted. 

## App Service Plan
You create infrastructure (PaaS) VMs, use any existing app service plan instances

Function default timeout is 30 mins, but can be changed to unlimited

Scaling here takes a bit more time since you are creating a VM 

Runs continuously - you pay for the number of instances that are running 

## Consumption Plan
Serverless platform, no dedicated infrastructure. You just provide the code. 

You only pay for execution - if it's consuming 10 ACUs and 28 mb of memory, you pay for that 

if your function does not finish in 5 minutes it auto terminates, you can bump up this to 10 mins. 

There is a cold start to this plan -> code needs to be loaded into memory

small instance size 
## Premium Plan
Pre warmed workers with no delay in execution. It automatically scales depending on the demand and executes the functions.

code always remain in memory 

Function default timeout is 30 mins, but can be changed to unlimited

You can choose the instance size that you want and you pay for the number of instances 
### Comparison
All hosting plans auto scale

you pay for execution in consumption 
you pay for the number of instances in premium and app 
![[Pasted image 20251016181241.png]]

