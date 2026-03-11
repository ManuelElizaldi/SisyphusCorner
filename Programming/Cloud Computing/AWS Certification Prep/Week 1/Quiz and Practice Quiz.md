[[AWS]]

## Practice Quiz
# AWS Solutions Architect – Study Guide

A focused review of key AWS concepts, presented as exam-style questions with detailed explanations. Use this to test yourself and reinforce your understanding of core services.

---

## 1. S3 Upload Limits

**Scenario:** An application running on EC2 encounters a failure when attempting to upload an 8 GB file to S3. What could be causing this problem, and how can it be resolved?

**Answer:** With a single PUT operation, you can upload an object up to **5 GB** in size. Since the file is 8 GB, the upload exceeds this threshold and fails. The solution is to use S3's **multipart upload** feature, which breaks the file into smaller parts, uploads them independently (and in parallel), and then reassembles them on the S3 side. Multipart upload supports objects up to **5 TB**.

**Key Takeaway:** Always remember the 5 GB single PUT limit. For anything larger, multipart upload is required — not optional. This has nothing to do with EBS performance, NAT gateways, or VPC endpoints.

---

## 2. Internet Gateway and VPC Relationship

**Scenario:** Is it possible to attach more than one Internet Gateway to a VPC? Can you attach multiple VPCs to a single Internet Gateway?

**Answer: False.** The relationship between an Internet Gateway and a VPC is strictly **one-to-one**. You cannot attach more than one Internet Gateway to a single VPC, and you cannot attach a single Internet Gateway to multiple VPCs. This is a hard architectural constraint in AWS.

**Key Takeaway:** One VPC = One Internet Gateway. No exceptions.

---

## 3. S3 Storage Class Selection

**Scenario:** An organization is developing web and mobile applications that upload 100,000 images daily to S3. They anticipate volume spikes but are budget-constrained. What information should you gather to determine if S3 is suitable?

**Answer:** Gather information on the **high availability requirements** and **frequency of access requests** to choose the appropriate S3 storage class. The primary cost driver in S3 is the storage class you select. For example, if most images are rarely accessed after upload, **S3 Standard-IA** or **S3 Intelligent-Tiering** could significantly reduce costs compared to S3 Standard. Understanding access patterns is essential for a cost-effective design.

**Why not the other options?**

- S3 automatically handles high request rates across prefixes (no need to manually design key namespaces since 2018).
- S3 is a fully managed, virtually unlimited object store — you don't "provision" storage.
- S3 natively scales to handle massive request volumes without special configuration.

**Key Takeaway:** For cost optimization questions on the exam, think about storage classes first. Know the differences between Standard, Standard-IA, One Zone-IA, Glacier, Glacier Deep Archive, and Intelligent-Tiering.

---

## 4. EC2 Storage for Database Workloads

**Scenario:** Your application requires a backend database and you need to provision an EC2 instance with appropriate storage. Which storage option is the best fit?

**Answer: Elastic Block Storage (EBS).** EBS is ideal for database workloads because it provides persistent, low-latency block-level storage. You can provision specific IOPS levels (io1/io2) to meet demanding database performance requirements, and EBS supports point-in-time snapshots for backups. EBS volumes persist independently of the EC2 instance lifecycle.

**Why not the other options?**

- **EFS** is a managed NFS file system for shared access — databases need block storage, not network file storage.
- **S3** is object storage. You cannot mount it as a disk volume and run a database engine on it.
- **Instance Storage** is ephemeral — all data is lost when the instance stops or terminates. Unacceptable for database durability.

**Key Takeaway:** Databases = block storage = EBS. Know the difference between block storage (EBS), file storage (EFS), and object storage (S3).

---

## 5. Exposing ECS Applications to the Internet

**Scenario:** A company has a web application running on ECS and needs to make it available to customers over the internet. What is your recommendation?

**Answer: Use Elastic Load Balancing (ELB).** Specifically, an Application Load Balancer (ALB) integrates directly with ECS services through dynamic port mapping and target groups. It distributes traffic across multiple ECS tasks, performs health checks, and automatically registers/deregisters containers as ECS scales.

**Why not the other options?**

- **API Gateway** is designed for REST/WebSocket APIs, best suited for serverless architectures with Lambda — not for fronting a full web application on ECS.
- **CloudFront** is a CDN for caching static content at edge locations. It can complement an ELB but cannot replace it for routing traffic to ECS containers.
- **Elastic IP on EC2** ties traffic to a single instance, provides no load balancing, and defeats the purpose of running containers on ECS.

**Key Takeaway:** ECS + internet-facing = ALB. The exam loves testing the distinction between API Gateway (APIs/serverless) and ELB (web apps/containers).

---

## 6. Reducing Network Latency with Placement Groups

**Scenario:** A distributed system requiring very low network latency needs to be deployed. EC2 instances are sufficiently sized, but you are concerned about network bandwidth. What should you do?

**Answer: Use Placement Groups.** Specifically, a **Cluster Placement Group** places EC2 instances physically close together within a single Availability Zone, providing low latency and high throughput (up to 10 Gbps, or 25 Gbps with enhanced networking).

**Why not the other options?**

- **Increasing instance size** doesn't guarantee low latency between instances and wastes money if compute is already sufficient.
- **Dedicated Hosts** provide a physical server for licensing/compliance — they do nothing for network latency.
- **Co-locating in a region** doesn't ensure physical proximity. Instances can still span multiple AZs and data centers.

**Key Takeaway:** Know the three placement group strategies: **Cluster** (low latency, single AZ), **Spread** (high availability, instances on separate hardware), and **Partition** (large distributed workloads like HDFS/Cassandra). The exam frequently tests when to use each.

---

## 7. VPC CIDR Block Prefix Lengths

**Scenario:** What is the permitted set of IPv4 prefix lengths for a VPC CIDR block?

**Answer: /16 to /28.**

- **/16** is the largest allowed (65,536 IP addresses).
- **/28** is the smallest allowed (16 IP addresses).

AWS also requires that the CIDR block come from the RFC 1918 private address ranges (10.0.0.0/8, 172.16.0.0/12, or 192.168.0.0/16), though non-RFC 1918 ranges are technically permitted.

**Key Takeaway:** Memorize /16 to /28 for VPC IPv4. Also remember that /56 is relevant to IPv6, where AWS assigns a /56 block to a VPC.

---

## 8. ECS Placement Strategies

**Scenario:** A company uses ECS with EC2 launch type and wants to ensure all EC2 instances are utilized to the maximum. Which placement strategy is most appropriate?

**Answer: Binpack.** The binpack strategy places tasks on instances with the least available remaining CPU or memory, filling up each instance before moving to the next. This maximizes resource utilization and minimizes the number of running instances.

**Why not the other options?**

- **Random** distributes tasks with no resource consideration, leading to uneven utilization.
- **Spread** distributes tasks evenly across distinct hardware for fault tolerance — the opposite of maximizing utilization.
- **Max** is not a valid ECS placement strategy.

**Key Takeaway:** Know the three valid ECS strategies: **binpack** (maximize utilization), **spread** (maximize availability), and **random** (no optimization). Binpack = cost savings. Spread = fault tolerance.

---

## 9. Cross-Business Unit Data Exchange

**Scenario:** An organization with multiple business units running legacy applications in different languages needs a service for data exchange to achieve cross-business-unit workflows. Which AWS service is best suited?

**Answer: SQS (Simple Queue Service).** SQS is accessed via REST APIs, making it language-agnostic. It decouples producer and consumer applications, persists messages until processed, and requires minimal changes to legacy applications.

**Why not the other options?**

- **Kinesis** is designed for real-time data streaming (logs, clickstreams, IoT) — overkill for simple workflow data exchange.
- **SNS** is pub/sub notification service that doesn't retain messages if a subscriber is unavailable.
- **Kafka (Amazon MSK)** introduces significant operational complexity that isn't warranted for basic cross-team data exchange.

**Key Takeaway:** SQS = decoupled, reliable, simple message exchange. SNS = fan-out notifications. Kinesis = real-time streaming. Know when to use each.

---

## 10. Reducing Global Latency with CloudFront

**Scenario:** Your globally popular application is responding slowly for some users but not others. The application itself is fine. Which service will reduce transfer latency?

**Answer: CloudFront.** CloudFront is AWS's CDN with 400+ edge locations worldwide. It caches content close to users, so requests don't need to travel back to the origin server. The fact that only some users complain strongly suggests a geographic latency issue — users far from the origin experience slow responses while nearby users do not.

**Why not the other options?**

- **Route 53** is a DNS service. Latency-based routing helps direct users to the nearest region, but DNS resolution is a tiny fraction of response time.
- **Load Balancer** distributes traffic within a single region — it doesn't help distant users.
- **S3** serves from a single region. Without CloudFront in front of it, distant users still experience high latency.

**Key Takeaway:** "Some users slow, others fine" + global audience = CloudFront. The exam often presents this pattern to test CDN knowledge.

---

## Quick Reference Table

|Topic|Key Number / Fact|
|---|---|
|S3 single PUT limit|5 GB|
|S3 multipart upload limit|5 TB|
|S3 single object max size|5 TB|
|VPC CIDR range (IPv4)|/16 to /28|
|VPC IPv6 CIDR|/56 (assigned by AWS)|
|Internet Gateway : VPC|1 : 1|
|ECS placement – max utilization|Binpack|
|ECS placement – max availability|Spread|
|Cluster Placement Group bandwidth|Up to 10–25 Gbps|
|Database on EC2 storage|EBS (persistent block storage)|
|Global latency reduction|CloudFront|
|Decoupled messaging|SQS|
|Internet-facing ECS|Application Load Balancer|
## Quiz
# AWS Solutions Architect – Study Guide (Part 2)

A focused review of key AWS concepts, presented as exam-style questions with detailed explanations. Use this to test yourself and reinforce your understanding of core services.

---

## 1. MAC Address Persistence on EC2

**Scenario:** Your application is MAC address dependent per its licensing terms. How can you ensure the MAC address remains the same when deploying to AWS on an r4.2xlarge instance?

**Answer:** Use a VPC with an **Elastic Network Interface (ENI)** that has a fixed MAC address. Each ENI is assigned a MAC address at creation, and that address persists for the lifetime of the ENI — even if you detach it from one instance and reattach it to another.

**Why not the other options?**

- AWS does not allow you to manually assign a custom MAC address to an EC2 instance.
- A private subnet doesn't guarantee MAC persistence across instance replacements.
- There is no mechanism to bind a MAC address to a subnet.

**Key Takeaway:** When the exam mentions MAC-dependent licensing, the answer is always **ENI**. Remember that ENIs carry three persistent attributes: MAC address, private IP address, and Elastic IP (if associated). ENIs can be moved between instances, making them the go-to solution for license portability.

---

## 2. ECS Capacity Provider Components

**Scenario:** For ECS workloads hosted on EC2 instances, what components must a capacity provider consist of?

**Answer: All of the following:**

- **Name** — A unique identifier for the capacity provider.
- **An Auto Scaling Group (ASG)** — Manages the pool of EC2 instances providing compute capacity. Each capacity provider maps to exactly one ASG, and each ASG can only be associated with one capacity provider.
- **Settings for managed scaling and managed termination protection** — Managed scaling allows ECS to automatically scale the ASG based on task demand. Managed termination protection prevents the ASG from terminating instances still running tasks during scale-in events.

**Key Takeaway:** Capacity providers bridge ECS task placement and EC2 Auto Scaling. Fargate has its own built-in providers (`FARGATE` and `FARGATE_SPOT`) that don't require any of these components.

---

## 3. S3 Bucket URL Formats

**Scenario:** You create a bucket named "myorgtraildata" in US West. Which URLs are valid for accessing the bucket?

**Answer (select 2):**

- `https://myorgtraildata.s3.us-west-1.amazonaws.com` — **Virtual-hosted style** (preferred). Bucket name as subdomain.
- `https://s3.us-west-1.amazonaws.com/myorgtraildata` — **Path-style** (legacy). Bucket name in the URL path.

**Why not the others?**

- `https://s3.myorgtraildata.us-west-1.amazonaws.com` — Bucket name placed between `s3` and the region is not a valid structure.
- `https://s3.amazonaws.com/myorgtraildata` — Uses the global endpoint without a region. Not valid for non-us-east-1 buckets.

**Key Takeaway:** Memorize the two formats:

|Style|Format|
|---|---|
|Virtual-hosted (preferred)|`https://<bucket>.s3.<region>.amazonaws.com`|
|Path-style (legacy)|`https://s3.<region>.amazonaws.com/<bucket>`|

---

## 4. ECS Container Agent Communication Failure

**Scenario:** An ECS cluster has 10 EC2 instances with container agents installed, but ECS is not receiving operating data from the agents. What could be causing this?

**Answer (select 2):**

- **IAM role used to run the ECS instance does not have `ecs:Poll` action in its policy.** The container agent needs specific ECS permissions to communicate with the ECS service. Without the `ecs:Poll` action, the agent cannot poll for task updates or report data back to ECS.
- **Interface VPC endpoint is not configured for the ECS service.** If the EC2 instances are in a private subnet with no internet access (no NAT gateway or Internet Gateway), they need an Interface VPC endpoint for the ECS service to communicate with it. Without this endpoint, the agent has no route to reach the ECS service.

**Key Takeaway:** ECS agent communication requires both proper **IAM permissions** and **network connectivity** to the ECS service endpoint. In private subnets, you need either a NAT gateway/Internet Gateway for public access or Interface VPC endpoints for private access. The required VPC endpoints for ECS are `com.amazonaws.<region>.ecs`, `com.amazonaws.<region>.ecs-agent`, and `com.amazonaws.<region>.ecs-telemetry`.

---

## 5. ECS Placement Strategies

**Scenario:** A company using ECS with EC2 launch type wants to ensure all EC2 instances are utilized to the maximum. Which placement strategy is most appropriate?

**Answer: Binpack.** It places tasks on instances with the least available remaining CPU or memory, filling each instance before moving to the next.

**Key Takeaway:** The three valid ECS placement strategies:

|Strategy|Purpose|
|---|---|
|**Binpack**|Maximize utilization, reduce costs|
|**Spread**|Maximize availability, fault tolerance|
|**Random**|No optimization|

---

## 6. Handling Disk Space Running Out on EC2

**Scenario:** Your application allows file uploads and disk space is running out due to higher-than-expected demand. What is the easiest approach without complex migration?

**Answer:** Increase the size of the existing EBS volume. AWS allows you to **modify an EBS volume while it's still attached and in use** — no downtime required. After increasing the volume size in AWS, extend the filesystem at the OS level.

**Why not the other options?**

- Attaching multiple volumes requires managing multiple mount points and reconfiguring the application — too complex.
- Moving to a network file store (EFS) requires data migration and architecture changes.
- Storing uploaded files in a database is an anti-pattern requiring significant code changes.

**Key Takeaway:** EBS volumes are elastic — you can increase their size on the fly. Remember the two-step process: (1) modify the volume in AWS, (2) extend the filesystem using tools like `growpart` and `resize2fs`. You can only **increase** size, never decrease it.

---

## 7. Secure EC2 Access to AWS Resources

**Scenario:** An application on EC2 needs to access S3 and DynamoDB. What is the most secure approach?

**Answer:** Assign an **IAM role** with the desired policies to the EC2 instance. AWS automatically provides and rotates temporary security credentials through the instance metadata service — no hardcoded secrets needed.

**Why not the other options?**

- Embedding access keys in code is the worst approach — credentials can leak through version control, logs, or decompilation.
- Storing credentials via AWS CLI on the instance means long-lived secrets on disk.
- The launching IAM user's permissions don't transfer to the EC2 instance.

**Key Takeaway:** The answer is **always IAM roles** when an AWS resource needs to access another AWS resource. Key advantages: no long-lived credentials, automatic rotation, credentials never stored on disk, permissions can be changed instantly by updating the role's policies.

---

## 8. S3 Durability Guarantees

**Scenario:** Which potential threats are safeguarded by S3 data durability guarantees?

**Answer (select 2):**

- **Infrastructure failure** — Hardware failures, server crashes, or storage rack outages. Data survives because copies exist across multiple AZs.
- **Data center security breach** — Physical compromise of a single facility. Data still exists in other Availability Zones.

**Not covered by durability:**

- **User misconfiguration** — Accidental deletions are valid API operations. Use versioning, MFA Delete, and Object Lock for protection.
- **Account security breach** — Compromised credentials leading to deletion. Address with IAM policies, MFA, and access controls.

**Key Takeaway:** Durability protects against infrastructure/physical failures. Security features (versioning, MFA Delete, IAM) protect against human error and unauthorized access. Know the difference.

---

## 9. VPC Endpoint Routing Precedence Over NAT Gateway

**Scenario:** You created a VPC endpoint and a NAT gateway route for S3 access, but S3 logs show traffic isn't going through the NAT gateway. What's the cause?

**Answer:** The request was **redirected through the VPC endpoint**. When both a NAT gateway route and a VPC endpoint exist on the same route table, AWS always prioritizes the VPC endpoint for traffic destined to the supported service (most specific route wins).

**Key Takeaway:** VPC endpoints always take precedence over NAT gateways and Internet Gateways for traffic to the associated service. Also remember:

|Endpoint Type|Services|Cost|Mechanism|
|---|---|---|---|
|**Gateway Endpoint**|S3, DynamoDB|Free|Route table entry|
|**Interface Endpoint**|Most other services|Per hour + per GB|PrivateLink / ENI|

---

## 10. ECS Task Definition Parameters

**Scenario:** Which of the following are parameters specified in task definitions?

**Answer (select 3):**

- The **Docker images** to use with the containers
- How much **CPU and memory** to use with each container
- The **command** the container should run when it starts

**Not task definition parameters:**

- **EC2 instance types** — Determined when launching instances into the cluster or configuring the ASG.
- **VPC and subnets** — Specified at the service level or in the `RunTask` API call.

**Key Takeaway:** A task definition is a blueprint for your containers ("what should run and how"), not your infrastructure ("where should it run"). It covers image, resources, commands, environment variables, logging, and volumes.

---

## 11. ECS Fargate Capacity Providers

**Scenario:** For ECS workloads hosted on Fargate, which predefined capacity providers are available?

**Answer (select 2):**

- **FARGATE** — Standard on-demand compute.
- **FARGATE_SPOT** — Runs on spare capacity at up to 70% discount, with a two-minute interruption warning.

**Not valid:** Fargate Reserved and Fargate Dynamic do not exist. For Fargate cost optimization, use Fargate Spot or Compute Savings Plans.

---

## 12. Investigating S3 Access from Unknown IPs

**Scenario:** An S3 bucket is restricted to certain IAM users within your organization's IP range, but suspicious requests from other IPs are suspected. How do you find the requester's IP?

**Answer (select 2):**

- **Server Access Logging** — Captures per-request details including requester IP, object accessed, timestamp, and HTTP status. Purpose-built for S3 access auditing.
- **CloudTrail Logging** (with object-level/data events enabled) — Records the `sourceIPAddress` in every event along with IAM identity and operation performed.

**Not useful:**

- **VPC Flow Logs** — Operate at the network layer within your VPC; don't capture S3 request-level details.
- **CloudWatch Metrics** — Only provides aggregate statistics, not individual requester IPs.

---

## 13. Secondary VPC CIDR Blocks

**Scenario:** A VPC has a primary CIDR of 192.168.16.0/24. Which secondary CIDR can be added?

**Answer: 192.168.0.0/24** — Range 192.168.0.0–192.168.0.255. Does not overlap with the primary.

**Why not the others?**

- **172.31.0.0/16** — Restricted due to association with the default VPC.
- **192.168.0.0/16** — Completely contains the primary CIDR (overlap).
- **192.168.16.0/23** — Encompasses the primary CIDR as a superset (overlap).

**Key Takeaway:** Secondary CIDRs must never overlap with existing CIDRs. Always expand CIDR notation into the full IP range and check for any intersection.

---

## 14. Subnet and Availability Zone Relationship

**Scenario:** What is the relationship between a subnet and an Availability Zone?

**Answer:** An Availability Zone can have **multiple subnets**, but a subnet is always confined to **exactly one** Availability Zone.

**Key Takeaway:** The relationship is one-to-many in one direction only. A common architecture pattern is at least two subnets per AZ (one public, one private) across at least two AZs for high availability.

---

## 15. InvalidAMIID.NotFound Error

**Scenario:** A cloud automation script errors out with "InvalidAMIID.NotFound". What is the likely cause?

**Answer:** The **region code is incorrect**. AMIs are region-specific resources. An AMI ID valid in `us-east-1` does not exist in `us-west-2`.

**Key Takeaway:** `InvalidAMIID.NotFound` = wrong region. If you need the same AMI across regions, you must explicitly **copy the AMI** to each target region, which generates a new AMI ID per region.

---

## 16. S3 Bucket Properties

**Scenario:** Which of the following are S3 bucket properties?

**Answer (select 2):**

- **Server Access Logging** — Configured and applied at the bucket level.
- **Object Level Logging** — Configured at the bucket level through CloudTrail.

**Not bucket properties:**

- **Storage Class** — Object-level property. Different objects in the same bucket can have different storage classes.
- **Metadata** — Object-level property. Each object has its own system and user-defined metadata.

**Key Takeaway:** Know the distinction between bucket-level properties (logging, versioning, encryption defaults, transfer acceleration) and object-level properties (storage class, metadata, tags).

---

## 17. Pre-signed URL Access Failures

**Scenario:** Pre-signed URLs generated using EC2 role temporary credentials are failing for users. What could be the cause?

**Answer (select 2):**

- **Pre-signed URLs expired** — URLs have a set expiration time. Additionally, URLs generated with temporary credentials become invalid when those credentials expire, regardless of the URL's own expiration setting.
- **Bucket has a deny policy, EC2 role not whitelisted** — An explicit deny in a bucket policy always overrides allow permissions. Pre-signed URLs inherit the signer's permissions, so a deny policy blocks access even though the role has GetObject.

**Not correct:**

- Users do **not** need to be IAM users — the whole point of pre-signed URLs is granting access to anyone.
- There is no separate "default policy" on temporary credentials that strips permissions.

**Key Takeaway:** Pre-signed URL failures come down to **expiration** and **explicit deny policies**. A pre-signed URL can never grant more access than the identity that created it.

---

## 18. Configuring a NAT Instance

**Scenario:** What must you do to configure a NAT instance after creating it?

**Answer:** **Disable the source/destination check** on its ENI. By default, EC2 instances verify they are the source or destination of traffic. A NAT instance forwards traffic on behalf of others, so this check must be turned off.

**Key Takeaway:** This concept applies to any EC2 instance acting as a network appliance (firewalls, proxies, load balancers). NAT **gateways** are AWS-managed and don't require this step.

---

## 19. Dedicated Tenancy for Compliance

**Scenario:** A corporate governance policy disallows co-hosting or co-locating applications with any other organization. Which launch configuration should be selected?

**Answer: Dedicated Tenancy.** This is a VPC-level setting that ensures every instance in the VPC runs on hardware physically isolated from other AWS customers.

**Key Takeaway:** Know the hierarchy:

|Option|Scope|Primary Use|
|---|---|---|
|**Dedicated Tenancy**|VPC-level|Blanket compliance / governance isolation|
|**Dedicated Instance**|Instance-level|Same isolation, but per-instance (risk of gaps)|
|**Dedicated Host**|Physical server|BYOL licensing with socket/core visibility|

For governance and compliance questions requiring blanket isolation, dedicated tenancy is the safest answer.

---

## Quick Reference Table — Part 2

| Topic                        | Key Fact                                     |
| ---------------------------- | -------------------------------------------- |
| MAC address persistence      | Elastic Network Interface (ENI)              |
| S3 URL — virtual-hosted      | `https://<bucket>.s3.<region>.amazonaws.com` |
| S3 URL — path-style          | `https://s3.<region>.amazonaws.com/<bucket>` |
| ECS agent needs              | IAM permissions + network connectivity       |
| EBS volume resize            | Can increase on the fly, never decrease      |
| EC2 accessing other services | Always use IAM roles                         |
| S3 durability covers         | Infrastructure failure + data center breach  |
| S3 durability does NOT cover | User error + account compromise              |
| VPC endpoint vs NAT gateway  | VPC endpoint always takes precedence         |
| Subnet : AZ relationship     | Many subnets per AZ, one AZ per subnet       |
| InvalidAMIID.NotFound        | Wrong region                                 |
| Pre-signed URL failures      | Expiration + explicit deny policies          |
| NAT instance config          | Disable source/destination check             |
| Co-hosting compliance        | Dedicated tenancy (VPC-level)                |
| Fargate capacity providers   | FARGATE + FARGATE_SPOT                       |