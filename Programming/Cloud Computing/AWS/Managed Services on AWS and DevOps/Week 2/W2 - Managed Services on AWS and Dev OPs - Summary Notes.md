# Introduction

AWS Lambda is a serverless, event-driven compute service that lets you run code for virtually any type of application or backend service without provisioning or managing servers. You can trigger Lambda from over 200 AWS services and software as a service (SaaS) applications, and only pay for what you use.

  

**Lambda concepts**

- A **function** is a resource that you can invoke to run your code in Lambda. A function has code to process the events that you pass into the function or that other AWS services send to the function.
    
- A **trigger** is a resource or configuration that invokes a Lambda function.
    
    - Triggers include AWS services that you can configure to invoke a function and event source mappings.
        
    - An **event source mapping** is a resource in Lambda that reads items from a stream or queue and invokes a function.
        
- An **event** is a JSON-formatted document that contains data for a Lambda function to process.
    
    - The runtime converts the event to an object and passes it to your function code. When you invoke a function, you determine the structure and contents of the event.
        
- An **execution environment** provides a secure and isolated runtime environment for your Lambda function.
    
    - An execution environment manages the processes and resources that are required to run the function.
        
    - The execution environment provides lifecycle support for the function and for any extensions associated with your function.
        
- The **instruction set architecture** determines the type of computer processor that Lambda uses to run the function. Lambda provides a choice of instruction set architectures:
    
    - arm64 – 64-bit ARM architecture, for the AWS Graviton2 processor.
        
    - x86_64 – 64-bit x86 architecture, for x86-based processors.
        
- A **Lambda layer** is a .zip file archive that can contain additional code or other content. A layer can contain libraries, a custom runtime, data, or configuration files.
    
- **Extension**
    
    - Lambda extensions enable you to augment your functions.
        
- **Concurrency** is the number of requests that your function is serving at any given time. When your function is invoked, Lambda provisions an instance of it to process the event. When the function code finishes running, it can handle another request. If the function is invoked again while a request is still being processed, another instance is provisioned, increasing the function's concurrency.
    
- **Qualifier**
    
    - When you invoke or view a function, you can include a qualifier to specify a version or alias.
        
    - A version is an immutable snapshot of a function's code and configuration that has a numerical qualifier.
        

  

You can use Lambda functions to build services that give new skills to Alexa, the Voice assistant on Amazon Echo.

- The Alexa Skills Kit provides the APIs, tools, and documentation to create these new skills, powered by your own services running as Lambda functions.
    
- Amazon Echo users can access these new skills by asking Alexa questions or making requests.
    

# Features

The following key features help you develop Lambda applications that are scalable, secure, and easily extensible:

- **Concurrency and scaling controls**
    
    - Concurrency and scaling controls such as concurrency limits and provisioned concurrency give you fine-grained control over the scaling and responsiveness of your production applications.
        

![[Pasted image 20250804205015.png]]

![[Pasted image 20250804205021.png]]

![[Pasted image 20250804205029.png]]

- **Functions defined as container images**
    
    - Use your preferred container image tooling, workflows, and dependencies to build, test, and deploy your Lambda functions.
        
- **Code signing**
    
    - Code signing for Lambda provides trust and integrity controls that let you verify that only unaltered code that approved developers have published is deployed in your Lambda functions.
        
- **Lambda extensions**
    
    - You can use Lambda extensions to augment your Lambda functions. For example, use extensions to more easily integrate Lambda with your favorite tools for monitoring, observability, security, and governance.
        
- **Function blueprints**
    
    - A function blueprint provides sample code that shows how to use Lambda with other AWS services or third-party applications. Blueprints include sample code and function configuration presets for Node.js and Python runtimes.
        
- **Database access**
    
    - A database proxy manages a pool of database connections and relays queries from a function. This enables a function to reach high concurrency levels without exhausting database connections.
        
- **File systems access**
    
    - You can configure a function to mount an Amazon Elastic File System (Amazon EFS) file system to a local directory. With Amazon EFS, your function code can access and modify shared resources safely and at high concurrency.
        
- **Deployment package**
    
    - You deploy your Lambda function code using a deployment package.
        

Lambda supports two types of deployment packages:

- A .zip file archive that contains your function code and its dependencies. Lambda provides the operating system and runtime for your function.
    
- A container image that is compatible with the Open Container Initiative (OCI) specification. You add your function code and dependencies to the image. You must also include the operating system and a Lambda runtime.
    

- **Runtime**
    
    - The runtime provides a language-specific environment that runs in an execution environment.
        
    - The runtime relays invocation events, context information, and responses between Lambda and the function. You can use runtimes that Lambda provides, or build your own. If you package your code as a .zip file archive, you must configure your function to use a runtime that matches your programming language.
        
- **Asynchronous Invocation**
    

![[Pasted image 20250804205039.png]]

- When you invoke a function, you can choose to invoke it synchronously or asynchronously.
    
- With synchronous invocation, you wait for the function to process the event and return a response.
    
- With asynchronous invocation, Lambda queues the event for processing and returns a response immediately.
    

  

- **Event source mappings**
    
    - To process items from a stream or queue, you can create an event source mapping.
        
    - An event source mapping is a resource in Lambda that reads items from an Amazon Simple Queue Service (Amazon SQS) queue, an Amazon Kinesis stream, or an Amazon DynamoDB stream, and sends the items to your function in batches.
        
    - Each event that your function processes can contain hundreds or thousands of items.
        

![[Pasted image 20250804205046.png]]

  

- **Destinations**
    
    - A destination is an AWS resource that receives invocation records for a function. For asynchronous invocation, you can configure Lambda to send invocation records to a queue, topic, function, or event bus.
        

![[Pasted image 20250804205053.png]]