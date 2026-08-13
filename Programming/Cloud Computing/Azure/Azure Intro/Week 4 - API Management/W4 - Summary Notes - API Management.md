**Microsoft Azure - 4**

  

**Azure API Management**

- Azure API Management is a hybrid, multi-cloud management platform for APIs across all environments.
    
- As a platform-as-a-service, API Management supports the complete API lifecycle.
    
- It provides a set of tools and services for creating, publishing, and managing APIs, as well as for enforcing security, scaling, and monitoring API usage.
    
- API management includes a range of features and tools, such as an API gateway, a web-based developer portal, API lifecycle management, monitoring and analytics tools, and security features.
    
- Azure API Management can be used with a variety of back-end services, such as Azure Functions, Azure Logic Apps, and Azure Virtual Machines, as well as with on-premises and third-party systems.
    
- It can help developers to build and manage APIs in a way that is secure, scalable, and easy to use
    
- Azure API Management helps customers meet these challenges:
    
    - Abstract backend architecture diversity and complexity from API consumers
        
    - Securely expose services hosted on and outside of Azure as APIs
        
    - Protect, accelerate, and observe APIs
        
    - Enable API discovery and consumption by internal and external users
        

  

**API Management components**

Azure API Management is made up of an API gateway, a management plane, and a developer portal. These components are Azure-hosted and fully managed by default. API Management is available in various tiers differing in capacity and features.

![](file:///tmp/lu1430504drlds.tmp/lu1430504drlhc_tmp_bccd4f5.png)

  

**API Gateway**

All requests from client applications first reach the API gateway, which then forwards them to respective backend services. The API gateway acts as a facade to the backend services, allowing API providers to abstract API implementations and evolve backend architecture without impacting API consumers. The gateway enables consistent configuration of routing, security, throttling, caching, and observability.

Specifically, the gateway:

- Acts as a facade to backend services by accepting API calls and routing them to appropriate backends
    
- Verifies API keys and other credentials such as JWT tokens and certificates presented with requests
    
- Enforces usage quotas and rate limits
    
- Optionally transforms requests and responses as specified in policy statements
    
- If configured, caches responses to improve response latency and minimize the load on backend services
    
- Emits logs, metrics, and traces for monitoring, reporting, and troubleshooting
    

  

**Management plane**

API providers interact with the service through the management plane, which provides full access to the API Management service capabilities.

Users can use the management plane to:

- Provision and configure API Management service settings
    
- Define or import API schemas from a wide range of sources, including OpenAPI specifications, Azure compute services, or WebSocket or GraphQL backends
    
- Package APIs into products
    
- Set up policies like quotas or transformations on the APIs
    
- Get insights from analytics
    
- Manage users
    

  

**Developer portal**

![](file:///tmp/lu1430504drlds.tmp/lu1430504drlhc_tmp_9af8889a.png)

  

- The open-source developer portal is an automatically generated, fully customizable website with the documentation of your APIs.
    
- API providers can customize the look and feel of the developer portal by adding custom content, customizing styles, and adding their branding. Extend the developer portal further by self-hosting.
    
- Using the developer portal, developers can:
    
    - Read API documentation
        
    - Call an API via the interactive console
        
    - Create an account and subscribe to get API keys
        
    - Access analytics on their own usage
        
    - Download API definitions
        
    - Manage API keys
        

  

**Terminologies**

**APIs-** APIs are the foundation of an API Management service instance. Each API represents a set of operations available to app developers. Each API contains a reference to the backend service that implements the API, and its operations map to backend operations.

  

**Products-** Products are how APIs are surfaced to developers. Products in API Management have one or more APIs, and can be open or protected. Protected products require a subscription key, while open products can be consumed freely.

  

**Groups-** Groups are used to manage the visibility of products to developers. API Management has the following built-in groups:

- **Administrators** - Manage API Management service instances and create the APIs, operations, and products that are used by developers.
    

Azure subscription administrators are members of this group.

- **Developers -** Authenticated developer portal users who build applications using your APIs. Developers are granted access to the developer portal and build applications that call the operations of an API.
    
- **Guests -** Unauthenticated developer portal users, such as prospective customers visiting the developer portal. They can be granted certain read-only access, such as the ability to view APIs but not call them.
    

  

**Policies-** With policies, an API publisher can change the behavior of an API through configuration. Policies are a collection of statements that are executed sequentially on the request or response of an API. Popular statements include format conversion from XML to JSON and call-rate limiting to restrict the number of incoming calls from a developer.

  

**Creating a new Azure API Management service instance**

- Subscription- The subscription under which this new service instance will be created.
    
- Resource group Select a new or existing resource group. A resource group is a logical container into which Azure resources are deployed and managed.
    
- Region- Select a geographic region near you from the available API Management service locations.
    
- Resource name- A unique name for your API Management service. The name can't be changed later. The service name refers to both the service and the corresponding Azure resource.
    

The service name is used to generate a default domain name: <name>.azure-api.net.

- Organization name- The name of your organization. This name is used in many places, including the title of the developer portal and the sender of notification emails.
    
- Administrator email- The email address to which all the notifications from API Management will be sent.
    
- Pricing tier- Select the Developer tier to evaluate the service. This tier isn't for production use.
    

  

**Creating an API**

By default, when you add an API, even if it's connected to some backend service, API Management won't expose any operations until you allow them. To allow an operation of your backend service, create an API Management operation that maps to the backend operation.

- **OpenAPI specification-**
    
    - Specifies the backend service implementing the API and the operations that the API supports.
        
    - The backend service URL appears later as the Web service URL on the API's Settings page.
        
    - After import, you can add, edit, rename, or delete operations in the specification.
        
- **Include query parameters in operation templates-** Specifies whether to import required query parameters in the specification as template parameters in API Management.
    
- **Display name-** After you enter the OpenAPI specification URL, API Management fills out this field based on the JSON.
    
- **Name-** After you enter the OpenAPI specification URL, API Management fills out this field based on the JSON.
    
- **Description**- After you enter the OpenAPI specification URL, API Management fills out this field based on the JSON.
    
- **URL scheme-** Which protocols can access the API.
    
- **API URL suffix-** The suffix appended to the base URL for the API Management service. API Management distinguishes APIs by their suffix, so the suffix must be unique for every API for a given publisher.
    
- **Tags-** Tags for organizing APIs for searching, grouping, or filtering.
    
- **Products-** Association of one or more APIs. Each API Management instance comes with two sample products: Starter and Unlimited. You publish an API by associating the API with a product.
    
- **Gateways-** API gateway(s) that expose the API. This field is available only in Developer and Premium tier services.
    
- **Version this API?-** Select or deselect
    

NOTE: To publish the API to API consumers, you must associate it with a product.

  

**Policies in Azure API Management**

- In Azure API Management, API publishers can change API behavior through configuration using policies. Policies are a collection of statements that are run sequentially on the request or response of an API.
    
- Popular statements include:
    
    - Format conversion from XML to JSON
        
    - Call rate limiting to restrict the number of incoming calls from a developer
        
    - Filtering requests that come from certain IP addresses
        
- Policies are applied inside the gateway between the API consumer and the managed API. While the gateway receives requests and forwards them, unaltered, to the underlying API, a policy can apply changes to both the inbound request and outbound response.
    
- Policy definitions are simple XML documents that describe a sequence of statements to apply to requests and responses.
    
- To help you configure policy definitions, the portal provides these options:
    
    - A guided, form-based editor to simplify configuring popular policies without coding XML
        
    - A code editor where you can insert XML snippets or edit XML directly
        
- The policy XML configuration is divided into inbound, backend, outbound, and on-error sections. This series of specified policy statements is executed in order for a request and a response.
    
- Example-
    

![](file:///tmp/lu1430504drlds.tmp/lu1430504drlhc_tmp_1636e19c.png)

  

Two Sides of API Management

1. Administrative
    

- Define or import API
    
- Define policies on request/response of an API
    
- Bundle API into products
    
- Manage users and subscriptions
    
- Monitor API usage
    

2. Consumer (developer)
    

- Subscribe to products
    
- Check API documentation
    
- Test API using the interactive console
    
- Check their own analytics
    

  

**Create and publish a product**

- In Azure API Management, a product contains one or more APIs, a usage quota, and the terms of use.
    
- After a product is published, developers can subscribe to the product and begin to use the product's APIs.
    
- Products are associations of one or more APIs. You can include many APIs and offer them to developers through the developer portal. During the product creation, you can add one or more existing APIs. You can also add APIs to the product later, either from the Products Settings page or while creating an API.
    
- **Display name-** The name as you want it to be shown in the developer portal.
    
- **Description-** Provide information about the product such as its purpose, the APIs it provides access to, and other details.
    
- **State-** Select Published if you want to publish the product. Before the APIs in a product can be called, the product must be published. By default, new products are unpublished and are visible only to the Administrators group.
    
- **Requires subscription-** Select if a user is required to subscribe to use the product (the product is protected) and a subscription key must be used to access the product's APIs. If a subscription isn't required (the product is open), a subscription key isn't required to access the product's APIs.
    
- **Requires approval-** Select if you want an administrator to review and accept or reject subscription attempts to this product. If not selected, subscription attempts are auto-approved.
    
- **Subscription count limit-** Optionally limit the count of multiple simultaneous subscriptions.
    
- **Legal terms-** You can include the terms of use for the product which subscribers must accept in order to use the product.
    
- **APIs-** Select one or more APIs. You can also add APIs after creating the product.
    
- If the product is open (doesn't require a subscription), you can only add an API that isn't associated with another open product.
    

NOTE: Use care when configuring a product that doesn't require a subscription. This configuration may be overly permissive and may make the product's APIs more vulnerable to certain API security threats.

  

- After you publish a product, developers can access the APIs. Depending on how the product is configured, they may need to subscribe to the product for access.
    
    - **Protected product -** Developers must first subscribe to a protected product to get access to the product's APIs. When they subscribe, they get a subscription key that can access any API in that product. If you created the API Management instance, you are an administrator already, so you are subscribed to every product by default.
        

When a client makes an API request with a valid product subscription key, API Management processes the request and permits access in the context of the product. Policies and access control rules configured for the product can be applied.

- **Open product -** Developers can access an open product's APIs without a subscription key. However, you can configure other mechanisms to secure client access to the APIs, including OAuth 2.0, client certificates, and restricting caller IP addresses.
    

NOTE: Open products aren't listed in the developer portal for developers to learn about or subscribe to. They're visible only to the Administrators group. You'll need to use another mechanism to inform developers about APIs that can be accessed without a subscription key.

- When a client makes an API request without a subscription key:
    
    - API Management checks whether the API is associated with an open product. An API can be associated with at most one open product.
        
    - If the open product exists, it then processes the request in the context of that open product. Policies and access control rules configured for the open product can be applied.
        

  

  

  

  

  

  

  

**Containers vs. virtual machines**

  

|   |   |   |
|---|---|---|
  
|**Features**|**Virtual Machines**|**Containers**|
|Isolation|Provides complete isolation from the host operating system and other VMs. This is useful when a strong security boundary is critical, such as hosting apps from competing companies on the same server or cluster.|Typically provides lightweight isolation from the host and other containers, but doesn't provide as strong a security boundary as a VM. (You can increase the security by using Hyper-V isolation mode to isolate each container in a lightweight VM).|
||||
|Operating system|Runs a complete operating system including the kernel, thus requiring more system resources (CPU, memory, and storage).|Runs the user mode portion of an operating system, and can be tailored to contain just the needed services for your app, using fewer system resources.|
|Guest compatibility|Runs just about any operating system inside the virtual machine|Runs on the same operating system version as the host (Hyper-V isolation enables you to run earlier versions of the same OS in a lightweight VM environment)|
|Deployment|Deploy individual VMs by using Windows Admin Center or Hyper-V Manager; deploy multiple VMs by using PowerShell or System Center Virtual Machine Manager.|Deploy individual containers by using Docker via command line; deploy multiple containers by using an orchestrator such as Azure Kubernetes Service.|
|Operating system updates and upgrades|Download and install operating system updates on each VM. Installing a new operating system version requires upgrading or often just creating an entirely new VM. This can be time-consuming, especially if you have a lot of VMs...|Updating or upgrading the operating system files within a container is the same:<br><br>1. Edit your container image's build file (known as a Dockerfile) to point to the latest version of the Windows base image.<br>    <br>2. Rebuild your container image with this new base image.<br>    <br>3. Push the container image to your container registry.<br>    <br>4. Redeploy using an orchestrator.  <br>    The orchestrator provides powerful automation for doing this at scale.|
|Load balancing|Virtual machine load balancing moves running VMs to other servers in a failover cluster.|Containers themselves don't move; instead an orchestrator can automatically start or stop containers on cluster nodes to manage changes in load and availability.|

  

- **Container architecture**
    
    - A container is an isolated, lightweight silo for running an application on the host operating system.
        
    - Containers build on top of the host operating system's kernel (which can be thought of as the buried plumbing of the operating system), and contain only apps and some lightweight operating system APIs and services that run in user mode, as shown in this diagram.
        

![](file:///tmp/lu1430504drlds.tmp/lu1430504drlhc_tmp_949fc42b.png)

- **Virtual machine architecture**
    
    - In contrast to containers, VMs run a complete operating system–including its own kernel–as shown in this diagram.
        

![](file:///tmp/lu1430504drlds.tmp/lu1430504drlhc_tmp_a94a120e.png)

  

**Why containers-**

- Agility- When developers build and package their applications into containers and provide them to IT to run on a standardized platform, this reduces the overall effort to deploy applications and can streamline the whole dev and test cycle. This also increases collaboration and efficiency between dev and operations teams to ship apps faster.
    
- Portability- Containers provide a standardized format for packaging and holding all the components necessary to run the desired application. This solves the typical problem of “It works on my machine” and allows for portability between OS platforms and between clouds. Any time a container is deployed anywhere, it executes in a consistent environment that remains unchanged from one deployment to another. You now have a consistent format, from dev box to production.
    
- Rapid scalability- Since containers do not have the overhead typical of VMs, including separate OS instances, many more containers can be supported on the same infrastructure. The lightweight nature of containers means they can be started and stopped quickly, unlocking rapid scale-up and scale-down scenarios.
    

  

**Containers Services-**

- Azure Container Registry-
    
    - It is a managed registry service based on the open-source Docker Registry 2.0.
        
    - Create and maintain Azure container registries to store and manage your container images and related artifacts.
        
    - Use Azure container registries with your existing container development and deployment pipelines, or use Azure Container Registry Tasks to build container images in Azure.
        
    - Build on demand, or fully automate builds with triggers such as source code commits and base image updates.
        
- Azure Container Instances-
    
    - Containers are becoming the preferred way to package, deploy, and manage cloud applications.
        
    - Azure Container Instances offers the fastest and simplest way to run a container in Azure, without having to manage any virtual machines and without having to adopt a higher-level service.
        
    - Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs
        
- Azure App services-
    
    - Azure App Service is an HTTP-based service for hosting web applications, REST APIs, and mobile back ends. You can develop in your favorite language, be it .NET, .NET Core, Java, Node.js, PHP, and Python.
        
    - Applications run and scale with ease on both Windows and Linux-based environments.
        
    - App Service adds the power of Microsoft Azure to your application, such as security, load balancing, autoscaling, and automated management.
        
    - Additionally, you can take advantage of its DevOps capabilities, such as continuous deployment from Azure DevOps, GitHub, Docker Hub, and other sources, package management, staging environments, custom domain, and TLS/SSL certificates.
        
- Azure Container Groups-
    
    - A container group is a collection of containers that get scheduled on the same host machine.
        
    - The containers in a container group share a lifecycle, resources, local network, and storage volumes. It's similar in concept to a pod in Kubernetes.
        
    - The following diagram shows an example of a container group that includes multiple containers:
        

![](file:///tmp/lu1430504drlds.tmp/lu1430504drlhc_tmp_df20746f.png)

  

- This example container group:
    
    - Is scheduled on a single host machine.
        
    - Is assigned a DNS name label.
        
    - Exposes a single public IP address, with one exposed port.
        
    - Consists of two containers. One container listens on port 80, while the other listens on port 5000.
        
    - Includes two Azure file shares as volume mounts, and each container mounts one of the shares locally.
        

- Azure Kubernetes Service-
    
    - Azure Kubernetes Service (AKS) simplifies deploying a managed Kubernetes cluster in Azure by offloading the operational overhead to Azure.
        
    - As a hosted Kubernetes service, Azure handles critical tasks, like health monitoring and maintenance.
        
    - When you create an AKS cluster, a control plane is automatically created and configured.
        
    - This control plane is provided at no cost as a managed Azure resource abstracted from the user. You only pay for and manage the nodes attached to the AKS cluster.
        
- Azure Service Fabric-
    
    - Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.
        
    - Service Fabric also addresses the significant challenges in developing and managing cloud native applications.
        
    - A key differentiator of Service Fabric is its strong focus on building stateful services.
        
    - You can use the Service Fabric programming model or run containerized stateful services written in any language or code.
        
    - You can create Service Fabric clusters anywhere, including Windows Server and Linux on premises and other public clouds, in addition to Azure.
        

  

**Creating a Container Registry**

- By default the registry name will have the suffix azurecr.io
    
- In this quickstart, you create a Basic registry, which is a cost-optimized option for developers learning about Azure Container Registry. Choose other tiers for increased storage and image throughput, and capabilities such as connection using a private endpoint.
    
- Before pushing and pulling container images, you must log in to the registry instance through CLI
    
- To push an image to an Azure Container registry, you must first have an image.
    
- Before you can push an image to your registry, you must tag it with the fully qualified name of your registry login server.
    
- After pushing the image, to list the images in your registry, navigate to your registry in the portal and select Repositories.