# Terraform Cheat Sheet

#### Policy Statement
```hcl
statement {
  principals { ... }   # WHO
  actions   = [...]    # WHAT THEY CAN DO
  resources = [...]    # ON WHAT
  effect    = "Allow"  # ALLOW OR DENY
  condition { ... }    # ONLY IF
}
```

```
statement {
  sid       = "Name"        # label, optional
  effect    = "Allow"       # or "Deny" — Deny always wins
  principals { ... }        # WHO
  actions   = ["kms:Decrypt"]   # WHAT ACTION
  resources = ["*"]         # ON WHAT
  condition { ... }         # ONLY IF
}
```

#### Block types
```
terraform { }   # settings for Terraform itself (versions, backend)
provider  { }   # how to reach a platform (AWS region, credentials)
resource  { }   # CREATES something. Costs money. Shows in plan.
data      { }   # READS or COMPUTES something. Creates nothing. Free.
```

#### Commands
```
terraform init      # download providers. Once per directory.
terraform fmt       # canonical formatting
terraform validate  # syntax + references. No AWS calls.
terraform plan      # dry run. Reads AWS, changes nothing.
terraform apply     # makes real changes. Costs money.
terraform destroy   # tears down everything in state
```

# Lab
Had to install the new version of awscli, for this I had to remove it and then re install it. 

When checking the version of the software after installing I got this error:

```
manu  /tmp  aws --version
bash: /usr/bin/aws: No such file or directory

```

I had to add aws to the PATH, but that was not the fix, the fix was simpler, I only needed to clear the cache, because bash was still looking for the removed path. We had to reset the cache with:

`hash -r`

you can use \rm to bypass any aliases

We create an additional user inside the AWS account so that it has isolated permission. 
- one example of this is not granting it AWS management console. We only need CLI for this lab. 
- Also, we only grant Admin access (AdministratorAccess).


## Attaching policies directly 
We are only going to give this account the permissions it needs. 
- AdministratorAccess

We also create access keys for this account inside the Create Access Key section. 
- We tag it with the corresponding tag to identify it. 
  - `hipaa-labs-terraform`

After creating the access key we get 2 values, the access key and secret access key.

Also it is good to know that the credentials are stored in ~/.aws/credentials 

we can also run the command `aws sts get-caller-identity --profile hipaa-labs` to verify if we set up the profile correctly. 

We setup the CLI for our hipaa labs with this command before hand `aws configure --profile hipaa-labs` this is how we told the system we are working on the hipaa-labs profile. 
### Best practices for storing this keys
password manager 

## Installing terraform
There were a couple of dependencies we needed to install before using terraform. 

We also need the ashicorps GPG key 

```
# 1. Install dependencies
sudo apt update && sudo apt install -y gnupg software-properties-common curl

# 2. Add HashiCorp's GPG key
wget -O- https://apt.releases.hashicorp.com/gpg | \
  gpg --dearmor | \
  sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

# 3. Verify the key fingerprint
gpg --no-default-keyring \
  --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
  --fingerprint
```

Those were the commands I ran 

step 2, with the wget gets us the public hashicorp public key and stored in the machine. 
- some of the bash commands I don't understand but the goal was to get the key inside the machine. 

In step 3 we print out the key into the terminal to determine if we go it right. it looks like this:

`798A EC65 4E5C 1542 8C8E  42EE AA16 FCBC A621 E701`

This is a publish hash key that proves hashi corp's identity to me.  Next time I do a sudo apt update, apt will look at this key and compare it before downloading any packages. 

Note -> most of this stuff can be located here https://developer.hashicorp.com/terraform/install#linux on their official website 

## Cloning the Repo
Since the desktop will be the only place where I will work on these labs I cloned it to my Projects folder on the desktop

Added a .gitignore specialized for terraform, I have never used this before, only have used gitignore for python. Interesting to compare the two configs. 
```
# Terraform state — contains resource IDs, potentially secrets. Never commit.
*.tfstate
*.tfstate.*

# Variable values — real tfvars may contain account-specific info
*.tfvars
!*.tfvars.example

# Terraform working directory — provider binaries, large
.terraform/

# Crash logs
crash.log
crash.*.log

# OS noise
.DS_Store
```


#### terraform.tfstate
This is Terraform's memory. This file keeps track of what was done. Terraform's job is to make reality (infrastructure) match your code. For that it needs to look at your code (what infrastructure you want), current state (what terraform believe exists) and current state (what actually exists - through AWS APIs). 

After each apply, Terraform writes a json with the mapping of resources. 

When there's a difference between current state and what should be - it is called *drift*.

#### What is Terraform.tfvars 
Variables/values specific to your account, for example:
```hcl
# terraform.tfvars
aws_region = "us-east-1" 
environment = "lab" 
bucket_prefix = "hipaa-lab01-manu"
```

tfvars is where things like environment-specific secrets and account IDs end up.

two files 
- variables.tf -> declares that a variable exists, name, type, description. Which is code committed. 
- terraform.tfvars -> assigns your values to those variables. This is configuration specific to your account. 

#### What is .terraform.lock.hcl
This file is similar to a python requirements.txt file you run on pip to ensure you use the right version of a package to run it. 

## Important Note
Always commit first the .gitignore. A terraform.tfstate can contain sensitive information 

## Continuing With Repo Config
2 commands inside the lab 1 folder inside the repo:

```
mkdir -p lab-01-kms-cloudtrail/{terraform,diagrams,verification,writeup}
mkdir -p docs
```

The braces command is something new I had never seen, but basically this is a way to call several mkdir commands at once. 

### Declaring a versions.tf
Inside the folder, I assume each lab gets its own variables I created the versions.tf file. These are the contents:

```
terraform {
  required_version = "~> 1.9"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

'~>' is a pessimistic constraint operator. What this does is that it allows versions from 1.9 up to the last 1.x version. My current version is 1.15. It would block any 2.0 versions. 

The *providers* section will transform all terraform resources into AWS API calls. 
- This is a sort of plugin that translates Terraform's generic resource model into the specific platform 
- CloudFront only speaks AWS, Terraform can speak any other API provider.

Here's another example including Azure provider API
```
required_providers {
  aws = {
    source  = "hashicorp/aws"
    version = "~> 5.0"
  }
  azurerm = {
    source  = "hashicorp/azurerm"
    version = "~> 4.0"
  }
}
```

### Creating the main.tf 
main <- this name is a trap. At first I thought this was the meat and potatoes of terraform, a place to keep all of the infrastructure. Anything desired in the environment goes here, but no. Terraform happens to not care about names. It only looks at .tf files. Then concatenates them and creates a logical setup of all the files. 

The meat lives in the files named after what they contain:

versions.tf    → toolchain contracts (what versions of what tools)
main.tf        → provider config + shared locals (plumbing)
variables.tf   → input declarations (the knobs)
outputs.tf     → what to print after apply (the receipts)
kms.tf         → ← meat
s3.tf          → ← meat
cloudtrail.tf  → ← meat
iam.tf         → ← meat

main file:

```terraform
provider "aws" {
  region  = var.aws_region
  profile = "hipaa-labs"

  default_tags {
    tags = local.common_tags
  }
}

locals {
  common_tags = {
    Project     = "hipaa-aws-labs"
    Lab         = "lab-01-kms-cloudtrail"
    Environment = var.environment
    ManagedBy   = "terraform"
    DataClass   = "phi-simulated"
  }
}
```


#### Referencing inputs in files
From this file I can see that **var.** is used to reference the variables.tf file. Which we haven't created yet, but will generate in the next step. 

Another examples of using prefix to reference an input:
```
var.aws_region          # input variables (declared in variables.tf)
local.common_tags       # locals (computed values, declared in a locals block)
aws_kms_key.phi.arn     # resource attributes (things AWS returned after creation)
data.aws_caller_identity.current.account_id   # data sources (read-only lookups)
```

This way you can always know where inputs are coming from. 

There are also some hard coded values like the project name, lab and DataClass 

#### Default_tags

### Important detail in main.tf
**Tag** are very important for security reasons. Specially for HIPAA or PHI data. Access, cost allocation of resources and makes audit easier.  

**DataClass** This is just a tag of the data we are working with. 

## Creating variables.tf

```
variable "aws_region" {
  description = "AWS region for all lab resources"
  type        = string
  default     = "us-east-1"
}

variable "environment" {
  description = "Environment tag applied to all resources"
  type        = string
  default     = "lab"
}

variable "bucket_prefix" {
  description = "Prefix for S3 bucket names (must be globally unique when combined with suffix)"
  type        = string
  default     = "hipaa-lab01"
}
```


## After Config files were created
We type these commands inside the terraform directory :

```
terraform init
terraform plan
git status
```

`Terraform init` -> doesn't create infra, it downlaods the provider's plug in so that terraform can talk to AWS 
`terraform plan` -> reads. .tf files, asks aws what currently exists and prints the diff 
`terraform apply` -> command that makes the API call to create infrastructure 

# Terraform mental model
.tf files -> The description of the infrastructure that you want 
- Downloads the AWS provider plugin so that terraform can create infrastructure 

.terraform/ -> this folder is created when you initalize terraform, providers binaries so that terraform can talk to aws 

`terraform apply` -> this will create the infrastructure in your AWS 

### Init - Creates a .lock.hcl file 
When we init terraform, we initalize terraform 

# Interlude
I discovered that I installed vscode through flatpak, sometimes linux is can have its hurdles. I discovered this when I ran terraform init and the vscode terminal said it was not available, but when I tried it on the host terminal it did work. I had never enocuntered this when using vscode on mac or windows. So I had to uninstall and reinstall through the microsoft .deb package. 

# Building KMS Keys
## iam.tf file
We create this file to create three roles - role is not attached to anything, its just a set of permissions. The file determines who can borrow/use them. 

in the iam.tf file we create 3 roles - one for ingestion, processing and finally a third as a control, to prove that security is being enforced. You need permission from the S3 and the KMS key to access the PHI data. 

This file creates 3 roles
## kms.tf file
This file creates the KMS key and what each role can perform with the key

This file creates the KMS key  

### At this point terraform will create 5 resources 
3 roles, 1 key 1 alias for the key 

## Some Terraform Syntax - block types

```
resource "aws_iam_role" "claims_ingestion" { ... }    # creates something
data "aws_caller_identity" "current" {}               # looks something up
```


## (known after apply)
After running Terraform plan, some field will have this tag. This means AWS has not told terraform the arn value for that resource. Some still need to be created so they won't have one yet. 



after running the commands we have the customer managed key
![[Pasted image 20260807180445.png]]


# How Terraform reaches AWS
inside main.tf - in the provider section `profile = "hipaa-labs"` tells terraform to use the credentials stored under this profile 

inside ~/.aws theres a file named credentials, with a profile named "hipaa-labs"
- main.tf has the profile 

we set up this with the awscli using -> `aws configure --profile hipaa-labs`

### Dependency Graph
This is important, this is where order comes from 

# S3 in Terraform 
Creates a landing zone bucket, locks down how objects can be written on it and gives the the three roles their S3 permissions

## Bucket_key_enabled
Every upload would trigger GenerateDataKey, take this into an enterprise environment and the cost sky rockets. With this setting enabled, S3 keeps a KMS key 

CloudTrail can capture S3 events - which specific objects, by whom, when 

KMS captures - was the key used, by whom, through which service


A lot of roles and permissions to keep track of. I need to draw an architectural plan 

# Half way through this lab - CloudTrail
We have to create an additional KMS key for the logs, if a hacker grabs the KMS key, then he could delete the logs, destroying any evidence. 

We also created an S3 bucket specific for logs. With public access denied and only cloud trail can write to it 

`is_multi_region_trail = true` - this setting is important to set as true in production, without it you can't track what is happening in other regions. An attacker can log into that region and start spinning up resources. 
- since right now we are only building a practice lab it is not requiered. 

# Running into my first terraform error
After running terraform plan for the cloudtrail.tf section of the project I ran into this error: 

```
Plan: 7 to add, 0 to change, 0 to destroy.
╷
│ Error: expected event_selector.1.data_resource.0.type to be one of ["AWS::DynamoDB::Table" "AWS::Lambda::Function" "AWS::S3::Object"], got AWS::KMS::Key
│ 
│   with aws_cloudtrail.phi_audit,
│   on cloudtrail.tf line 200, in resource "aws_cloudtrail" "phi_audit":
│  200:       type   = "AWS::KMS::Key"
│ 
╵
```

event_selector is an older API that only supports three data types, DynamoDB, Lambda functions and S3 objects. KMS is not one of them. 

We need the new API `advanced_event_selector` -> this supports many more resources 

structure of the advanced_event_selector:
```
advanced_event_selector {

name = "PHI key usage"

  

field_selector {

field = "eventCategory"

equals = ["Data"]

}

  

field_selector {

field = "resources.type"

equals = ["AWS::KMS::Key"]

}

  

field_selector {

field = "resources.ARN"

equals = [aws_kms_key.phi_landing_zone.arn]

}

}

}
```


Every field_selector is filtering forward, each section is acts as an and. Or happens inside the field_selector:
```
field_selector { field = "resources.type" equals = ["AWS::S3::Object", "AWS::KMS::Key"] }
```

### Tainted term
When a resource is created but its configuration fails partway through. Terraform marks it tained -> meaning that terraform knows it exists but does not trust it to be correct. 

