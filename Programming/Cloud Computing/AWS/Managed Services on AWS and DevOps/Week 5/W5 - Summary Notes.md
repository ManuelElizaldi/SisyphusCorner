**Class Notes – Managed Services on AWS and DevOps Week 5**

  

CloudTrail

AWS CloudTrail is an AWS service that helps you enable operational and risk auditing, governance, and compliance of your AWS account. Actions taken by a user, role, or an AWS service are recorded as events in CloudTrail. Events include actions taken in the AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs.

![[Pasted image 20250910154453.png]]

Features

AWS CloudTrail enables auditing, security monitoring, and operational troubleshooting. CloudTrail records user activity and API calls across AWS services as events. CloudTrail events help you answer the question of "Who did what, where, and when?"

CloudTrail records two types CloudTrail of events:

- **Management events** that capture control plane actions on resources, such as creating or deleting Amazon Simple Storage Service (S3) buckets.
- **Data events** that capture data plane actions within a resource, such as reading or writing an Amazon S3 object.

CloudTrail uses these event sources in three features:

- Event history provides a 90-day history of control plane actions at no additional cost. As part of its core audit capabilities, CloudTrail provides customer managed keys for encryption and log file validation to enable immutability. You pay for only what you use of the paid features. Some of the following features are provided at no additional charge. No minimum fees or upfront commitments are required.
- AWS CloudTrail Lake is a managed data lake for capturing, storing, accessing, and analyzing user and API activity on AWS for audit and security purposes. You can aggregate, immutably store your activity logs (from AWS and non-AWS sources) for up to seven years and query logs within seconds for search and analysis. Additionally, you can import any existing CloudTrail logs from your S3 buckets into an existing or new CloudTrail Lake event data store. IT auditors can use CloudTrail Lake as an immutable record of all activities to meet audit requirements. Security administrators can verify that user activity is in accordance with internal policies. DevOps engineers can troubleshoot operational issues such as an unresponsive Amazon Elastic Compute Cloud (EC2) instance or a resource being denied access. CloudTrail Lake helps security teams perform retrospective investigations by answering who made what configuration changes to resources associated with security incidents such as data exfiltration or unauthorized access to your AWS environment. CloudTrail Lake helps compliance engineers investigate non-compliant changes to their production environments by relating non-compliant AWS Config rules to who and what resource changes prompted them. IT teams can perform historical asset inventory analysis on configuration items with CloudTrail Lake’s seven-year retention period and SQL query engine.
- Trails capture a record of AWS account activities, delivering and storing these events in S3, with optional delivery to Amazon CloudWatch Logs and Amazon EventBridge. These events can be fed into your security monitoring solutions. You can use your own third-party solutions or solutions such as Amazon Athena for searching and analyzing logs captured by CloudTrail. You can create trails for a single AWS account or for multiple AWS accounts by using AWS Organizations. AWS CloudTrail Insights analyzes control plane events for anomalous behavior in API call volumes and can detect unusual activity such as spikes in resource provisioning or gaps in periodic activity.

Storage Gateway

AWS Storage Gateway is a service that connects an on-premises software appliance with cloud-based storage to provide seamless and secure integration between your on-premises IT environment and the AWS storage infrastructure in the AWS Cloud.

![[Pasted image 20250910154507.png]]

Features

1. **Standard Storage Protocols:** Storage Gateway seamlessly connects to your local production or backup applications with NFS, SMB, iSCSI, or iSCSI-VTL, so you can adopt AWS Cloud storage without needing to modify your applications. Its protocol conversion and device emulation enables you to access block data on volumes managed by Storage Gateway on top of Amazon Simple Storage Service (S3), store files as native Amazon S3 objects or in fully managed cloud file shares with Amazon FSx for Windows File Server, and keep virtual tape backups online in a virtual tape library backed by S3 or move the backups to a tape archive tier on Amazon S3 Glacier and Amazon S3 Glacier Deep Archive.
2. **Fully Managed Cache:** The local gateway appliance maintains a cache of recently written or read data so your applications can have low-latency access to data that is stored durably in AWS. The gateways use a read-through and write-back cache, committing data locally, acknowledging the write operations, and then asynchronously copying data to AWS, reducing application latency.
3. **Optimized and Secure Data Transfer:** Storage Gateway provides secure upload of changed data and secure downloads of requested data, encrypting data in transit between any type of gateway appliance and AWS using SSL. Storage Gateway delivers end-to-end protection of customer data from the Storage Gateway in the enterprise network to the data residing in AWS. The service supports security features and access controls, and supplies compliances and certifications that address enterprise customers’ real and perceived security concerns when using AWS storage via the Storage Gateway Optimizations such as multi-part management, automatic buffering, delta transfers used across all gateway types, and data compression applied for all block and virtual tape data.
4. **High Availability on VMware:** Storage Gateway provides high availability on VMware through a set of health-checks integrated with VMware vSphere High Availability (VMware HA). With this integration, Storage Gateway deployed in a VMware environment on-premises, or in VMware Cloud on AWS, will automatically recover from most service interruptions in under 60 seconds. This protects storage workloads against hardware, hypervisor, or network failures; storage errors; and software errors, such as connection timeouts and file share or volume unavailability. 

  

CodeCommit  

CodeCommit is a secure, highly scalable, managed source control service that hosts private Git repositories. CodeCommit eliminates the need for you to manage your own source control system or worry about scaling its infrastructure. You can use CodeCommit to store anything from code to binaries. It supports the standard functionality of Git, so it works seamlessly with your existing Git-based tools.

  

With CodeCommit, you can:

- Benefit from a fully managed service hosted by AWS. CodeCommit provides high service availability and durability and eliminates the administrative overhead of managing your own hardware and software. There is no hardware to provision and scale and no server software to install, configure, and update.
- Store your code securely. CodeCommit repositories are encrypted at rest as well as in transit.
- Work collaboratively on code. CodeCommit repositories support pull requests, where users can review and comment on each other's code changes before merging them to branches; notifications that automatically send emails to users about pull requests and comments; and more.
- Easily scale your version control projects. CodeCommit repositories can scale up to meet your development needs. The service can handle repositories with large numbers of files or branches, large file sizes, and lengthy revision histories.
- Store anything, anytime. CodeCommit has no limit on the size of your repositories or on the file types you can store.
- Integrate with other AWS and third-party services. CodeCommit keeps your repositories close to your other production resources in the AWS Cloud, which helps increase the speed and frequency of your development lifecycle. It is integrated with IAM and can be used with other AWS services and in parallel with other repositories. 
- Easily migrate files from other remote repositories. You can migrate to CodeCommit from any Git-based repository.
- Use the Git tools you already know. CodeCommit supports Git commands as well as its own AWS CLI commands and APIs.  
    

**Concepts**

- An active user is any unique AWS identity (IAM user/role, federated user, or root account) that accesses AWS CodeCommit repositories during the month. AWS identities that are created through your use of other AWS Services, such as AWS CodeBuild and AWS CodePipeline, as well as servers accessing CodeCommit using a unique AWS identity, count as active users.
- A repository is the fundamental version control object in CodeCommit. It’s where you securely store code and files for your project. It also stores your project history, from the first commit through the latest changes.
- A file is a version-controlled, self-contained piece of information available to you and other users of the repository and branch where the file is stored.
- A pull request allows you and other repository users to review, comment on, and merge code changes from one branch to another.
- An approval rule is used to designate a number of users who will approve a pull request before it is merged into your branch.
- A commit is a snapshot of the contents and changes to the contents of your repository. This includes information like who committed the change, the date and time of the commit, and the changes made as part of the commit.
- In Git, branches are simply pointers or references to a commit. You can use branches to separate work on a new or different version of files without impacting work in other branches. You can use branches to develop new features, store a specific version of your project from a particular commit, etc.

**Repository Features**

- You can share your repository with other users. 
- If you add AWS tags to repositories, you can set up notifications so that repository users receive email about events, such as another user commenting on code. 
- You can create triggers for your repository so that code pushes or other events trigger actions, such as emails or code functions.
- To copy a remote repository to your local computer, use the command ‘git clone’
- To connect to the repository after the name is changed, users must use the ‘git remote set-url’ command and specify the new URL to use.
- To push changes from the local repo to the CodeCommit repository, run ‘git push remote-name branch-name’.
- To pull changes to the local repo from the CodeCommit repository, run ‘git pull remote-name branch-name’.
- You can create up to 10 triggers for Amazon SNS or AWS Lambda for each CodeCommit repository.

**Pull Requests**

- Pull requests require two branches: a source branch that contains the code you want reviewed, and a destination branch, where you merge the reviewed code.
- Create pull requests to let other users see and review your code changes before you merge them into another branch.
- Create approval rules for your pull requests to ensure the quality of your code by requiring users to approve the pull request before the code can be merged into the destination branch. You can specify the number of users who must approve a pull request. You can also specify an approval pool of users for the rule.
- To review the changes on files included in a pull request and resolve merge conflicts, you use the CodeCommit console, the ‘git diff’ command, or a diff tool.
- After the changes have been reviewed and all approval rules on the pull request have been satisfied, you can merge a pull request using the AWS Console, AWS CLI, or with the ‘git merge’ command.
- You can close a pull request without merging it with your code.  
    

**Commit and Branch Features**

- If using the AWS CLI, you can use the ‘create-commit’ command to create a new commit for your branch.
- If using the AWS CLI, you can use ‘create-branch’ command to create a new branch for your repository..
- You can also use Git commands to manage your commits and branches.
- Create a new commit to a branch using ‘git commit -m message’.
- Create a branch in your local repo by running the git checkout -b new-branch-name command.

  

  

CodeBuild

AWS CodeBuild is a fully managed build service in the cloud. CodeBuild compiles your source code, runs unit tests, and produces artifacts that are ready to deploy. CodeBuild eliminates the need to provision, manage, and scale your own build servers. It provides prepackaged build environments for popular programming languages and build tools such as Apache Maven, Gradle, and more. You can also customize build environments in CodeBuild to use your own build tools. CodeBuild scales automatically to meet peak build requests.

CodeBuild provides these benefits:

- **Fully managed** – CodeBuild eliminates the need to set up, patch, update, and manage your own build servers.
- **On demand** – CodeBuild scales on demand to meet your build needs. You pay only for the number of build minutes you consume.
- **Out of the box** – CodeBuild provides preconfigured build environments for the most popular programming languages. All you need to do is point to your build script to start your first build.
- You can use the AWS CodeBuild or AWS CodePipeline console to run CodeBuild. You can also automate the running of CodeBuild by using the AWS Command Line Interface (AWS CLI) or the AWS SDKs.

![[Pasted image 20250910154529.png]]


 As the following diagram shows, you can add CodeBuild as a build or test action to the build or test stage of a pipeline in AWS CodePipeline. AWS CodePipeline is a continuous delivery service that you can use to model, visualize, and automate the steps required to release your code. This includes building your code. A _pipeline_ is a workflow construct that describes how code changes go through a release process.
 
![[Pasted image 20250910154537.png]]
  

Concepts

- A **build project** defines how CodeBuild will run a build. It includes information such as where to get the source code, which build environment to use, the build commands to run, and where to store the build output.
- A **build environment** is the combination of operating system, programming language runtime, and tools used by CodeBuild to run a build.
- The **build specification** is a YAML file that lets you choose the commands to run at each phase of the build and other settings. Without a build spec, CodeBuild cannot successfully convert your build input into build output or locate the build output artifact in the build environment to upload to your output bucket.
- If you include a build spec as part of the source code, by default, the build spec file must be named buildspec.yml and placed in the root of your source directory.
- A collection of input files is called **build input artifacts or build input** and a deployable version of a source code is called **build output artifact or build output**.

CodeDeploy

CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, serverless Lambda functions, or Amazon ECS services.

You can deploy a nearly unlimited variety of application content, including:

- Code
- Serverless AWS Lambda functions
- Web and configuration files
- Executables
- Packages
- Scripts
- Multimedia files

CodeDeploy can deploy application content that runs on a server and is stored in Amazon S3 buckets, GitHub repositories, or Bitbucket repositories. CodeDeploy can also deploy a serverless Lambda function. You do not need to make changes to your existing code before you can use CodeDeploy.

CodeDeploy makes it easier for you to:

- Rapidly release new features.
- Update AWS Lambda function versions.
- Avoid downtime during application deployment.
- Handle the complexity of updating your applications, without many of the risks associated with error-prone manual deployments.

The service scales with your infrastructure so you can easily deploy to one instance or thousands.

CodeDeploy is able to deploy applications to three compute platforms:

- **EC2/On-Premises**: Describes instances of physical servers that can be Amazon EC2 cloud instances, on-premises servers, or both. Applications created using the EC2/On-Premises compute platform can be composed of executable files, configuration files, images, and more.

Deployments that use the EC2/On-Premises compute platform manage the way in which traffic is directed to instances by using an in-place or blue/green deployment type. **AWS Lambda**: Used to deploy applications that consist of an updated version of a Lambda function. AWS Lambda manages the Lambda function in a serverless compute environment made up of a high-availability compute structure. All administration of the compute resources is performed by AWS Lambda. 

You can manage the way in which traffic is shifted to the updated Lambda function versions during a deployment by choosing a canary, linear, or all-at-once configuration.

- **Amazon ECS**: Used to deploy an Amazon ECS containerized application as a task set. CodeDeploy performs a blue/green deployment by installing an updated version of the application as a new replacement task set. CodeDeploy reroutes production traffic from the original application task set to the replacement task set. The original task set is terminated after a successful deployment. You can manage the way in which traffic is shifted to the updated task set during a deployment by choosing a canary, linear, or all-at-once configuration.

**Overview of in-place deployment**

Here's how an in-place deployment works:

1. First, you create deployable content on your local development machine or similar environment, and then you add an _application specification file_ (AppSpec file). The AppSpec file is unique to CodeDeploy. It defines the deployment actions you want CodeDeploy to execute. You bundle your deployable content and the AppSpec file into an archive file, and then upload it to an Amazon S3 bucket or a GitHub repository. This archive file is called an _application revision_ (or simply a _revision_).
2. Next, you provide CodeDeploy with information about your deployment, such as which Amazon S3 bucket or GitHub repository to pull the revision from and to which set of Amazon EC2 instances to deploy its contents. CodeDeploy calls a set of Amazon EC2 instances a _deployment group_. A deployment group contains individually tagged Amazon EC2 instances, Amazon EC2 instances in Amazon EC2 Auto Scaling groups, or both.

Each time you successfully upload a new application revision that you want to deploy to the deployment group, that bundle is set as the _target revision_ for the deployment group. In other words, the application revision that is currently targeted for deployment is the target revision. This is also the revision that is pulled for automatic deployments.

1. Next, the CodeDeploy agent on each instance polls CodeDeploy to determine what and when to pull from the specified Amazon S3 bucket or GitHub repository.
2. Finally, the CodeDeploy agent on each instance pulls the target revision from the Amazon S3 bucket or GitHub repository and, using the instructions in the AppSpec file, deploys the contents to the instance.

CodeDeploy keeps a record of your deployments so that you can get deployment status, deployment configuration parameters, instance health, and so on.

  

**Overview of blue-green deployment**

A blue/green deployment is used to update your applications while minimizing interruptions caused by the changes of a new application version. CodeDeploy provisions your new application version alongside the old version before rerouting your production traffic.

- **AWS Lambda**: Traffic is shifted from one version of a Lambda function to a new version of the same Lambda function.
- **Amazon ECS**: Traffic is shifted from a task set in your Amazon ECS service to an updated, replacement task set in the same Amazon ECS service.
- **EC2/On-Premises**: Traffic is shifted from one set of instances in the original environment to a replacement set of instances.

All AWS Lambda and Amazon ECS deployments are blue/green. An EC2/On-Premises deployment can be in-place or blue/green. A blue/green deployment offers a number of advantages over an in-place deployment:

- You can install and test an application in the new replacement environment and deploy it to production simply by rerouting traffic.
- If you're using the EC2/On-Premises compute platform, switching back to the most recent version of an application is faster and more reliable. That's because traffic can be routed back to the original instances as long as they have not been terminated. With an in-place deployment, versions must be rolled back by redeploying the previous version of the application.
- If you're using the EC2/On-Premises compute platform, new instances are provisioned for a blue/green deployment and reflect the most up-to-date server configurations. This helps you avoid the types of problems that sometimes occur on long-running instances.
- If you're using the AWS Lambda compute platform, you control how traffic is shifted from your original AWS Lambda function version to your new AWS Lambda function version.
- If you're using the Amazon ECS compute platform, you control how traffic is shifted from your original task set to your new task set.

A blue/green deployment with AWS CloudFormation can use one of the following methods:

- **AWS CloudFormation templates for deployments**: When you configure deployments with AWS CloudFormation templates, your deployments are triggered by AWS CloudFormation updates. When you change a resource and upload a template change, a stack update in AWS CloudFormation initiates the new deployment. 
- **Blue/green deployments through AWS CloudFormation**: You can use AWS CloudFormation to manage your blue/green deployments through stack updates. You define both your blue and green resources, in addition to specifying the traffic routing and stabilization settings, within the stack template. Then, if you update selected resources during a stack update, AWS CloudFormation generates all the necessary green resources, shifts the traffic based on the specified traffic routing parameters, and deletes the blue resources.

  

CodePipeline

  

AWS CodePipeline is a continuous delivery service you can use to model, visualize, and automate the steps required to release your software. You can quickly model and configure the different stages of a software release process. CodePipeline automates the steps required to release your software changes continuously.

  

Continuous delivery is a software development methodology where the release process is automated. Every software change is automatically built, tested, and deployed to production. Before the final push to production, a person, an automated test, or a business rule decides when the final push should occur. Although every successful software change can be immediately released to production with continuous delivery, not all changes need to be released right away.

Continuous integration is a software development practice where members of a team use a version control system and frequently integrate their work to the same location, such as a main branch. Each change is built and verified to detect integration errors as quickly as possible. Continuous integration is focused on automatically building and testing code, as compared to _continuous delivery_, which automates the entire software release process up to production.

You can use CodePipeline to help you automatically build, test, and deploy your applications in the cloud. Specifically, you can:

- **Automate your release processes**: CodePipeline fully automates your release process from end to end, starting from your source repository through build, test, and deployment. You can prevent changes from moving through a pipeline by including a manual approval action in any stage except a Source stage. You can release when you want, in the way you want, on the systems of your choice, across one instance or multiple instances.
- **Establish a consistent release process**: Define a consistent set of steps for every code change. CodePipeline runs each stage of your release according to your criteria.
- **Speed up delivery while improving quality**: You can automate your release process to allow your developers to test and release code incrementally and speed up the release of new features to your customers.
- **Use your favorite tools**: You can incorporate your existing source, build, and deployment tools into your pipeline. 
- **View progress at a glance**: You can review real-time status of your pipelines, check the details of any alerts, retry failed stages or actions, view details about the source revisions used in the latest pipeline execution in each stage, and manually rerun any pipeline.
- **View pipeline history details**: You can view details about executions of a pipeline, including start and end times, run duration, and execution IDs.

The following diagram shows an example release process using CodePipeline.

![[Pasted image 20250910154622.png]]


In this example, when developers commit changes to a source repository, CodePipeline automatically detects the changes. Those changes are built, and if any tests are configured, those tests are run. After the tests are complete, the built code is deployed to staging servers for testing. From the staging server, CodePipeline runs more tests, such as integration or load tests. Upon the successful completion of those tests, and after a manual approval action that was added to the pipeline is approved, CodePipeline deploys the tested and approved code to production instances.

CodePipeline can deploy applications to EC2 instances by using CodeDeploy, AWS Elastic Beanstalk, or AWS OpsWorks Stacks. CodePipeline can also deploy container-based applications to services by using Amazon ECS. Developers can also use the integration points provided with CodePipeline to plug in other tools or services, including build services, test providers, or other deployment targets or systems

A _pipeline_ is a workflow construct that describes how software changes go through a release process. Each pipeline is made up of a series of _stages_.

Stages

A stage is a logical unit you can use to isolate an environment and to limit the number of concurrent changes in that environment. Each stage contains actions that are performed on the application artifacts. Your source code is an example of an artifact. A stage might be a build stage, where the source code is built and tests are run. It can also be a deployment stage, where code is deployed to runtime environments. Each stage is made up of a series of serial or parallel _actions_.

Transitions

A _transition_ is the point where a pipeline execution moves to the next stage in the pipeline. You can disable a stage's inbound transition to prevent executions from entering that stage, and then you can enable the transition to allow executions to continue. When more than one execution arrives at a disabled transition, only the latest execution continues to the next stage when the transition is enabled. This means that newer executions continue to supersede waiting executions while the transition is disabled, and then after the transition is enabled, the execution that continues is the superseding execution.

![[Pasted image 20250910154639.png]]

Actions

An _action_ is a set of operations performed on application code and configured so that the actions run in the pipeline at a specified point. This can include things like a source action from a code change, an action for deploying the application to instances, and so on. For example, a deployment stage might contain a deployment action that deploys code to a compute service like Amazon EC2 or AWS Lambda.

Valid CodePipeline action types are source, build, test, deploy, approval, and invoke. 

Pipeline executions

An _execution_ is a set of changes released by a pipeline. Each pipeline execution is unique and has its own ID. An execution corresponds to a set of changes, such as a merged commit or a manual release of the latest commit. Two executions can release the same set of changes at different times.

While a pipeline can process multiple executions at the same time, a pipeline stage processes only one execution at a time. To do this, a stage is locked while it processes an execution. Two pipeline executions can't occupy the same stage at the same time. The execution waiting to enter the occupied stage is referred to an _inbound execution_. An inbound execution can still fail, be superseded, or be manually stopped. 

Pipeline executions traverse pipeline stages in order. Valid statuses for pipelines are InProgress, Stopping, Stopped, Succeeded, Superseded, and Failed.

Stopped executions

The pipeline execution can be stopped manually so that the in-progress pipeline execution does not continue through the pipeline. If stopped manually, a pipeline execution shows a Stopping status until it is completely stopped. Then it shows a Stopped status. A Stopped pipeline execution can be retried.

There are two ways to stop a pipeline execution:

- **Stop and wait**
- **Stop and abandon**

Failed executions

If an execution fails, it stops and does not completely traverse the pipeline. Its status is FAILED status and the stage is unlocked. A more recent execution can catch up and enter the unlocked stage and lock it. You can retry a failed execution unless the failed execution has been superseded or is not retryable. You can roll back a failed stage to a previous successful execution.

Execution modes

To deliver the latest set of changes through a pipeline, newer executions pass and replace less recent executions already running through the pipeline. When this occurs, the older execution is superseded by the newer execution. An execution can be superseded by a more recent execution at a certain point, which is the point between stages. SUPERSEDED is the default execution mode.

In SUPERSEDED mode, if an execution is waiting to enter a locked stage, a more recent execution might catch up and supersede it. The newer execution now waits for the stage to unlock, and the superseded execution stops with a SUPERSEDED status. When a pipeline execution is superseded, the execution is stopped and does not completely traverse the pipeline. You can no longer retry the superseded execution after it has been replaced at this stage. Other available execution modes are PARALLEL or QUEUED mode.

Stage operations

When a pipeline execution runs through a stage, the stage is in the process of completing all of the actions within it. For information about how stage operations work and information about locked stages, see How executions are processed in SUPERSEDED mode.

Valid statuses for stages are InProgress, Stopping, Stopped, Succeeded, and Failed. You can retry a failed stage unless the failed stage is not retryable. For more information, see [StageExecution](https://docs.aws.amazon.com/codepipeline/latest/APIReference/API_StageExecution.html). You can roll back a stage to a specified previous successful execution. A stage can be configured to roll back automatically on failure. 

Action executions

An _action execution_ is the process of completing a configured action that operates on designated artifacts. These can be input artifacts, output artifacts, or both. For example, a build action might run build commands on an input artifact, such as compiling application source code. Action execution details include an action execution ID, the related pipeline execution source trigger, and the input and output artifacts for the action.

Execution types

A pipeline or stage execution can be either a standard or a rolled-back execution.

For standard types, the execution has a unique ID and is a full pipeline run. A pipeline rollback has a stage to be rolled back and a successful execution for the stage as the target execution to which to roll back. The target pipeline execution is used to retrieve source revisions and variables for the stage to rerun.

Action types

_Action types_ are preconfigured actions that are available for selection in CodePipeline. The action type is defined by its owner, provider, version, and category. The action type provides customized parameters that are used to complete the action tasks in a pipeline.

Artifacts

_Artifacts_ refers to the collection of data, such as application source code, built applications, dependencies, definitions files, templates, and so on, that is worked on by pipeline actions. Artifacts are produced by some actions and consumed by others. In a pipeline, artifacts can be the set of files worked on by an action (_input artifacts_) or the updated output of a completed action (_output artifacts_).

Actions pass output to another action for further processing using the pipeline artifact bucket. CodePipeline copies artifacts to the artifact store, where the action picks them up. 

Source revisions

When you make a source code change, a new version is created. A _source revision_ is the version of a source change that triggers a pipeline execution. An execution processes source revisions. For GitHub and CodeCommit repositories, this is the commit. For S3 buckets or actions, this is the object version.

You can start a pipeline execution with a source revision, such as a commit, that you specify. The execution will process the specified revision and override what would have been the revision used for the execution. 

Triggers

_Triggers_ are events that start your pipeline. Some triggers, such as starting a pipeline manually, are available for all source action providers in a pipeline. Certain triggers depend on the source provider for a pipeline. For example, CloudWatch events must be configured with event resources from Amazon CloudWatch that have the pipeline ARN added as a target in the event rule. Amazon CloudWatch Events is the recommended trigger for automatic change detection for pipelines with a CodeCommit or S3 source action. Webhooks are a type of trigger configured for third-party repository events. For example, WebhookV2 is a trigger type that allows Git tags to be used to start pipelines with third-party source providers such as GitHub.com, GitHub Enterprise Server, GitLab.com, GitLab self-managed, or Bitbucket Cloud. In the pipeline configuration, you can specify a filter for triggers, such as push or pull request. You can filter code push events on Git tags, branches, or file paths. You can ﬁlter pull request events on event (opened, updated, closed), branches, or ﬁle paths.

Variables

A _variable_ is a value that can be used to dynamically configure actions in your pipeline. Variables can be either declared on the pipeline level, or emitted by actions in the pipeline. Variable values are resolved at the time of pipeline execution and can be viewed in the execution history. For variables declared at the pipeline level, you can either define default values in the pipeline configuration, or override them for a given execution. For variables emitted by an action, the value is available after an action succesfully completes. 

References : 

**AWS Documentation**

1. CloudTrail Documentation - [https://aws.amazon.com/cloudtrail/](https://aws.amazon.com/cloudtrail/)
2. Storage Gateway Documentation - [https://docs.aws.amazon.com/storagegateway/](https://docs.aws.amazon.com/storagegateway/)
3. CodeCommit Documentation - [https://aws.amazon.com/codecommit/](https://aws.amazon.com/codecommit/)
4. CodeBuild Documentation - [https://aws.amazon.com/codebuild/](https://aws.amazon.com/codebuild/)
5. CodeDeploy documentation - [https://aws.amazon.com/codedeploy/](https://aws.amazon.com/codedeploy/)
6. CodePipeline documentation - [https://aws.amazon.com/codepipeline/](https://aws.amazon.com/codepipeline/)

**Datasheets**

1. CloudTrail - [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/AWS_CloudTrail_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/AWS_CloudTrail_Datasheet.pdf)
2. Storage Gateway - [https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/AWS_Storage_Gateway_Datasheet.pdf](https://d6opu47qoi4ee.cloudfront.net/aws_certification/jit/AWS_Storage_Gateway_Datasheet.pdf)