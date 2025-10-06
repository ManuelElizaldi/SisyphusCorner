----

### Index Card 1: DevOps Philosophy ✅

- **Core Goal**: To deliver applications and services at a high velocity by evolving and improving products faster than organizations using traditional software development models. It aims to prevent silos and foster collaboration between development and IT operations teams.
- **Key Practices**:
    - **CI/CD (Continuous Integration/Continuous Delivery)**: Automates the software release process, from building and testing to deployment.
    - **Microservices**: Breaking down large, monolithic applications into smaller, independent services that can be developed, deployed, and scaled individually.
    - **Shift Left**: A practice of thinking about security, cost optimization, and reliability from day one of development, rather than after deployment.

---

### Index Card 2: Infrastructure as Code (IaC) ✅

- **Concept**: Managing and provisioning infrastructure through machine-readable definition files (code), rather than through manual processes. This makes your infrastructure reusable, maintainable, extensible, and testable.
- **AWS CloudFormation**:
    - A service that helps you model and set up your AWS resources using templates written in JSON or YAML.
    - You define all your resources (like EC2 instances, databases, VPCs) in a **template**, and CloudFormation provisions them as a single unit called a **stack**.
    - It automates provisioning in a safe and controlled manner, with the ability to preview changes (ChangeSets) and roll back automatically if errors occur.
    - You only pay for the resources you create, not for CloudFormation itself.
- **Terraform**: An alternative IaC tool from HashiCorp that is also widely used with AWS.

---

### Index Card 3: The AWS CI/CD Toolchain

- **Purpose**: A suite of AWS services that automates the entire software release workflow, helping developers quickly and reliably deploy code.
- **The Workflow**:
    1. **Source (CodeCommit)**: Store and version control your code in a managed Git repository.
    2. **Build (CodeBuild)**: Compile source code, run tests, and produce a deployable artifact.
    3. **Deploy (CodeDeploy)**: Automate the deployment of the artifact to your target environment (e.g., EC2, ECS, Lambda).
    4. **Orchestrate (CodePipeline)**: Models, visualizes, and automates the entire end-to-end process, connecting the source, build, and deploy stages.

---

### Index Card 4: Containers & Orchestration (Docker & ECS)

- **Containers (Docker)**: A lightweight, standalone unit of software that packages up code and all its dependencies, allowing it to run reliably in any environment. Containers share the host OS kernel, making them faster and more resource-efficient than Virtual Machines (VMs).
- **Amazon Elastic Container Service (ECS)**: A fully managed **container orchestration service** that helps you deploy, manage, and scale containerized applications. It manages clusters of instances and schedules the placement of containers.
- **Key ECS Concepts**:
    - **Task Definition**: A blueprint (in JSON format) that describes the container(s) to run, including the Docker image, CPU/memory requirements, and networking information.
    - **Task**: A running instance of a Task Definition.
    - **Service**: Manages long-running tasks, ensuring a specified number of tasks are always running and handling tasks that fail.
    - **AWS Fargate**: A serverless compute engine for containers, allowing you to run ECS tasks without managing the underlying EC2 instances.

---

### Index Card 5: Serverless Computing & Lambda

- **Concept**: A cloud computing model where the cloud provider dynamically manages the allocation and provisioning of servers. You write and deploy code in small, event-driven units called functions.
- **AWS Lambda**:
    - An **event-driven, serverless compute service** that runs your code in response to triggers.
    - **Triggers** can be from over 200 AWS services, such as an S3 file upload, an API Gateway request, or a message in an SQS queue.
    - You only pay for the compute time you consume; there is no charge when your code is not running.
    - Excellent for use cases like web backends, real-time data processing, and automating operational tasks.

---

### Index Card 6: Monitoring & Auditing

- **AWS CloudWatch**:
    - The primary **observability and monitoring** service.
    - It collects and tracks metrics, collects and stores log files, and sets alarms.
    - You can create dashboards to get a unified view of the health and performance of your AWS resources and applications.
- **AWS CloudTrail**:
    - An **auditing and tracking** service that records user activity and API usage across your AWS account.
    - It answers the questions: "**Who did what, when, and where?**".
    - Crucial for security analysis, compliance audits, and troubleshooting operational issues. It is enabled by default.