# Dev Ops
Bring in the development and operations team together so they can manage the life cycle of a project from end to end.

Set of practices that can help us manage and deploy our projects end to end 

In Azure Dev Ops is done by a group of managed services for teams.

Source control for versioning

Pipelines for automated application deployments 

Define processes/guidelines for projects -> source controls, reviews that need to be done. 

## Two types of pipelines in Azure - CI/CD
CI -> Continuous Integration. If someone places code in the source code, you can grab that to start building. 
- Create Build

CD -> Continuous Deployment -> If something is built and there is output files, we can continuous built from that process. 
- Release Build 

Azure supports different templates to quickly deploy pipelines. 
## Azure Dev Ops in Cloud
You can use it on cloud and on prem by installing Azure DevOps Server

## Supports integration
You can connect to the external resources you currently have. You don't have to use all of the azure resources, you can use your own. For example if you want your source code to be in GitHub, you can do that. 

## Azure Boards
Agile Tools - Tracker of progress, issues, etc. 

You can set up Scrum and Kanban

## Azure Repo
Source control within Azure DevOps, you can choose the type of repo:
- Git 
- Team Foundation Version Control

## Azure Test Plans
Application testing - manual and continuous 

## Azure Artifacts
Common place to share packages 

You can reuse packages, you don't need to re download packages. 

Putting common components from another applications in Artifacts 

# Dev Ops Environment | Dev.azure.com
This is where dev ops is performed. 

You can have public or private projects. You can also choose the version control software (by default git)

Inside this environment you can create your own custom dashboards. For example to track work items, test plans, burn down charts, burn up charts, etc. 

## Boards
Help us mange work items 

There is a sprint section - similar to Jira/Agile/Trello

## Pipelines 
You can connect to git hub to use that as your source code in your pipeline 

## Branches & Policies
You can create branches and attach them to work items. Within the branches you can also specify the policies/permissions so that your code is safe. 

For example you can set a minimum number of reviewers -> how many people need to see the code before it is pushed.

Comment resolution -> comments need to be checked before pushing 

# Creating a Project Repo 
The professor creates a project:
1) a basic website in the local env (vs code)
2) check in into dev branch
	1) clone, created project, commit, push
3) Pull request to pull changes into main branch
4) Build pipeline to build project
5) Deploy project into Azure App Service
	1) created app service plan (azure cli)
	2) created app service (azure cli)
	3) deploy code inside app service (task for deployment) 

You can clone a repo from HTTPS or SSH into your coding environment like Vs code. There is an option in vscdoe to clone a repo directly. 

# Building a Pipeline - Build - CI pipeline
Takes code from source control and builds a pipeline 

There is no mandatory requirement for where you store the source code

*classic editor* -> UI designer to build your pipeline without YAML
- Templates are available for you to build. 

## Run times
*Hosted Azure Pipeline* -> Azure provides the infrastructure for your run time
- Whatever time it takes to build your project is what you will be billed
- or you can use a private run time by setting up your own machines 

You also specify the agent/machine specifications. If these do not fit your requirements, you need to create your own VM.

*Path to publish* -> staging directory defined in the `variables` section

After you click run, you can track the progress in `pipelines`.

After it grabs everything from your `main branch` it will start running the jobs to build the code. 

### Build Policies
You can add a policy to test code before merging to the main branch. You can build any policies you want to ensure the right code is pushed into the pipelines. 


# Release Pipeline - CD pipeline - Deployment
Release pipeline in the left hand side console management 

There are templates here as well

You can build in the CI pipeline then do the release pipeline to push into kubernetes 

*Artifact* -> Files you want to deploy. 

Deploy the build pipeline by choosing it in the Source. This is how you combine both pipelines. 
![[Pasted image 20251125172205.png]]

### End to end release pipeline
![[Pasted image 20251125172301.png]]

Between each stage you can add 'pre' and 'post' deployment conditions. For example, if you want to deploy into UAT (2nd stage), it will only go into UAT if the team lead approves. Here you can put the name of the approver. 

Stages can be set in different environments (Dev, UAT, Prod)

inside the `task` section you can determine what will be deployed. Here you choose what infrastructure you require. You can choose templates, deploy something like Azure CLI commands, deploy an azure function, there are many options here. 


Adding tasks -> 1) Azure CLI, 2) Azure CLI, 3) App Service Deploy (code goes here).![[Pasted image 20251125172923.png]]

You will also need to provide the connection information with the *Service Connection* feature. For example, you can connect to Github, Docker, etc. In this video the professor connected to Azure to use the Azure CLI through the Service Principal with scope level Subscription. 

After connection is setup:
![[Pasted image 20251125173343.png]]

### Creating release 
After every task is defined, you click on `create release` and it will begin executing the pipeline. You can choose which stages you want to deploy on. 

All build versions will be listed in this section as well

The email notifications are built into the release pipeline 

After the Stage is approved, the status will change to `Queued`. It will be ready until it finishes running all the tasks we set up. 





