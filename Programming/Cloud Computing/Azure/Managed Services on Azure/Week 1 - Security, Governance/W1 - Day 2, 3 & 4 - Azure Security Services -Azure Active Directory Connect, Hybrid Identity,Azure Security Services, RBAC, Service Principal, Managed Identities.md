[[Cybersecurity]] [[Cloud Security]]
# Hybrid Identity 
On prem users can access on prem applications and cloud resources. You don't have to create all the users in the organization on the cloud. You create a single identity for the user and it is called *hybrid identity*

Sync on prem to cloud users

single sign on environment 

# Azure AD Connect 
Synchronize identities across on prem AD and azure AD 

Utility that is downloaded on your on-prem environment 

Synchronize users, groups and other entities 
- Not passwords, for that you have to specify separately 

## Azure AD connect health
Monitors the connection between on prem AD and Azure AD to ensure reliability 

Continuous syncing is happening, so you need to check if this is working properly 

## Authentication Options for Azure AD Connect
Supports different authentication options:
- Password hash synchronization
- Pass - through authentication
- Active Directory Federation Services (ADFS)

### Password Hash Synchronization
This means that all passwords will be synced from on prem environment active directory to azure active directory 

Unified sign in experience that doesn't require additional infrastructure

Hash is like scrambling data, one way process. Encryption is a two way process. Hash cannot be turned to its original form 

*Example* -> user: ABC, password: 123, 
- then the hash is 456, which is stored on prem. 
	- When sync happens b/w on prem and cloud it will take the value 456 stored on prem and create a hash of this, then this hash will be 789 and passed to azure active directory 
	- This type of sync happens every 2 minutes 
- User can get a token from on prem and azure active directory when they input credentials 

### Pass-through authentication
This set up allows users to log in to Azure without Azure Active Directory storing the password. AAD compares the credentials to the on prem AD, and if they are valid the user can log in. 

Don't sync passwords in the cloud with the on prem environment 

user can go to on prem AD and get token from there 

user can also go to azure active directory and AAD will collect the credentials on behalf of the user 

### Active Directory Federation Services (ADFS)
If you are not comfortable with AAD storing passwords, ADSF doesn't sync any passwords. 

AAD cannot collect the credentials on behalf on-prem AD 

User has to go on prem, provide credentials, get a token and access on prem or cloud applications

User cannot go to AAD and provide credentials 

You require additional infrastructure to use this option 
- allows smart card auth, RSA tokens 

# Security Services 
*Role Based Access Control* -> Assign access to identities (users or user groups) using built in or custom roles 

*Azure Active Directory* -> MFA, conditional Access, PIM, Access Reviews 
- PIM = Privileged Identity Management 

*Network Security* -> inbound and outbound rules, firewall, DDoS protection, private link

*Application Security* -> Web application firewalls (prevents attacks at an application level)

*Azure Security Center* -> big service in the cloud, Cloud Security Posture Management (CSPM), Cloud Workloud Protection Platform (CWPP) 
- *CSPM* = Free.
	- Security of cloud resources. Continuously monitor for misconfigurations, policy violations and compliance gaps. 
	- *Prevents risks through configuration and policy management*
- *CWPP* = Costs 
	- runtime protection for workloads running on the cloud, secure VMs, containers, serverless functions and other compute workloads against vulnerabilities. 
	- *Protecting running workloads not just checking configurations*
	- These monitor if there's suspicious malware running in VMs

*Azure Key Vault* -> store secrets (passwords, connection strings, etc.)

*Managed Identities* -> Provides an identity for a resources. One per resource. It creates a service account for the service. Then you don't need to provide credentials for the service to access the Key Vault.  
- Another type of user that is in azure and we can grant access on different resources 

## Role Based Access Control
Role -> set of permissions, they can be custom or built in. 

Identity -> which user, group of users or AAD application

Scope -> At what level do I want to give permission. At subscription level, management group level, resource group or at an individual resource level. 
- Inside each level, there's a Access Control (IAM) section, here you can create roles 

The combination of these 3, constitutes RBAC 

> [!NOTE] Contributor Role
> Can do everything the owner can, except grant permissions. there are many pre defined contributor roles. 


## Azure Key Vault
Service where you can centrally store secrets, keys (RSA), certificates 

With a key vault, you don't need to maintain secrets in apps individually. 

If there's changes in the secret (password), you can update it in one place. 

You can have multiple vaults, and each environment points to different vault 
### Setting up 
Clicking on add gives you a common azure set up window, also if you haven't created a vault, it will prompt you to create one. 
- when naming the vault, the name needs to be unique since urls will be generated for your keys 

Once you create a vault, you can create secrets here. You can upload passwords from the console management window or CLI. 

inside upload options, you can select upload or generate as well.
- for generate, you can select the type of encryption 
![[Pasted image 20251105201458.png]]

![[Pasted image 20251105202114.png]]

There are url created for your secrets, applications can hit this url to get the passwords 
- You will need a bearer token to access this

If you want to view the secret 

### Pricing tiers
Standard -> contains everything you need. 

Premium -> includes HSM backed keys -> Hardware security module. This are extra secure 

Soft delete is always enabled, but you decide for how many days the keys are kept 
- if you delete the entire key vault, the information will still be available to restore for the amount of days you choose 
 
## Why Key Vault?
Secure vault completely - if there are multiple applications in an environment, and each application has its passwords.

If you each application is accessing a database, and the sql password is in the config file. In these set up each application is managing its own passwords. 

To solve this, you can create a *key vault* and everything is stored here, including the connection string to the database. Instead of using a connection string to access the database, they can make a call to the key vault.

Using a key vault enables you to not put secrets inside the code. 

![[Pasted image 20251105201028.png]]

## Accessing Key Vault with Functions - Service Principal 
Create a function, which needs authentication, for this we use *service principal*

# Service Principal
Service account on the on prem environment. A type of user you are creating which has user, user id, password but it can't do interactive authentication. Not in the ID format, its not a proper user that can be added to the active directory. 

Is essentially an Identity used by an application, service or automation tool to access azure resources. 
- User account for an app 

This is the same as a service account from google API. 

## Creating Service Principal | AAD App
For this you require the AAD app on your on-prem environment. Once you get this app, you get a user id and password, which can receive permissions to access the key vault. 

Inside the Azure Active Directory, you go to *App Registrations*, click on + New Registration. 

![[Pasted image 20251111192407.png]]

1) Create Azure Active Directory Application. 
2) Inside the AAD you can find the client id, client secret and tenant ID/directory ID. 
	1) Inside Certificates and secrets is where you can create a new client secret (password)
3) Give access to the application from the Key Vault
	- To give access you go inside the Key Vault -> Access Policies and inside here you can give permissions to your AAD App. You can choose to give access to keys, secrets or permissions. You decide which permissions you give. In the demo shown in the lecture, the professor gave all the permissions in Secrets. You also choose which principal will receive permissions. 
	

Once you give the necessary permissions:
If you don't have a function, create one. Inside Code + Test is where you write the code for the function. The professor showed code that has a function that receives the key vault name and secret it wants to access/grab. It also receives the tenant ID, client ID and client secret so that authentication can be performed.  

After you run the function you get a json back with your request.

In case you don't want to type the secret strings (tenant id, client id and secret), you can deploy *Managed Identities*
### Use case - Azure Function & Key Vault 
You have a Key Vault and a data base. You also have an azure function that needs to access the database.

For this you create the *AAP App/Service Principal*. The application receives permission to access the Key Vault. 

1) Inside the Azure Function, you can use the AAP user Id (client id) and password (client secret) in your code and use that to authenticate and get a token to access the key vault. 
2) You give token + secret you want to access to the Key Vault 
3) Key Vault returns the Secret -> The function can now access the data base 

With these steps you ensure that you don't need to put secrets in your code. 
![[Pasted image 20251111192116.png]]

# Managed Identities
This can be deployed to remove the password and user id from the code and still get access to the key vault. 

In previous steps, we had a function that would take in client id, tenant id and client secret. 

When you enable Managed Identities, then there is a AAD App that is created for the particular resource. 

## Setting Up
Inside the Functions app, you go to *Identity*. System Assigned Managed Identity. It creates a Service Principal that is only applicable to the function app. There can only be one per service. 

You still need to grant permissions from the Key Vault to let the resource access the Key Vault. 

Steps:
1) Enable *Managed Identity* inside resource. 
2) Give Access to Managed Identity on Key Vault
3) The resource can ask for a token from the key vault. Internally it uses the Service Principal from the resource. If permissions are right, then you do get the token back when you run the function (code).

The only thing you need is to point to the right key vault and secret name

### Where is this used
You can grant Managed Identity to a VM so it can access secrets, functions also use this (very common). In app services. 
- The VM can be granted identity and the app inside the VM can grab the secret 

Azure Data Factory as well 


> [!NOTE] Managed Identity Over All Security Services
> Managed Identity is the recommended service. It is more scalable and safer than the o

