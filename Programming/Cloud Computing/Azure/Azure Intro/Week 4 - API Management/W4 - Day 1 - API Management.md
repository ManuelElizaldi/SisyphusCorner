[[API]]
# Azure API Management - Build & Deploy APIs

securing, monitoring and managing APIs for your application/organization


API -> deployed on VM

API Gateway for back end services 

Publish APIs to external developers or customers

developer = customer = consumer of API

you can monitor APIs

You can make them rest compliant 
### Rest Compliant
Make an API rest compliant means to design it according to the principles of [[REST]] - representational state transfer - an architectural style designed for networking applications - primarily web servers 


Modify the requests and responses 

Define policies of APIs and throttling 
- Make API compliant before exposing it to consumers

Build Mock APIs and export them as product 

## Use Cases
Expose legacy API in compliance with organization standards 

Control API access and monetize assets

provide consistent interface to customers 

## Two Sides of API Management 
### Administrative
Define or import API, define policies, bundle API products, etc.

### Consumer
Subscribe to products, check API documentation, test APIs, check analytics

# API Management Components 
## Set up of API management
In resources you will find API Management Services -> you choose the region where you want it deployed

you have to provide a unique name because it is used in a GatewayURL and in the developer portal

You can have one centralized API management for all of your organization's APIs 

*pricing tier* -> premium has a SLA of 99.95 to 99.99, developer which is same as premium but with no SLA and there's also a consumption tier that you pay per request and has no developer portal with SLA of 99.95

You can track with *Application Insights*

Scaling, networking and identity can be configured 

protocol settings allows you to choose different algorithms for cipher and protocols for front side and back end

## APIs and Operations
In the left hand side inside the console there's a section for API and you can create APIs here from scratch. 
- you can also create from a azure resource 
- you can import from on prem as well with API definitions - WADL, WSDL and OpenAPI files

*collection of methods* -> operations

*operation* -> method, for example, cancel flight, book flight, etc. 

Create blank API, give it name and a suffix for the url -> 

### Mock APIs
Dummy API that can be used to test an operation 
![[Pasted image 20251021170141.png]]

*Function Definition* -> interface agreed on by both the Webb App team and the Flight Booking APIs

## Setting up an API & a Mock
![[Pasted image 20251021170545.png]]

inbound and outbound is where you can modify the request and response 

In the backend you can determine the actual location of the backend

### Mocking
There is a policy inside the inbound processing where you create a mock response, this means that the request wont go to the backend but still mock a response. 
- Once the back end is ready you can remove the Mock policy

You can also set up a mock json response 
#### Testing
For testing you go to Test in the same portal, here you can define parameters and headers if needed. Here you can also see the request URL

### Inbound Policy 
Filter to IPs, mock reponses, set headers

*headers* -> extra pieces of information sent with the request or response in an API, they provide metadata about the request but are not the main content 

there is another option for 'Other Policies' -> this gives you the code (XML) so that you can define your own policies. In this XML you can also view all the policies you have set. There is an order to the XML depending on what you want to evaluate first 
- <base/> determines that all global policies will apply. Depending on where you place this, it determines the order what policies it will evaluate first  

*Inbound Processing Limit Calls* -> You set the limit of calls per a renewal period. You also have a counter key, meaning the way you are going to count the call, by IP, by subscription or a custom one 

Inbound policies:
![[Pasted image 20251021220635.png]]

There is a hierarchy to the policies, in this example the rate limit by key is grayed out because it needs to be above. As stated above, the order is important. 

## Creating an API based of a Azure Function
Get method function that grabs a list of To Dos 

From the APIs console, import a Function and you can browse the functions you currently have. 

Same set up, you get a URL for the API url

Inside the Frontend properties you can change the URL 

> [!NOTE] Set - Backend - Service
> You need this policy in order to send the request to the backend server

### Modifying outbound policies
In the video the professor added a header in the code, so the header was displayed in the response json. Then he went inside the outbound policies to remove this header. He also added an override action 
- he deleted a header and overwrote it with another one 


# Summary of API Management
API gate way -> handles APIs, you can control any aspect of the response and request. The menu with the 4 boxes.
- Here you can also determine the policies
- Accepts API calls and diverts them to backends 
- verifies requests
- logs incoming requests

API = operation = method that can be invoked

APIs are a set of operations 

API maps to a backend service

Operation maps to methods implemented by back-end services

Policies -> set of statements which are executed on the request or response. Work in sequential order, these modify the behavior of the operation. 


## Operation, Methods and APIs

APIs is the overall collection of endpoints that a service exposes. 
- The whole menu of things you can do 

Operations is the specific action or task you can perform with an API 

Method is the http method used to perform the action
- get 
- post
- put
- delete
