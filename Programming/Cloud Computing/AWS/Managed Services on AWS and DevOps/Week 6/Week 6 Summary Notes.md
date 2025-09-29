**Class Notes – Managed Services on AWS and DevOps Week 6**

  

# CloudFormation

  

AWS CloudFormation is a service that helps you model and set up your AWS resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and CloudFormation takes care of provisioning and configuring those resources for you. You don't need to individually create and configure AWS resources and figure out what's dependent on what; CloudFormation handles that.

![[Pasted image 20250915180734.png]]

# Features

1. **Extensibility**
    

Using the AWS CloudFormation Registry, you can model and provision third-party resources and modules published by AWS Partner Network (APN) Partners and the developer community. Examples of third-party resources are monitoring, team productivity, incident management, and version control tools, along with resources from APN Partners such as MongoDB, Datadog, Atlassian Opsgenie, JFrog, Trend Micro, Splunk, Aqua Security, FireEye, Sysdig, Snyk, Check Point, Spot by NetApp, Gremlin, Stackery, and Iridium. You can also browse, discover, and choose from a collection of pre-built modules by JFrog and Stackery, along with those maintained by AWS Quick Starts.

  

2. **Cross account & cross-region management**
    

CloudFormation StackSets let you provision a common set of AWS resources across multiple accounts and regions, with a single CloudFormation template. StackSets takes care of automatically and safely provisioning, updating, or deleting stacks, no matter where they are.

  

3. **Authoring with JSON/YAML**
    

CloudFormation allows you to model your entire cloud environment in text files. You can use open-source declarative languages, such as JSON or YAML, to describe what AWS resources you want to create and configure. If you prefer to design visually, you can use AWS CloudFormation Designer to help you get started with AWS CloudFormation templates.

  

4. **Safety controls**
    

CloudFormation automates provisioning and updating your infrastructure in a safe and controlled manner. There are no manual steps or controls that can lead to errors. You can use Rollback Triggers to specify the CloudWatch alarms that CloudFormation should monitor during the stack creation and update process. If any of the alarms are triggered, CloudFormation rolls back the entire stack operation to a previously deployed state.

Using ChangeSets, you can preview the proposed changes that CloudFormation intends to make to your infrastructure and application resources prior to execution, so that your deployments go exactly as planned. CloudFormation determines the right operations to perform, provisions resources in the most efficient way possible, and rolls back automatically if errors are encountered. This returns the state of your infrastructure and application resources to the last known good state. Using Drift Detection, you can keep track of changes to resources outside CloudFormation, making sure you always have the most up-to-date picture of your infrastructure.

**Template**

A CloudFormation template is a JSON or YAML formatted text file. You can save these files with any extension, such as .json, .yaml, .template, or .txt. CloudFormation uses these templates as blueprints for building your AWS resources. For example, in a template, you can describe an Amazon EC2 instance, such as the instance type, the AMI ID, block device mappings, and its Amazon EC2 key pair name. Whenever you create a stack, you also specify a template that CloudFormation uses to create whatever you described in the template.

For example, if you created a stack with the following template, CloudFormation provisions an instance with an ami-0ff8a91507f77f867 AMI ID, t2.micro instance type, testkey key pair name, and an Amazon EBS volume.

**Stacks**

When you use CloudFormation, you manage related resources as a single unit called a stack. You create, update, and delete a collection of resources by creating, updating, and deleting stacks. All the resources in a stack are defined by the stack's CloudFormation template. Suppose you created a template that includes an Auto Scaling group, Elastic Load Balancing load balancer, and an Amazon Relational Database Service (Amazon RDS) database instance. To create those resources, you create a stack by submitting the template that you created, and CloudFormation provisions all those resources for you. You can work with stacks by using the CloudFormation console, API, or AWS CLI.

  

**Working Principle**

When creating a stack, AWS CloudFormation makes underlying service calls to AWS to provision and configure your resources. CloudFormation can only perform actions that you have permission to do. For example, to create EC2 instances by using CloudFormation, you need permissions to create instances. You'll need similar permissions to terminate instances when you delete stacks with instances. You use AWS Identity and Access Management (IAM) to manage permissions.

The calls that CloudFormation makes are all declared by your template. For example, suppose you have a template that describes an EC2 instance with a t2.micro instance type. When you use that template to create a stack, CloudFormation calls the Amazon EC2 create instance API and specifies the instance type as t2.micro. The following diagram summarizes the CloudFormation workflow for creating stacks.

![[Pasted image 20250915180751.png]]

1. Use the AWS CloudFormation Designer or your own text editor to create or modify a CloudFormation template in JSON or YAML format. You can also choose to use a provided template. The CloudFormation template describes the resources you want and their settings. For example, suppose you want to create an EC2 instance. Your template can declare an Amazon EC2 instance and describe its properties.
    
2. Save the template locally or in an Amazon S3 bucket. If you created a template, save it with a file extension like: .json, .yaml, or .txt.
    
3. Create a CloudFormation stack by specifying the location of your template file, such as a path on your local computer or an Amazon S3 URL. If the template contains parameters, you can specify input values when you create the stack. Parameters allow you to pass in values to your template so that you can customize your resources each time you create a stack.
    

When you need to update your stack's resources, you can modify the stack's template. You don't need to create a new stack and delete the old one. To update a stack, create a change set by submitting a modified version of the original stack template, different input parameter values, or both. CloudFormation compares the modified template with the original template and generates a change set. The change set lists the proposed changes. After reviewing the changes, you can start the change set to update your stack or you can create a new change set. The following diagram summarizes the workflow for updating a stack.

![[Pasted image 20250915180800.png]]

  

  

# Terraform

HashiCorp Terraform is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share. You can then use a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle. Terraform can manage low-level components like compute, storage, and networking resources, as well as high-level components like DNS entries and SaaS features.

  

Terraform creates and manages resources on cloud platforms and other services through their application programming interfaces (APIs). Providers enable Terraform to work with virtually any platform or service with an accessible API.

  

  

HashiCorp and the Terraform community have already written thousands of providers to manage many different types of resources and services. You can find all publicly available providers on the Terraform Registry, including Amazon Web Services (AWS), Azure, Google Cloud Platform (GCP), Kubernetes, Helm, GitHub, Splunk, DataDog, and many more.

  

The core Terraform workflow consists of three stages:

  

- Write: You define resources, which may be across multiple cloud providers and services. For example, you might create a configuration to deploy an application on virtual machines in a Virtual Private Cloud (VPC) network with security groups and a load balancer.
    
- Plan: Terraform creates an execution plan describing the infrastructure it will create, update, or destroy based on the existing infrastructure and your configuration.
    
- Apply: On approval, Terraform performs the proposed operations in the correct order, respecting any resource dependencies. For example, if you update the properties of a VPC and change the number of virtual machines in that VPC, Terraform will recreate the VPC before scaling the virtual machines.
    

![[Pasted image 20250915180815.png]]

## Terminology

  

**Resource**

Resource is aws_vpc, aws_db_instance, etc. A resource belongs to a provider, accepts arguments, outputs attributes, and has a lifecycle. A resource can be created, retrieved, updated, and deleted.

  

**Resource module**

Resource module is a collection of connected resources which together perform the common action (for e.g., AWS VPC Terraform module creates VPC, subnets, NAT gateway, etc). It depends on provider configuration, which can be defined in it, or in higher-level structures (e.g., in infrastructure module).

  

**Infrastructure module**

An infrastructure module is a collection of resource modules, which can be logically not connected, but in the current situation/project/setup serves the same purpose. It defines the configuration for providers, which is passed to the downstream resource modules and to resources. It is normally limited to work in one entity per logical separator (e.g., AWS Region, Google Project).

  

For example, terraform-aws-atlantis module uses resource modules like terraform-aws-vpc and terraform-aws-security-group to manage the infrastructure required for running Atlantis on AWS Fargate.

  

Another example is terraform-aws-cloudquery module where multiple modules by terraform-aws-modules are being used together to manage the infrastructure as well as using Docker resources to build, push, and deploy Docker images. All in one set.

  

**Composition**

Composition is a collection of infrastructure modules, which can span across several logically separated areas (e.g.., AWS Regions, several AWS accounts). Composition is used to describe the complete infrastructure required for the whole organization or project.

  

A composition consists of infrastructure modules, which consist of resources modules, which implement individual resources.

  

**Data source**

Data source performs a read-only operation and is dependant on provider configuration, it is used in a resource module and an infrastructure module.

  

Data source terraform_remote_state acts as a glue for higher-level modules and compositions.

  

The external data source allows an external program to act as a data source, exposing arbitrary data for use elsewhere in the Terraform configuration. Here is an example from the terraform-aws-lambda module where the filename is computed by calling an external Python script.

  

The http data source makes an HTTP GET request to the given URL and exports information about the response which is often useful to get information from endpoints where a native Terraform provider does not exist.

  

  

References –

1. CloudFormation Documentation - [https://docs.aws.amazon.com/cloudformation/](https://docs.aws.amazon.com/cloudformation/)
    
2. Terraform Documentation - [https://www.terraform.io/](https://www.terraform.io/)
    
3. CloudFormation Datasheet - [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/AWS_CloudFormation_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/AWS_CloudFormation_Datasheet.pdf)