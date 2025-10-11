[[Azure Functions]] [[Functions]]

# Functions
Runs on serverless environment because you don't need a dedicated infrastructure. You can write a small piece of code and run it.

Multiple language support 

You can run containers inside Azure Functions

True infrastructure scaling 
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


# Creating a Function
*Function App* When creating a function app, it will ask you to choose a code or a container 

it asks you for what *run time* you want to use, version and in which region it will be executed
- The function app will be configured to run apps for this run time, so it will only support that language 

**You also always need a storage account to keep files produced by the function or config files needed to run the function**

OS -> windows or linux

*Hosting option*:
- consumption (serverless)

*Application insights* -> monitoring 

**You can create multiple functions inside the function app

## Template 



### Payment
you pay for each execution - there is an option to limit these

There's an option to enable only HTTPS

### Development portal
You can choose the IDE to develop your code
- vs code
- in portal, etc. 

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

*Function Code*

*Output Binding* -> Write the data to a sink without writing much code 





