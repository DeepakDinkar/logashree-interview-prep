# 🗣️ Vocal — AWS (Explain Out Loud)

> 🟢 basic · 🟡 mid · 🔴 advanced · 🔥 high-frequency · Tags: company that asked.
> Answer each in 2–4 sentences. Definitions: [`../../Definitions/04-AWS-definitions.md`](../../Definitions/04-AWS-definitions.md)

## Fundamentals
1. 🟢🔥 `[GEN]` What is Region vs Availability Zone? Why deploy across AZs?

    Ans: A Region is a geographical area that contains multiple Availability Zones (AZs), which are isolated data centers within that region. Deploying across AZs ensures high availability and fault tolerance, as it allows applications to continue running even if one AZ experiences an outage.

2. 🟢🔥 `[TCS][INFY]` Explain the Shared Responsibility Model.

    Ans: In the Shared Responsibility Model, AWS is responsible for the security of the cloud infrastructure (hardware, software, networking, and facilities), while customers are responsible for securing their data, applications, and configurations within the cloud. This model delineates the responsibilities to ensure both parties maintain a secure environment.

3. 🟡 `[WMT]` Multi-AZ vs Multi-Region — HA vs DR?

    Ans: Multi-AZ deployments provide high availability (HA) by replicating resources across multiple Availability Zones within the same region, ensuring that applications remain operational during an AZ failure. Multi-Region deployments focus on disaster recovery (DR) by replicating resources across different regions, allowing for recovery in case of a regional outage.

4. 🟢 `[CTS]` On-Demand vs Reserved vs Spot instances.

    Ans: On-Demand instances are pay-as-you-go and provide flexibility without long-term commitments. Reserved instances require a one- or three-year commitment, offering significant cost savings for predictable workloads. Spot instances allow users to bid on unused EC2 capacity at reduced prices, ideal for flexible, fault-tolerant workloads.

5. 🟡 `[ACN]` What are the Well-Architected pillars?

    Ans: The Well-Architected Framework consists of five pillars: Operational Excellence (improving processes and procedures), Security (protecting data and systems), Reliability (ensuring workloads perform as expected), Performance Efficiency (using resources efficiently), and Cost Optimization (managing costs effectively).


## IAM 🔥
6. 🟢🔥 `[GEN]` IAM User vs Group vs Role vs Policy.

    Ans: An IAM User represents an individual with specific credentials to access AWS resources. An IAM Group is a collection of users that share the same permissions, making it easier to manage access. An IAM Role is an entity that can be assumed by users or services, granting temporary access to resources without needing long-term credentials. An IAM Policy is a JSON document that defines permissions and can be attached to users, groups, or roles to control access.

7. 🟡🔥 `[AMZN][PP]` What is least privilege? How did you apply it? (your 10+ resources story)

    Ans: Least privilege is a security principle that recommends granting users, applications, or services only the minimum permissions necessary to perform their tasks. For example, if an application needs to read data from an S3 bucket but does not need to write or delete objects, it should be granted a policy that allows only the "s3:GetObject" action on that specific bucket, rather than full access.

8. 🟡🔥 `[WMT]` How do you give an EC2/ECS app access to S3 without keys? (IAM Role)

    Ans: You can give an EC2 or ECS application access to S3 without using access keys by creating an IAM Role with the necessary S3 permissions and attaching it to the EC2 instance or ECS task. The application can then use the temporary credentials provided by the role to access S3 securely.

9. 🔴 `[AMZN]` How does STS / AssumeRole work? Where have you used it? (OIDC)

    Ans: AWS Security Token Service (STS) allows you to request temporary security credentials for IAM users or roles. AssumeRole is an STS API operation that enables a user or service to assume a different role, gaining the permissions associated with that role for a limited time. This is often used in cross-account access scenarios or when integrating with identity providers using OIDC, allowing secure access without sharing long-term credentials.

10. 🟡 `[CAPG]` Managed vs inline policy. What is a permission boundary / SCP?

    Ans: A managed policy is a standalone policy that can be attached to multiple users, groups, or roles, making it easier to manage permissions across accounts. An inline policy is embedded directly into a specific user, group, or role, providing more granular control but less reusability. A permission boundary is an advanced feature that sets the maximum permissions an IAM entity can have, while a Service Control Policy (SCP) is used in AWS Organizations to define the maximum permissions for accounts within the organization.


## VPC / Networking 🔥
11. 🟢🔥 `[GEN]` What is a VPC? Public vs private subnet.

    Ans: A Virtual Private Cloud (VPC) is a logically isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define. Public subnets are subnets that have a route to the internet via an Internet Gateway, allowing resources within them to communicate with the internet. Private subnets do not have direct internet access and are typically used for resources that should not be exposed to the public, such as databases or application servers.

12. 🟡🔥 `[CTS][WMT]` Security Group vs NACL (stateful vs stateless).

    Ans: Security Groups are stateful firewalls that control inbound and outbound traffic at the instance level, meaning that if you allow incoming traffic on a port, the response traffic is automatically allowed. Network Access Control Lists (NACLs) are stateless firewalls that operate at the subnet level, requiring explicit rules for both inbound and outbound traffic, which means you must define rules for both directions.

13. 🟡 `[INFY]` What is a NAT Gateway vs Internet Gateway?

    Ans: An Internet Gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. A NAT Gateway, on the other hand, enables instances in a private subnet to initiate outbound traffic to the internet while preventing inbound traffic from the internet, effectively allowing private instances to access external resources without exposing them directly.

14. 🔴 `[PP]` How does a private subnet reach the internet? When do you use a VPC endpoint?

    Ans: A private subnet can reach the internet by routing its traffic through a NAT Gateway or NAT Instance located in a public subnet, which then forwards the traffic to the Internet Gateway. You would use a VPC endpoint when you want to privately connect your VPC to supported AWS services (like S3 or DynamoDB) without using an Internet Gateway, NAT device, VPN connection, or AWS Direct Connect, ensuring that traffic does not leave the AWS network.

15. 🔴 `[AMZN]` Draw a 3-tier VPC across 2 AZs.

    Ans: A 3-tier VPC architecture typically consists of three layers: the presentation layer (web servers), the application layer (application servers), and the data layer (databases). In a multi-AZ setup, you would have two Availability Zones, each containing a public subnet for the web servers, a private subnet for the application servers, and another private subnet for the databases. The web servers in the public subnets can communicate with the application servers in the private subnets, which in turn can access the databases in their respective private subnets. Load balancers can be placed in front of the web servers to distribute traffic across both AZs.


## Compute
16. 🟡🔥 `[WMT]` ECS EC2 launch type vs Fargate — when each?

    Ans: The ECS EC2 launch type allows you to run containers on a cluster of EC2 instances that you manage, giving you more control over the underlying infrastructure and the ability to use custom AMIs. Fargate, on the other hand, is a serverless compute engine for containers that abstracts away the underlying infrastructure, allowing you to focus solely on defining and running your containers without managing servers. Use EC2 launch type when you need more control or have specific requirements for the host environment, and use Fargate for simplicity and reduced operational overhead.

17. 🟡 `[CTS]` EC2 vs ECS vs Lambda — when VM vs container vs serverless?

    Ans: EC2 is suitable for running traditional virtual machines where you need full control over the operating system and environment. ECS is ideal for containerized applications that require orchestration, scaling, and management of multiple containers. Lambda is best for serverless applications where you want to run code in response to events without managing servers, making it suitable for lightweight, event-driven workloads.

18. 🟡🔥 `[WMT][PP]` How does an Auto Scaling Group self-heal and scale?

    Ans: An Auto Scaling Group (ASG) monitors the health of its instances and automatically replaces any that are deemed unhealthy, ensuring that the desired number of instances is maintained. It can also scale out (add instances) or scale in (remove instances) based on defined policies, such as CPU utilization or custom CloudWatch metrics, allowing the application to handle varying levels of traffic efficiently.

19. 🟡 `[HEXA]` What is a task definition vs a service in ECS?

    Ans: A task definition in ECS is a blueprint that describes how a container should run, including the Docker image, CPU and memory requirements, networking mode, and other configurations. A service, on the other hand, is responsible for running and maintaining a specified number of instances of a task definition, ensuring that the desired count of tasks is always running and handling load balancing if configured.

20. 🟢 `[TCS]` What is ECR and why use it?

    Ans: Amazon Elastic Container Registry (ECR) is a fully managed Docker container registry that makes it easy to store, manage, and deploy Docker container images. It integrates seamlessly with ECS and other AWS services, providing secure, scalable, and reliable storage for container images, along with features like image scanning for vulnerabilities and lifecycle policies for managing image versions.

## LB / DNS / CDN
21. 🟡🔥 `[WMT]` ALB (L7) vs NLB (L4) — when each?

    Ans: An Application Load Balancer (ALB) operates at Layer 7 (the application layer) and is ideal for routing HTTP/HTTPS traffic based on content, such as URL paths or host headers. It supports advanced features like SSL termination, WebSocket support, and integration with AWS WAF. A Network Load Balancer (NLB) operates at Layer 4 (the transport layer) and is designed for high-performance, low-latency traffic routing, making it suitable for TCP/UDP traffic and applications that require extreme performance and static IP addresses. Use ALB for web applications and NLB for high-throughput or latency-sensitive applications.

22. 🟡 `[CMCST]` What is a target group + health check?

    Ans: A target group is a collection of resources (such as EC2 instances, IP addresses, or Lambda functions) that a load balancer routes traffic to. Each target group has its own health check configuration, which periodically checks the health of the targets by sending requests to a specified endpoint. If a target fails the health check, it is marked as unhealthy and will not receive traffic until it passes the health check again.

23. 🟡🔥 `[PP]` What is CloudFront? How do you secure S3 behind it? (OAC)

    
    Ans: Amazon CloudFront is a content delivery network (CDN) that distributes content globally with low latency and high transfer speeds by caching copies of your content at edge locations. To secure an S3 bucket behind CloudFront, you can use an Origin Access Control (OAC) to restrict direct access to the S3 bucket, ensuring that only CloudFront can access the content. Additionally, you can configure signed URLs or signed cookies to control access to specific content.

24. 🟡 `[ACN]` Route 53 routing policies (weighted, latency, failover).

    Ans: Route 53 offers several routing policies to control how traffic is directed to your resources. Weighted routing allows you to distribute traffic across multiple resources based on assigned weights, enabling gradual rollouts or A/B testing. Latency-based routing directs traffic to the resource with the lowest latency for the user, improving performance. Failover routing automatically redirects traffic to a healthy resource if the primary resource becomes unavailable, ensuring high availability.

## Storage & DB
25. 🟢🔥 `[GEN]` S3 storage classes and lifecycle rules.

    Ans: Amazon S3 offers various storage classes to optimize cost and performance based on access patterns. These include Standard (frequent access), Intelligent-Tiering (automatic cost optimization), Standard-IA (infrequent access), One Zone-IA (lower-cost, single AZ), Glacier (archival), and Glacier Deep Archive (long-term archival). Lifecycle rules allow you to automate the transition of objects between storage classes or delete them after a specified period, helping manage costs and data retention policies.

26. 🟡 `[INFY]` How do you secure an S3 bucket? (Block Public Access, SSE, policy)

    
    Ans: To secure an S3 bucket, you can enable Block Public Access settings to prevent public access to the bucket and its objects. You can also use Server-Side Encryption (SSE) to encrypt data at rest, either with AWS-managed keys (SSE-S3), KMS-managed keys (SSE-KMS), or customer-provided keys (SSE-C). Additionally, you can create bucket policies or IAM policies to control access permissions, ensuring that only authorized users or roles can access the bucket and its contents.

27. 🟡 `[CTS]` EBS vs EFS vs S3.

    Ans: Amazon EBS (Elastic Block Store) provides block-level storage for EC2 instances, suitable for applications that require low-latency access to data, such as databases. Amazon EFS (Elastic File System) offers scalable, shared file storage that can be mounted by multiple EC2 instances, making it ideal for workloads that require concurrent access to a file system. Amazon S3 (Simple Storage Service) is an object storage service designed for storing and retrieving any amount of data from anywhere on the web, suitable for static content, backups, and archival.

28. 🟡🔥 `[WMT]` RDS Multi-AZ vs Read Replica.

    Ans: RDS Multi-AZ deployments provide high availability and failover support by automatically replicating data to a standby instance in a different Availability Zone. In the event of a failure, the standby instance is promoted to primary, minimizing downtime. Read Replicas, on the other hand, are used to offload read traffic from the primary database by creating one or more read-only copies of the database, which can be used for scaling read-heavy workloads and improving performance.

29. 🟡 `[PP]` When RDS vs DynamoDB?

    Ans: Use RDS when you need a relational database with support for SQL queries, transactions, and complex relationships between data. It is suitable for applications that require structured data and ACID compliance. DynamoDB is a NoSQL database that provides fast and predictable performance with seamless scalability, making it ideal for applications that require flexible schema design, high throughput, and low-latency access to unstructured or semi-structured data.

30. 🟡 `[CMCST]` What is a presigned URL?

    Ans: A presigned URL is a URL that grants temporary access to a specific S3 object without requiring AWS credentials. It is generated using the AWS SDK or CLI and includes an expiration time, after which the URL becomes invalid. Presigned URLs are commonly used for securely sharing private S3 objects with users or applications without exposing sensitive credentials.

## Messaging
31. 🟡 `[WMT]` SQS vs SNS. How do CloudWatch alarms notify via SNS?

    Ans: Amazon SQS (Simple Queue Service) is a fully managed message queuing service that enables decoupling of components in a distributed system, allowing messages to be stored and processed asynchronously. Amazon SNS (Simple Notification Service) is a fully managed pub/sub messaging service that allows you to send messages to multiple subscribers or endpoints simultaneously. CloudWatch alarms can notify via SNS by configuring the alarm to publish a message to an SNS topic when the alarm state changes, which then sends notifications to all subscribed endpoints (e.g., email, SMS, Lambda functions).

---
### ⭐ Your resume lines to rehearse
- "Provisioned VPC/ECS/CloudFront/S3 with Terraform, −70% effort" → walk the architecture.
- "IAM least-privilege across 10+ resources" → give a concrete policy example.
- "Migrated Render→AWS, −35% cost" → how (right-sizing, autoscale).
