## Microsoft Azure - 5

Azure Active Directory (Azure AD) is a cloud-bVishalased identity and access management

service. This service helps your employees access external resources, such as

Microsoft 365, the Azure portal, and thousands of other SaaS applications. Azure AD

also helps them access internal resources. These are resources like apps on your

corporate network and intranet, along with any cloud apps developed by your own

Organization.

- Allows Identity and Access Management.![](file:///tmp/lu1415788dmdr3.tmp/lu1415788dmdu1_tmp_28515321.png) ![](file:///tmp/lu1415788dmdr3.tmp/lu1415788dmdu1_tmp_28515321.png)
    

Authentication Authorisation

(Sign In) (getting resource permission)

  

- Create users (internal and external), Groups, Azure Active directory applications Etc.
    
- Setup Custom domains.
    

Ex: Ravikumar[@](mailto:Akshay.verma@organisationname.com)[organisationname](mailto:Akshay.verma@organisationname.com)[.com](mailto:Akshay.verma@organisationname.com)

- Use Azure Active directory to sign in, and access resources.
    
- Protect resources using access management.
    
- Integrated with many enterprise services like Microsoft 365.
    
- Different licenses are available.
    

  

Let's get an overview of a few important terms used

- Azure Tenant: This is the top-level container that holds all your subscriptions and their resources. It represents an organization in Azure.
    
- Azure Active Directory (AAD): This is a cloud-based identity and access management service provided by Microsoft Azure. It's often associated with an Azure AD directory tied to your Azure Tenant.
    
- Subscription: A subscription groups together user accounts and the resources that have been created by those user accounts. It's essentially a billing unit in Azure.
    
- Resource Group: A resource group is a logical container for resources deployed on Azure. It helps you organize and manage your Azure resources.
    

  

  

**Who uses Azure AD?**

**IT admins**: As an IT admin, use Azure AD to control access to your apps and your app

resources, based on your business requirements. For example, you can use Azure AD

to require multi-factor authentication when accessing important organizational

resources. You can also use Azure AD to automate user provisioning between your

existing Windows Server AD and your cloud apps, including Microsoft 365. Finally,

Azure AD gives you powerful tools to automatically help protect user identities and

credentials and to meet your access governance requirements.

  

**App developers**: As an app developer, you can use Azure AD as a standards-based

approach for adding single sign-on (SSO) to your app, allowing it to work with a user's

pre-existing credentials. Azure AD also provides APIs that can help you build

personalized app experiences using existing organizational data.

  

**Microsoft 365, Office 365, Azure, or Dynamics CRM Online subscribers**: As a

subscriber, you're already using Azure AD. Each Microsoft 365, Office 365, Azure, and

Dynamics CRM Online tenant is automatically an Azure AD tenant. You can

immediately start to manage access to your integrated cloud apps.

  

  

Azure Active Directory- Identity

● Create users (internal/external), groups, AAD applications etc.

● Provides Authentication capabilities

➢ Multi-factor authentication (MFA) and self-service password reset (SSPR)

  

● Create B2B or B2C Azure AD

➢ B2B– Handle internal users (employees) and external users.(It is meant for an organization)

➢ B2C– Allows users to create & manage accounts, sign-in to applications.

  

● Provides Identity Protection

➢ Setup user-risk and sign-in risk policies

Ex: Let's say we are in India and suddenly there is a login from the US. In this situation an active directory will flag this as a sign-in risk.

  

● Hybrid identity setup– Connect on- prem AD with Azure AD

  

**Hybrid Identity**

Today, businesses, and corporations are becoming more and more a mixture of on-premises and cloud applications. Users require access to those applications both on-premises and in the cloud. Managing users both on-premises and in the cloud poses challenging scenarios.

Microsoft’s identity solutions span on-premises and cloud-based capabilities. These solutions create a common user identity for authentication and authorization to all resources, regardless of location. We call this hybrid identity.

- Organizations users need access to on-prem and cloud resources.
    
- Instead of managing two identities for a user, create Hybrid Identity.
    
- Users can sign-in at one location and access resources anywhere.
    

  

Azure Active Directory- Access

● Setup Role-based Access Control (RBAC)

● Setup Conditional Access policies

For e.g. use MFA for management or admin tasks, allow access to only certain

locations, block risky sign-ins etc.

● Provides Privileged Identity Management (PIM)

➢ Enable Just-in-Time access, set approval workflows etc.

  

● Perform Access Reviews

➢ Review the granted permissions automatically, ask group owners to periodically

confirm access etc.

  

  

Azure AD Connect

Azure AD Connect is an on-premises Microsoft application that's designed to meet and

accomplish your hybrid identity goals. If you're evaluating how to best meet your goals,

you should also consider the cloud-managed solution Azure AD Connect cloud sync.

  

Azure AD Connect provides the following features:

● **Password hash synchronization**

- All the password will be synced from on-prem AD to Azure AD
    
- Password sync happens every 2 min.
    

  

● **Pass-through authentication**

- Do not sync any password with Azure AD.
    

Now Use can either go to on-prem AD provide the credential and then on-prem AD will provide the token.

- User can also go to Azure AD and Azure Ad will collect the credentials on behalf of the user.
    

Now these credentials are passed on to the on-prem environment, on-prem will authenticate the user and if successful provide will give the token to the user.

● **Federation integration** - Federation is an optional part of Azure AD Connect

and can be used to configure a hybrid environment using an on-premises AD FS

infrastructure. It also provides AD FS management capabilities such as certificate

renewal and additional AD FS server deployments.

● **Synchronization** - Responsible for creating users, groups, and other objects. As

well as, making sure identity information for your on-premises users and groups

is matching the cloud. This synchronization also includes password hashes.

● **Health Monitoring** - Azure AD Connect Health can provide robust mon

  

  

Azure Security Services

![](file:///tmp/lu1415788dmdr3.tmp/lu1415788dmdu1_tmp_8d7ac8fc.png)

- **Role-based Access Control**
    

Access management for cloud resources is a critical function for any organization that is using the cloud. Azure role-based access control (Azure RBAC) helps you manage who has access to Azure resources, what they can do with those resources, and what areas they have access to.

Azure RBAC is an authorization system built on [Azure Resource Manager](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview) that provides fine-grained access management to Azure resources.

**Roles** are basically a set of permissions.

- There are a lot of built in roles that are available in Azure or we can create custom roles as well.
    
- Identity : can be a user/ group /Azure AD app
    
- Scope, means to what level we need to give the permissions: be at subscription level, management level, Resource group level.
    

So the combination of Role, Identity and scope is what constitutes Role-based access control.

  

- **Azure Active Directory**
    

Features like MFA, Conditional access, PIM, Access Review, etc

- **Network Security**
    

Network security group, DDOS protection, Private Link, etc

- **Application Security**
    

Web application Firewall : The Azure Web Application Firewall (WAF) on Azure Application Gateway actively safeguards your web applications against common exploits and vulnerabilities.

- **Azure Security Center**
    

Azure Security Center is a security management tool that allows you to gain insight into your security state across hybrid cloud workloads, reduce your exposure to attacks, and respond to detected threats quickly.

  

**Azure Key Vault**

Azure Key Vault is a cloud service for securely storing and accessing secrets. A secret is anything that you want to tightly control access to, such as API keys, passwords, certificates, or cryptographic keys.

  

Azure Key Vault helps solve the following problems:

- **Secrets Management** - Azure Key Vault can be used to Securely store and tightly control access to tokens, passwords, certificates, API keys, and other secrets.
    

  

- **Key Management** - Azure Key Vault can be used as a Key Management solution. Azure Key Vault makes it easy to create and control the encryption keys used to encrypt your data.
    

  

- **Certificate Management** - Azure Key Vault lets you easily provision, manage, and deploy public and private Transport Layer Security/Secure Sockets Layer (TLS/SSL) certificates for use with Azure and your internal connected resources.
    

  

**Service Principle**

An Azure service principal is an identity created for use with applications, hosted services, and automated tools to access Azure resources. This access is restricted by the roles assigned to the service principal, giving you control over which resources can be accessed and at which level. For security reasons, it's always recommended to use service principals with automated tools rather than allowing them to log in with a user identity.

  

  

**Managed Identities**

A common challenge for developers is the management of secrets and credentials used

to secure communication between different components making up a solution. Managed

identities eliminate the need for developers to manage credentials.

  

Managed identities provide an identity for applications to use when connecting to

resources that support Azure Active Directory (Azure AD) authentication. Applications

may use the managed identity to obtain Azure AD tokens. With Azure Key Vault,

developers can use managed identities to access resources. Key Vault stores

credentials in a secure manner and gives access to storage accounts.

  

  

Azure Governance Services

Governance in Azure is one aspect of Azure Management. This section covers the

different areas of management for deploying and maintaining your resources in Azure.

Management refers to the tasks and processes required to maintain your business

applications and the resources that support them. Azure has many services and tools

that work together to provide complete management. These services aren't only for

resources in Azure, but also in other clouds and on-premises. Understanding the

different tools and how they work together is the first step in designing a complete

management environment.

The following diagram illustrates the different areas of management that are required to

maintain any application or resource. These different areas can be thought of as a

lifecycle. Each area is required in continuous succession over the lifespan of a

resource. This resource lifecycle starts with the initial deployment, through continued

operation, and finally when retired.

![](file:///tmp/lu1415788dmdr3.tmp/lu1415788dmdu1_tmp_67c47398.png)

  

  

**Azure policies**

Azure Policy helps to enforce organizational standards and to assess compliance

at-scale. Through its compliance dashboard, it provides an aggregated view to evaluate

the overall state of the environment, with the ability to drill down to the per-resource,per-policy granularity. It also helps to bring your resources to compliance through bulk

remediation for existing resources and automatic remediation for new resources.

  

Common use cases for Azure Policy include implementing governance for resource

consistency, regulatory compliance, security, cost, and management. Policy definitions

for these common use cases are already available in your Azure environment as

built-ins to help you get started. All Azure Policy data and objects are encrypted at rest.

  

**Azure Initiative**

- Group of azure policies that can be applied together
    

  

Initiatives enable you to group several related policy definitions to simplify assignments

and management because you work with a group as a single item. For example, you

can group related tagging policy definitions into a single initiative. Rather than assigning

each policy individually, you apply the initiative.

  

**Azure Blueprint**

Just as a blueprint allows an engineer or an architect to sketch a project's design

parameters, Azure Blueprints enables cloud architects and central information

technology groups to define a repeatable set of Azure resources that implements and

adheres to an organization's standards, patterns, and requirements. Azure Blueprints

makes it possible for development teams to rapidly build and stand up new

environments with trust they're building within organizational compliance with a set of

built-in components, such as networking, to speed up development and delivery.

  

Blueprints are a declarative way to orchestrate the deployment of various resource

templates and other artifacts such as:

  

- **Role assignments**
    
- **Policy assignments**
    
- **Azure Resource Manager Template**
    
- **Resource Group**
    

  

The Azure Blueprints service is backed by the globally distributed Azure Cosmos DB.

Blueprint objects are replicated to multiple Azure regions. This replication provides low

latency, high availability, and consistent access to your blueprint objects, regardless of

which region Azure Blueprints deploys your resources to.