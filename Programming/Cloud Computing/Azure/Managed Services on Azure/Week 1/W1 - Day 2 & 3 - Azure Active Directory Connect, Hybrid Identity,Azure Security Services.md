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
- CSPM = Free
- CWPP = Costs 

These monitor if there's suspicious malware running in VMs

*Azure Key Vault* -> store secrets (passwords, connection strings, etc.)

*Managed Identities* -> Provides as identity to resources 
- Another type of user that is in azure and we can grant access on different resources 
