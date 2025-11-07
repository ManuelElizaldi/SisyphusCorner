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

*Managed Identities* -> Provides as identity to resources 
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

![[Pasted image 20251105201028.png]]

## Accessing Key Vault with Functions - Service Principal 
Create a function, which needs authentication, for this we use *service principal*

