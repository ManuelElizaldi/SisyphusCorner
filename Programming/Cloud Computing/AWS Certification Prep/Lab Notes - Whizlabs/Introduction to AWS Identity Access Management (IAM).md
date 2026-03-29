IAM - service that helps users control access to AWS resources. 
- Creating IAM users and adding them to IAM groups. 
- No need of sharing AWS account credentials. 
- IAM is used to control who is authenticated and authorized to use AWS resources. 

The first user in IAM is the root user, which has access to all resources. 

The primary resources in IAM are users, groups, roles, policies, and identity providers.

## Lab
### Creating a user
Inside IAM, you go into Users section. When creating the user we give him access to the Management Console (this is where everything is created in AWS).

We set a custom password and unchecked the user must create password at login (since this is a lab).

In permissions we leave everything in default but we do add a tag:
`key:Dev-Team` `value:Developers`

We can send these log in setting to the person that will use this user or we can copy and paste them. We get a url that is used to log in into this user:
`https://629830531209.signin.aws.amazon.com/console`


We created 1 additional user for the Dev Team and the 2 other users for the HR team with the tags:
`key: HR-Team` `value:HR`


### Creating a User Group
When creating a group you set the name and you choose which users are going to be part of this group. 

This is what I see in the *Add user to group* section: 
![[Pasted image 20260329095919.png]]

In this window, you can't actually see which user belongs to what tag, but I was able to open in a new window and there check its tags. 

Then we have the *Attach permissions section*:![[Pasted image 20260329100557.png]]

The two permissions we selected:
- **AmazonEC2ReadOnlyAccess**
- **AmazonS3ReadOnlyAccess**

Both provide read access to Ec2 and S3
- Read access: You can open, read/view, copy files but not modify them. You can use resources without the ability to modify them.  

For HR Team we only give them *Billing* permission policy -> Grants permissions for billing and cost management

> [!NOTE] AWS Access Analyzer 
> **Access Analyzer**, which uses automated reasoning to help identify the resources that an IAM policy allows or denies access to. This can be useful for identifying unintended access and for auditing IAM policies to ensure they conform to security best practices. Access Analyzer also provides recommendations for how to modify policies to remove unintended access, making it easier to maintain a secure AWS environment


