https://manuelpracticeaws1.signin.aws.amazon.com/console

MFA -> factor -> piece of evidence. 
possession, inheritance, location, etc. 
- Convenience vs security 


account = root user 

# IAM

3 different identity objects:
user -> people or applications that need access to your account
Group -> collection of related users
Role -> used by AWS services or granting external access to your account 
policy -> allow or deny access to AWS services 

IAM main uses:
1) identity provider - IDP. 
2) authentication
3) authorize - allow or deny access to resources 

only 1 account root user - only used for the initial account user, then you use IAM users. 
- You only give the specific permissions needed to the IAM users. 

When you create IAM users you get a URL. They must be unique inside your account. 

*Least privilege access* -> Only grant the necessary permissions for an account. 

IAM can do as much as the root user, root user has full privilege, so it is best practice to create an additional identity and only give it the permissions it requires. 

IAM Policy -> Objects that allow or deny access to AWS services. 

No cost 