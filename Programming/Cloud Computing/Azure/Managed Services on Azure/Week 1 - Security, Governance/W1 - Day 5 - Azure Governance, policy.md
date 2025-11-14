[[Governance]]

# Governance
Accordance to company's policies

Azure policies, initiatives and Blueprints 

# Services

*Azure Policy* -> Enforce rules on azure resources. Tracking resources so they are compliant with organization's policies. 
- For example, maybe storage accounts require encryption. Maybe managed identity is required. Maybe department tags are required for each resources. 
- If you don't enable encryption, you wont be able to continue with deployment 

How to apply these policies -> *Azure Policy*.

There are built in, but you can build custom

*Azure Initiative* -> Group of policies that can be applied together. Saves you time/work 

*Azure Blueprint* -> Having guidelines when creating a new project. Defines a set of standards to bring consistency and compliance.

In blueprint you can include policies, role assignments, resource groups and ARM templates. 


## Azure Policy 
Can be applied at the subscription level or resource level. 

For example, there is a custom policy -> Disk encryption should be applied on virtual machines. 

You can also enforce Managed Identity for Function Apps. 

Policies have a *definition* which is defined in a json file. This file can be modified to fit what you need.
- Policy rule filed is mandatory in the json. 

example:
![[Pasted image 20251111205450.png]]


### Policy Effects
*Deny Effect* -> Deny the creation of a resource
- If the resource doesn't exist, creation will be denied. f
- If it already exists, it will be flagged as non compliant 

*Audit Resource* -> You are allowed to create the resource but it will show as non compliant.
- If the resource doesn't exist then you create it, it will be flagged as non compliant 
- If it already exists, it will also be flagged.  

In the json above, this is shown in the `"effect"` 



