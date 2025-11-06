[[Managed Services]]
# Active Directory - Intro
Manage users and their permissions 

Identity and access management 
- Which user has which access?
- To do anything in azure you need to be in the active directory 

users can be external and internal 

Initial Domain name -> You get a default domain name: `<name>.onmicrosoft.com` 
- The initial domain name is the domain that has not been customized 

Inside the active directory you can create custom domains, for example:
- greatlearning.onmicrosoft.com, then you create mohit@greatlearning.onmicrosoft.com
	- Each domain is a user. 
	- If the user is using the domain within the active directory, it will be an *internal user*
	- If you add a user but its not using the active directory's domain, then its an *external user*

sign in through Azure AD and then access resources 

Licenses are available here

# Setting up Azure Active Directory & Features
When you first log in and create an Azure account you become the Azure Tenant
- If you create 2 tenants, there is absolutely no link between them
	- Inside the Active Directory there is a button to create a new tenant but if you click this, there will be no connection between the two accounts
- *Default Directory* = active directory. -> this is the active directory you create when you first log in 
- Being a tenant means you are the global administrator 

If you log in to an organization's Azure, you are a user 

Subscriptions are inside the active directory 

## Creating Custom Domain Names
![[Pasted image 20251103180356.png]]

Inside this window you can add custom domain names. 

After you create a custom domain, when you create a new user, you get the option to choose this custom domain instead of the initial domain. 

### When creating a user
There is also an option to create a guest user. You invite users based on their email address. When you invite a user, it sends him an email to set up the azure account on your active directory. 

## Creating Groups
You can create a group of users to set permissions to that specific group. 

For example, the database team is the only on that has permissions to access the dbs 

## Creating a Tenant
use *B2B active directory* -> meant for organizations
- add employees and they can access resources
- handles internal and external users 

use a *B2C active directory* -> you are creating a service, for example an e-commerce business. In this setting, users are allowed to create and manage accounts, sign in to applications 
- Once they sign in, you can control these accounts, reset passwords, etc. 

When you choose your country, you choose the data center location (this is important for some industries).

> [!NOTE] Active Directory and Subscriptions
>Subscriptions can't be shared with other active directories. An active directory CAN have multiple subscriptions, but it can't share them with other active directories.  

## Enterprise Applications
Single sign (SSO) on with other cloud providers = connects azure active directory to other cloud provider's authentication systems.

Mainly used to unify identity and access management across cloud environments 

Users can log in to azure and then click on the AWS icon and they are signed in automatically to AWS. No separate accounts needed.  

You can connect users from other application into your active directory
- for example, you can connect to drop box and save all of your files there instead of using azures storage options. 

## Identity Protection
Multi factor authentication

Identity protection -> if there's sign in risk, user risk, etc. 

Hybrid Identity -> connect on prem AD with Azure AD 


# Active Directory Access

*Role Based Access Control* -> Assign access to identities (users or user groups) using built in or custom roles 

*Conditional Access policies* -> You decide to which users or user groups can have access, which devices, what locations, etc. There are many conditions you can build.
- If there's a log in risk access, you can determine what to do with this user. 
- If the conditions are true, you can block or authorize a user
- You can ask users for multi factor authentication 

*Authentication Methods* -> You can ask users for a text code, authentication app or other methods. 

*Privileged Identity Management (PIM)*
- Just in time access, set approval workflows 

*Access Reviews* -> every month (you decide frequency) you check who has access, checks for permissions and sets emails to accept permissions 



