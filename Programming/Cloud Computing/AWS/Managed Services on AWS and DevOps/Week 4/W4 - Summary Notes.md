# Elastic Container Registry

Amazon Elastic Container Registry (Amazon ECR) is an AWS managed container image registry service that is secure, scalable, and reliable. Amazon ECR supports private repositories with resource-based permissions using AWS IAM. This is so that specified users or Amazon EC2 instances can access your container repositories and images. You can use your preferred CLI to push, pull, and manage Docker images, Open Container Initiative (OCI) images, and OCI compatible artifacts.

![[Pasted image 20250825185441.png]]

# Features

1. **Amazon container orchestrator integration**
    

Amazon Elastic Container Registry (Amazon ECR) is integrated with Amazon Elastic Container Service (Amazon ECS) and Amazon Elastic Kubernetes Service (Amazon EKS), which means you can easily store and run container images for applications with either orchestrator. All you need to do is specify the Amazon ECR repository in your task or pod definition for Amazon ECS or Amazon EKS to retrieve the appropriate images for your applications.

  

2. **OCI and Docker support**
    

Amazon ECR supports Open Container Initiative (OCI) standards and the Docker Registry HTTP API V2. This allows you to use Docker CLI commands (e.g., push, pull, list, tag) or your preferred Docker tools to interact with Amazon ECR, maintaining your existing development workflow. You can easily access Amazon ECR from any Docker environment, whether in the cloud, on-premises, or on your local machine. Amazon ECR lets you store Docker container images and related OCI artifacts in your repositories.

  

3. **Public container image and artifact gallery**
    

You can discover and use container software that vendors, open source projects, and community developers share publicly in the Amazon ECR public gallery. Popular base images such as operating systems, AWS-published images, Kubernetes add-ons, and files, such as Helm charts, can be found in the gallery. You don’t need to use an AWS account to search or pull a public image; however, using your account makes it easier and faster to use public container software.

  

4. **AWS Marketplace**
    

Amazon ECR stores both the containers you create and any container software you buy through AWS Marketplace. AWS Marketplace for Containers offers verified container software for high performance computing, security, and developer tools, as well as software as a service (SaaS) products that manage, analyze, and protect container applications.

  

5. **High availability and durability**
    

Amazon ECR stores your container images and artifacts in Amazon Simple Storage Service (S3). Amazon S3 is designed for 99.999999999% (11 9’s) of data durability because it automatically creates and stores copies of all S3 objects across multiple systems. This means that your data is available when needed and protected against failures, errors, and threats. Amazon ECR can also automatically replicate your data to multiple AWS Regions for your high availability applications.

  

6. **Team and public collaboration**
    

Amazon ECR supports the ability to define and organize repositories in your registry using namespaces. This allows you to organize your repositories based on your team’s existing workflows. You can set which API actions another user may perform on your repository (e.g., create, list, describe, delete, and get) through resource-level policies, allowing you to share your repositories easily with different users and AWS accounts. You can easily share your container artifacts with anyone in the world by storing them in a public repository.

  

7. **Access control**
    

Amazon ECR uses AWS Identity and Access Management (IAM) to control and monitor who and what (e.g., EC2 instances) can access your container images. Through IAM, you can define policies to allow users within the same AWS account or other accounts to access your container images in private repositories. You can also further refine these policies by specifying different permissions for different users and roles (e.g., push, pull, or full administrator access). Anyone in the world can access your container images stored in public repositories for worldwide collaboration.

  

8. **Encryption**
    

You can transfer your container images to and from Amazon ECR via HTTPS. Your images are also automatically encrypted at rest using Amazon S3 server-side encryption. Amazon ECR also lets you choose your own key managed by AWS Key Management Service (AWS KMS) to encrypt images at rest.

  

9. **Third-party integrations**
    

Amazon ECR is integrated with third-party developer tools. You can integrate Amazon ECR into your continuous integration and delivery process, allowing you to maintain your existing development workflow.

  

10. **Pull through cache repositories**
    

With Amazon ECR’s pull through cache repositories, you can retrieve, store, and sync container artifacts stored in publicly accessible container registries. They offer the high download rates that you need and the availability, security, and scale that you’ve come to depend on. With frequent registry syncs and no additional tools to manage, pull through cache repositories help you keep container images sourced from public registries up to date.

  

# Elastic Container Service

Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications. As a fully managed service, Amazon ECS comes with AWS configuration and operational best practices built-in. This also means that you don't need to manage control pane, nodes, or add-ons. It's integrated with both AWS and third-party tools, such as Amazon Elastic Container Registry and Docker. This integration makes it easier for teams to focus on building the applications, not the environment. You can run and scale your container workloads across AWS Regions in the cloud, and on-premises, without the complexity of managing a control plane or nodes.

![[Pasted image 20250825185458.png]]

  

# Features

The following are key features of Amazon ECS:

- **A serverless option with AWS Fargate.** With AWS Fargate, you don't need to manage servers, handle capacity planning, or isolate container workloads for security. Fargate handles the infrastructure management aspects of your workload for you. You can schedule the placement of your containers across your cluster based on your resource needs, isolation policies, and availability requirements.
    
- **An external instance option with ECS Anywhere.** With ECS Anywhere, you can use the Amazon ECS console and AWS CLI to manage your on-premises container workloads.
    
- **An Amazon EC2 option.** With EC2, you can use the Amazon ECS console and AWS CLI to manage your EC2 instances.
    

- **Integration with AWS Identity and Access Management (IAM)**. You can assign granular permissions for each of your containers. This allows for a high level of isolation when building your applications. In other words, you can launch your containers with the security and compliance levels that you've come to expect from AWS.
    
- **AWS managed container orchestration.**
    
- **Continuous integration and continuous deployment (CI/CD).** This is a common process for microservice architectures that are based on Docker containers. You can create a CI/CD pipeline that takes the following actions:
    
    - Monitors changes to a source code repository
        
    - Builds a new Docker image from that source
        
    - Pushes the image to an image repository such as Amazon ECR or Docker Hub
        
    - Updates your Amazon ECS services to use the new image in your application
        
- **Support for service discovery.** This is a key component of most distributed systems and service-oriented architectures. With service discovery, your microservice components are automatically discovered as they're created and terminated on a given infrastructure.
    
- **Support for sending your container instance log information to CloudWatch Logs**. After you send this information to Amazon CloudWatch, you can view the logs from your container instances in one convenient location. This prevents your container logs from taking up disk space on your container instances.
    

# Fargate architecture overview

Amazon ECS is a Regional service that simplifies the management involved with running containers in a highly available manner across multiple Availability Zones within an AWS Region. You can create Amazon ECS clusters within a new or existing VPC. After a cluster is up and running, you can create task definitions that define which container images run across your clusters. Your task definitions are used to run tasks or create services. Container images are stored in and pulled from container registries, such as the Amazon Elastic Container Registry.

The following diagram shows the architecture of an Amazon ECS environment that runs on AWS Fargate.

![[Pasted image 20250825185510.png]]

  

  

  

**References –**

1. **ECR Documentation -** [**https://docs.aws.amazon.com/ecr/**](https://docs.aws.amazon.com/ecr/)
    
2. **ECS Documentation -** [https://docs.aws.amazon.com/ecs/](https://docs.aws.amazon.com/ecs/)
    
3. **ECR Datasheet -** [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_Elastic_Container_Registry_(ECR)_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_Elastic_Container_Registry_\(ECR\)_Datasheet.pdf)
    
4. **ECS Datasheet -** [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_Elastic_Container_Service_(ECS)_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/Amazon_Elastic_Container_Service_\(ECS\)_Datasheet.pdf)