Professor -> Deepak Yenti

# Azure Certifications
There are organizations that are on both clouds (AWS & Azure)
- Azure demand is high 

![[Pasted image 20251111175612.png]]

Start with Azure Fundamentals, after the course you should be able to do this easily. Azure Admin is trickier, questions are more complex. After getting Azure fundamentals study for admin, AI Fundamentals is also available if you want to work on that 
- The professor passed the Azure Admin on the second chance 

Security Engineer are also popular. These are easier than the Azure Admin
- policies, security, etc. 

Azure Data Engineer are also popular 

There is also an Agent AI exam that will come out this November


# Design and Governance 
When you first start working, most resources are already built. 
![[Pasted image 20251111180109.png]]

Account/Enterprise Agreement -> From an account perspective, that's where it starts. This is where you open an account, in a professional context you don't see this step. Everything on top of this you do see. 

You do see subscriptions for example, to organize resources. 

After agreement -> tenant (owner of the environment). 

## Roles
*Owner, contributor and reader*. These are the 3 roles and then there are specific roles for specific services. 

An owner can make someone else an owner. Owner can do anything inside the environment. 

It can also attach more users. 

*Contributor* -> everything the owner can do, but it can't create users or groups or invite other users. 

*Reader* -> only can read 

# Tenant & Subscriptions
Entra = IAM 

First is *tenant* -> The organization starts here. Roles start below tenant. 
- Subscriptions belong to tenants. 
- You can have a tenant in each different region
	- Tenant US based, then another in India. They all belong to the same organization. 
	- If users are created in US, the user can only see the users that belong to this tenant. If the user wants to see the resources in India, it first needs to be transferred. 

After tenants, you will see *subscriptions = Landing Zones* -> where your resources are created. 
- A Landing Zone is an Environment where you create and run resources. 
- Subscriptions = accounts in AWS. 
- You create subscriptions at the Business Unit level -> one per department, for example, one for marketing, one for IT, one for HR, etc. 
- Without subscriptions you can't create resources

You can think of a subscriptions as a container for all your workloads and billing. You can have a subscription for testing, another for development, each business unit should have its own subscription. 

# Azure Hierarchy Overview 
```
Azure (Cloud)
└── Tenant (Azure AD / Microsoft Entra ID)
    ├── Management Groups
    │   ├── Sub-management groups
    │   │   └── Subscriptions
    │   │       ├── Resource Groups
    │   │       │   └── Resources (VMs, Storage, Databases, etc.)
    │   │       └── Policies, RBAC, Budgets
    │   └── Policies, Role Assignments
    └── Directory Users, Groups, Service Principals

```

## Real Life Hierarchy 
```yaml
Tenant: Contoso Corporation (contoso.onmicrosoft.com)
└── Management Group: Root
    ├── mg-Platform
    │   └── Subscription: Shared-Services
    │       └── RG: rg-monitoring
    │           ├── Log Analytics Workspace
    │           └── Azure Firewall
    ├── mg-Production
    │   └── Subscription: Prod-Apps
    │       └── RG: rg-api-prod
    │           ├── App Service (API)
    │           └── SQL Database
    └── mg-Development
        └── Subscription: Dev-Apps
            └── RG: rg-api-dev
                ├── App Service (API)
                └── Storage Account

```


# Management Groups 
*Management Groups* govern subscriptions/business units. The management groups determine what machines can be deployed by each business unit. 
- For example, HR wont need a super powerful machine, nor storage, etc. For that you create management groups

You can create policies at the subscription level, that way, the group that has those policies attached, wont be able to create high demanding machines. 

## Setting Up Management Group
Created inside *Resource Manager* -> *Management Group* 

You can add a subscription to the management group, 

# Availability Zones and Sets

region -> one or more data centers in different regions. 

zone -> US east 1, US east 2. Helps spread resources in the same region. 

Availability Zone -> Logical container that redundant VMs can be created within. Distribute resources to gain resilience. If you have critical applications, if the data center goes down, you will still have access to your resources. 
- Same data center 

Fault Domain -> Group of physical devices that represent one point of failure. 

Update domain -> Group of devices that get updated together 

# Proximity Placement Groups
Indicates that data center collocation requirements within a region 

Reduces latency between resources 

# Dedicated Host
If traditional cloud computing is an apartment building where each tenant rents a room, dedicated host is when you have your own house and now one shares infrastructure with you. 


