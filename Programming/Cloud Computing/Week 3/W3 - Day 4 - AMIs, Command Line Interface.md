[[Operating System]] [[AMI]]

# AMIs
AMI = OS

EC2 -> uses elastic block storage and the instance contains:
- OS
- Dependencies
- App
- Customization
- Tools
- Patches

Setting this up multiple times can cause errors, just as we saw in earlier classes. We also have Console to code to prevent this. Also, being real, one instance wont host an entire app. You use multiple EC2s.

AMIs can be created by users. You can place all your requirements to run you app inside an AMI and use that to launch other instances. 

AMIs can also be sold in the AWS marketplace 

## Real Life Example
A company needs 3 different environments -> 1) developing, 2) testing 3) production 

They create an AMI with the necessary configurations to run the application. They create this template and if the development team needs more instances they can use this template/custom AMI to launch new instances for them to work on reducing error while setting them up. 

This makes sure all 3 environments match 

#### Practice quiz question: Typically an AMI includes which of the following?

OS, app, customization, configurations, tools and patches  


# AWS Command Line Interface - Definition and uses 
AWS CLI is an open source and unified tool that allows you to interact with AWS services using you CLI shell.

It allows you to automate services through scripts 
and reduce human error, it also reduces time to market. In addition to this it allows operations to be repeatable 

used by operation engineers

Using AWS CLI is considered [[IaC]] (infrastructure as code)

it can be downloaded here -> https://aws.amazon.com/cli/

There are other 
## Automation Options
AWS CLI -> Used to interact with AWS accounts and write shell scripts to automate tasks

Other scripting languages can also be used to automate tasks. 
- For this the Boto3 dependency is needed. -> This module provides the necessary libraries to interact with AWS. 

There are other software that allow you to automate infrastructure:
- chef
- puppet 
- terraform -> go to option now a days

These tools work by integrating with AWS via [[OpsWorks]]

## Providing Programmatic Access to a user using IAM 
In order to use the CLI, you will need the right permissions from the IAM. 
- access key and secret keys are used.
	- These keys are also used for the SDK and other API tools 

But before that, you need to set up the AWS CLI with the proper access keys. 

On Linux the .aws folder contains all the configuration and credential files needed to run the AWS CLI 


# AWS CLI DIY 
Used a launch template to create the instances requested by the exercise 

Since this is my learning account, I had to manually set up the CLI in my linux machine. For this I installed the awscli using sudo apt install. Then performed the command `aws config`, entered the following place holder values:

![[Pasted image 20250620174355.png]]

After that I got the actual access key and secret access key from [here](https://awsacademy.instructure.com/courses/120745/modules/items/11429638). This is where we start the lab. I found the keys in AWS Details and then in the directory home/.aws I modified the credentials file. 

After doing the above, I entered the command `aws ec2 describe-instances` which successfully gave me a list of all the instances I currently have set up. 

A more complex command could be `aws ec2 describe-instances --filters Name=instance-state-name,Values=stopped`. Important args here:
- Values = stopped -> this will return any stopped instances

Using filters to isolate the instance information -> `aws ec2 describe-instances --filters Name=instance-state-name,Values=stopped | grep InstanceId | awk '{printf "%s\n", $2}'`

![[Pasted image 20250620175939.png]]
These are the IDs of stopped instances 

Shell scripting examples:
![[Pasted image 20250620180204.png]]
Here we create a list of instances based on a given criteria. 

This can also be done through a more concise command -> `aws ec2 describe-instances --region us-east-1 --instance-ids $instance_id --query 'Reservations[*]. Instances[*]. PublicIpAddress' --output text`

From the cli you can run bash scripts, like this one:

```bash
bash terminator.sh
```

```shell
#If this mode is not true then the script will NOT delete any resources. Good for reporting
DELETE_MODE=true
printf "\nLooking for EC2 instances\n"
printf "*********************************************************************************************************************\n"
ID_LIST1=$(aws ec2 describe-instances --filters Name=instance-state-name,Values=running,stopped | grep InstanceId | awk '{printf "%s", $2}')
ID_LIST2=${ID_LIST1//\"} #Get rid of the double quotes
ID_LIST3=${ID_LIST2//\,/ } #Replace the comma with a space
if [ "x$ID_LIST3" = "x" ]; then
 printf "No instances found to be terminated\n"
else
 printf "Terminating instances $ID_LIST3"
 if [ "$DELETE_MODE" = true ]; then
 aws ec2 terminate-instances --instance-ids $ID_LIST3
 echo " Done!"
 else
 echo " Skipped"
 fi
fi
```

this script terminates the instances inside the environment 

![[Pasted image 20250620180920.png]]

This is the output after running the script 


The CLI can also be used for [[Monitoring]] tasks. You can use commands that return the information 




--- 
#### Sources
[CLI documentation](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html)

