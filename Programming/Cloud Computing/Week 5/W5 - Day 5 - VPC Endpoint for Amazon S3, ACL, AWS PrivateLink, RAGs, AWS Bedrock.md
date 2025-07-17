[[Network]] [[AI]] [[RAG]]
## End points
VPC can connect to a S3 storage through endpoints

## Network Access Control List ACL
allows or denies inbound and outbound traffic at a subnet level.

# AWS Global Accelerator 
You are given a default pool of IPs, but you can also bring your own IPs (BYOIP). 
- IPs are entry points for clients 

**Global Accelerator improves the performance of you application by distributing traffic.**

The Global Accelerator will find the closest region for your client and send him there. Once it's inside the region (VPC), the pertinent AWS services handle the user. 

The Global Accelerator operates in a multi-region plane and it *routes IPs. 

As mentioned above, there are a list/group of static IPs (or your own defined IPs) and users connect to that. Their traffic then enters the AWS net and they are sent to your healthiest or defined route (via policy) to the best performing application (EC2, ALB, S3, etc.)

### Global Accelerator vs Network Load Balancing
They operate at a different level:
- one is multi regional -> Global Accelerator
- the other one is regional (VPC level), only operates at one region.

Global Accelerator *handles IPs* and the NLB *handles data packets (UDP and TCP protocols)*. 

Their traffic *entry points* are also different. Global Accelerator -> Closest AWS edge location to user 
- NLB inside your VPC's services 

#### They work together like this:
Global Accelerator brings users to their closest AWS region, once inside the region the NLB sends users to their corresponding EC2 instance. 


#### Practice quiz question: To block traffic from a particular IP, use?
NACL - Network Access Control List


# Secure and Accelerate Generative AI Deployment with Private Network Connectivity in AWS

part of a PDF read [here](https://d6opu47qoi4ee.cloudfront.net/genAI/ccaws/private-network/private-network.pdf)

--- 

Security is important to prevent personal identifiable information (PII) leakage. Reduce vulnerabilities and use private IPs.

**AWS PrivateLink** used for secure networking in generative AI. Enables secure access to AWS services and third party SaaS services through private connections. You don't expose information to the internet. 

### Generative AI 
Models move a lot of data during their different stages:
- *Training* -> learning phase

- *Fine-Tuning* -> specialization phase. You give it a smaller data set specific for the task

- *Inferencing* -> usage phase. The model is deployed and ready to use

### AWS VPC EndPoints and AWS PrivateLink
There's two types of EndPoints 1) Interface and 2)Gateway. 

1) Interface -> network interface in your subnet, privately access services. **This is how you use PrivateLink**
2) Gateway -> Adds a route to your route table and is only used for S3 and DynamoDB

PrivateLink is the underlying technology 

##### Analogy 
There's two building which need to be connected by a secure underground tunnel. The buildings are VPCs and the tunnel is the PrivateLink 

> [!NOTE]
>  Interface Endpoints are built on top of the PrivateLink technology 

This set up is done through secure private IPs


### Secure Generative AI Pipeline Using AWS PrivateLink
VPC must be private - **no Internet Gateway**

Use private IPs

Deploy PrivateLink to allow secure transfer of data within your VPC

## RAG (Retrieval Augmented Generation) Based Generative AI 
Retrieval + Generation

A generative AI model has a knowledge base - the information it was trained on. RAG based allows for retrieval of additional information. This can be obtained from a database, document store, vector index. 

> [!NOTE]
> Vector databases make search faster 

### Tools of a RAG system
- Retriever -> Where is your information, for example -> vector database
	- Goes out and looks for information

- Embedder -> Converts text into embeddings
	- Tool that converts text (or other data) into vectors of numbers that represent the meaning of the input
	- Translates info into numbers used by the computer
	
- LLM -> GPT
	- Writer - takes all the input and writes down the response to the prompt 
- Orchestration -> LangChain, LlamaIndex
	- This tool/element of a RAG system is what glues everything together. 

##### In simple terms
Google search + ChatGPT 

##### Benefits
Reduces hallucination
up to date information - provided by retrieving up to date databases 
access to external knowledge 
shows sources 
more precise 

### RAG in AWS 
If you want to deploy a RAG system/model, you can allow the retrieval of proprietary data to improve inferencing accuracy. The model will use you database and other services that contain information to have a more accurate response to the prompt - less hallucination. 

## Architecture for secure RAG Implementation 

### Key Components
#### 1) Vector Data Stores
As mentioned above, RAG models require vector embeddings stored in a vector database. AWS offers services that allow you to store a vector embeddings *Vector Data Stores*:

- Amazon OpenSeach
- Redshift
- Aurora Serverless
- MongoDb, datastax, snowflake <- Third party options which can be securely connected to via PrivateLink (endpoints)

You can also connect to on prem infrastructure if you are self hosting your vector store. 
#### 2) Foundation Models
Large pre trained models on massive broad datasets. These can be accessed through:
##### Amazon Bedrock
Allows you to connect via API to AI models without needing to handle infrastructure. So you can build generative AI applications using pre-trained models. 

Bedrock and also securely connect/integrate to vector data stores and enhance responses. 

Also through *SageMaker* or other third party model providers

## Traffic Flow Breakdown
After all the security and policy measures have been established, IAM, IPs, endpoints NACLs, etc. 

1. Client to Application Flow:
	- Client sends query 
	- Request routed through VPC interface endpoint 
	- Connects to application via PrivateLink

2. Application to Service Flow
	- Application retrieves data from vector stores
	- Fetches model inference from Foundation Models
	- Communicates through private secure networks 

### Provider Requirements to Deploy a AI SaaS
![[Pasted image 20250712180344.png]]

This is a rough drawing of the requirements to offer a AI SaaS. You need to create **Interface EndPoints** within your VPC to connect the Vector Data Store to your VPC and another EndPoint for the Foundation Model, in this drawing ChatGPT. You establish the necessary policies and security measures to ensure a private and secure connection. 

Then you create a PrivateLink EndPoint with a DNS that is shared to your clients. You can do private DNS so that only a certain groups of IPs can access this DNS 

##### Simple Analogy of the RAG model happening in AWS
Imagine a librarian (vector database) helping a researcher (AI application) find perfect reference materials before an expert (AI model) crafts a comprehensive answer - all happening in a private, secure research facility. Key Point: Every step is private, controlled, and secure - no public internet involved!

### Architecture Diagram - Private connectivity between the client and the generative AI SaaS provider
![[Pasted image 20250712181747.png]]

### Architecture Diagram - Secure RAG through Knowledge Bases for Amazon Bedrock
![[Pasted image 20250714182213.png]]