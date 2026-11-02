# 🧠 Rapid-Fire — 200 Quick Q&A (One-Liners)

> Machine-gun round prep. Read question → answer in one breath → check. These are the "quick definition" questions interviewers fire to test breadth. Answers are terse on purpose.

🔥 = very common

---

## AWS (1–50)
1. 🔥 Region vs AZ? — Geographic area vs isolated datacenter within it.

    Ans: Region is a geographic area that contains multiple Availability Zones (AZs). An AZ is an isolated data center within a region, designed for high availability and fault tolerance.

2. What is an Edge Location? — CloudFront cache point of presence.

    Ans: An Edge Location is a data center that is part of the Amazon CloudFront content delivery network (CDN). It is used to cache copies of content closer to end users, reducing latency and improving performance.

3. 🔥 EC2 instance types? — General, Compute, Memory, Storage, GPU optimized.

    Ans: EC2 instance types are categorized based on their intended use case. General-purpose instances provide a balance of compute, memory, and networking resources. Compute-optimized instances are designed for compute-intensive tasks. Memory-optimized instances are ideal for memory-intensive applications. Storage-optimized instances offer high I/O performance for large datasets. GPU-optimized instances are tailored for graphics-intensive and machine learning workloads.

4. What is an AMI? — Image template to launch EC2.

    Ans: An Amazon Machine Image (AMI) is a pre-configured template that contains the operating system, application server, and applications required to launch an EC2 instance. It serves as a blueprint for creating new instances.

5. Spot vs On-Demand vs Reserved? — Cheap/interruptible vs flexible vs committed.

    Ans: Spot instances are the cheapest option but can be interrupted by AWS with little notice. On-Demand instances provide flexibility and are billed by the hour or second, with no long-term commitment. Reserved instances require a commitment to use for a one- or three-year term, offering significant cost savings compared to On-Demand pricing.

6. 🔥 S3 durability? — 11 nines (99.999999999%).

    Ans: Amazon S3 is designed for 99.999999999% (11 nines) durability, meaning that it is highly unlikely that data stored in S3 will be lost. This is achieved through automatic replication of data across multiple devices and facilities within a region.

7. S3 vs EBS vs EFS? — Object vs block (1 EC2) vs shared file (many).

    Ans: S3 is an object storage service suitable for storing and retrieving any amount of data from anywhere on the web. EBS (Elastic Block Store) provides block-level storage volumes for use with EC2 instances, typically used for a single instance. EFS (Elastic File System) is a scalable file storage service that can be mounted by multiple EC2 instances, allowing shared access to files.

8. 🔥 SG vs NACL? — Stateful instance-level vs stateless subnet-level.

    Ans: Security Groups (SG) are stateful, meaning that if an incoming request is allowed, the response is automatically allowed. They operate at the instance level and control inbound and outbound traffic. Network Access Control Lists (NACLs) are stateless, meaning that they evaluate each request independently. They operate at the subnet level and provide an additional layer of security by allowing or denying traffic based on rules.

9. Public vs private subnet? — Has route to IGW vs not.

    Ans: A public subnet has a route to an Internet Gateway (IGW), allowing instances within it to communicate with the internet. A private subnet does not have a direct route to the IGW, meaning that instances within it cannot directly access the internet and typically rely on a NAT Gateway or NAT instance for outbound internet access.

10. NAT Gateway purpose? — Outbound internet for private subnets.

    Ans: A NAT Gateway allows instances in a private subnet to initiate outbound traffic to the internet while preventing inbound traffic from the internet. It enables secure internet access for resources that do not have public IP addresses.

11. 🔥 ALB vs NLB? — L7 HTTP vs L4 TCP.

    Ans: An Application Load Balancer (ALB) operates at Layer 7 (HTTP/HTTPS) and is designed to handle web traffic, providing advanced routing features based on content. A Network Load Balancer (NLB) operates at Layer 4 (TCP/UDP) and is optimized for handling high volumes of network traffic with low latency, making it suitable for applications that require extreme performance.

12. Route 53? — AWS DNS.

    Ans: Amazon Route 53 is a scalable and highly available Domain Name System (DNS) web service. It provides domain registration, DNS routing, and health checking of resources.

13. CloudFront? — CDN.

    Ans: Amazon CloudFront is a content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds. It caches content at edge locations to improve performance.

14. 🔥 IAM role vs user? — Assumable temp identity vs long-lived human.

    Ans: An IAM user is a long-lived identity that represents a person or service and has permanent credentials. An IAM role is an assumable identity that provides temporary security credentials for users or services to access AWS resources without needing to share long-term credentials.

15. IAM policy parts? — Effect, Action, Resource, Condition.

    Ans: An IAM policy consists of four main components: Effect (Allow or Deny), Action (the specific AWS service actions that are allowed or denied), Resource (the AWS resources to which the policy applies), and Condition (optional constraints that specify when the policy is in effect).

16. 🔥 Least privilege? — Grant only what's needed.

    Ans: The principle of least privilege means granting only the permissions necessary for a user or service to perform their tasks, reducing the risk of accidental or malicious actions.

17. Multi-AZ RDS? — Synchronous standby for failover (HA).

    Ans: Multi-AZ RDS deployments provide high availability by automatically replicating the database to a standby instance in a different Availability Zone. In the event of a failure, RDS can automatically failover to the standby instance, minimizing downtime.

18. Read Replica? — Async copies to scale reads.

    Ans: A Read Replica is an asynchronous copy of a primary database that can be used to offload read traffic and improve performance. It allows for scaling read operations without affecting the write performance of the primary database.

19. DynamoDB? — Managed NoSQL, single-digit ms.

    Ans: Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with single-digit millisecond latency. It is designed for applications that require high throughput and low latency at any scale.

20. ElastiCache? — Managed Redis/Memcached.

    Ans: Amazon ElastiCache is a fully managed in-memory data store and cache service that supports Redis and Memcached. It improves the performance of web applications by allowing you to retrieve information from fast, managed, in-memory caches instead of relying entirely on slower disk-based databases.

21. 🔥 Auto Scaling? — Add/remove instances on metrics.

    Ans: Auto Scaling automatically adjusts the number of EC2 instances in a group based on defined policies, health checks, and schedules. It helps maintain application availability and allows you to scale your EC2 capacity up or down automatically according to conditions you define.

22. Launch template? — Blueprint for ASG instances.

    Ans: A launch template is a resource that contains the configuration information required to launch EC2 instances, such as instance type, AMI ID, key pairs, security groups, and other settings. It serves as a blueprint for Auto Scaling Groups (ASGs) to create new instances consistently.

23. ECS? — AWS container orchestrator.

    Ans: Amazon Elastic Container Service (ECS) is a fully managed container orchestration service that allows you to run and manage Docker containers on a cluster of EC2 instances or using AWS Fargate for serverless container deployment.

24. 🔥 Fargate? — Serverless containers (no nodes).

    Ans: AWS Fargate is a serverless compute engine for containers that allows you to run containers without having to manage the underlying EC2 instances. It automatically provisions and scales the compute resources needed to run your containers.

25. ECR? — Private Docker registry.

    Ans: Amazon Elastic Container Registry (ECR) is a fully managed Docker container registry that makes it easy to store, manage, and deploy Docker container images. It integrates with ECS, EKS, and Fargate for seamless container deployment.

26. EKS? — Managed Kubernetes.

    Ans: Amazon Elastic Kubernetes Service (EKS) is a fully managed Kubernetes service that makes it easy to run Kubernetes on AWS without needing to install and operate your own Kubernetes control plane or nodes. It provides scalability, security, and high availability for containerized applications.

27. Lambda? — Serverless functions.

    Ans: AWS Lambda is a serverless compute service that allows you to run code without provisioning or managing servers. You can execute code in response to events, such as changes to data in S3, updates to DynamoDB tables, or HTTP requests via API Gateway.

28. 🔥 SQS vs SNS? — Queue (pull) vs pub/sub (push).

    Ans: Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables you to decouple and scale microservices, distributed systems, and serverless applications. It uses a pull-based model where consumers retrieve messages from the queue. Amazon Simple Notification Service (SNS) is a fully managed pub/sub messaging service that allows you to send messages to multiple subscribers or endpoints. It uses a push-based model where messages are delivered to subscribers in real-time.

29. EventBridge? — Event bus/rules.

    Ans: Amazon EventBridge is a serverless event bus service that makes it easy to connect applications using data from your own applications, integrated SaaS applications, and AWS services. It allows you to create rules to route events to different targets for processing.

30. API Gateway? — Managed API front door.

    Ans: Amazon API Gateway is a fully managed service that enables developers to create, publish, maintain, monitor, and secure APIs at any scale. It acts as a front door for applications to access data, business logic, or functionality from backend services.

31. 🔥 CloudWatch? — Logs, metrics, alarms, dashboards.

    Ans: Amazon CloudWatch is a monitoring and observability service that provides data and actionable insights for AWS resources, applications, and services. It collects and tracks metrics, collects and monitors log files, sets alarms, and automatically reacts to changes in your AWS resources.

32. CloudTrail? — API audit log.

    Ans: AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account. It records AWS API calls and events for your account and delivers log files to an Amazon S3 bucket, allowing you to track user activity and API usage.

33. X-Ray? — Distributed tracing.

    Ans: AWS X-Ray is a service that helps developers analyze and debug distributed applications, such as those built using a microservices architecture. It provides end-to-end tracing of requests as they travel through your application, allowing you to identify performance bottlenecks and errors.

34. KMS? — Managed encryption keys.

    Ans: AWS Key Management Service (KMS) is a fully managed service that makes it easy to create and control the encryption keys used to encrypt your data. It provides centralized key management, including key creation, rotation, and access control.

35. 🔥 Secrets Manager vs Parameter Store? — Rotation+cost vs cheap config.

    Ans: AWS Secrets Manager is a service that helps you protect access to your applications, services, and IT resources without the upfront investment and on-going maintenance costs of operating your own infrastructure. It provides automatic rotation of secrets, fine-grained access control, and auditing capabilities. AWS Systems Manager Parameter Store is a secure storage for configuration data and secrets management. It is a cost-effective solution for storing configuration data and secrets, but it does not provide automatic rotation or advanced features like Secrets Manager.

36. WAF? — Web app firewall.

    Ans: AWS Web Application Firewall (WAF) is a security service that helps protect your web applications from common web exploits and vulnerabilities. It allows you to create custom rules to block or allow traffic based on specific conditions, such as IP addresses, HTTP headers, or query string parameters.

37. GuardDuty? — Threat detection.

    Ans: Amazon GuardDuty is a threat detection service that continuously monitors for malicious or unauthorized behavior to help protect your AWS accounts and workloads. It analyzes data from AWS CloudTrail, VPC Flow Logs, and DNS logs to identify potential security threats.

38. Config? — Resource compliance rules.

    Ans: AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources. It continuously monitors and records your AWS resource configurations and allows you to automate the evaluation of recorded configurations against desired configurations.

39. Security Hub? — Aggregated security findings.

    Ans: AWS Security Hub is a security service that provides a comprehensive view of your security state within AWS. It aggregates, organizes, and prioritizes security findings from multiple AWS services and third-party security solutions, helping you identify and remediate potential security issues.

40. 🔥 S3 Block Public Access? — Prevents public exposure.

    Ans: S3 Block Public Access is a feature that helps you manage public access to your S3 buckets and objects. It provides settings to block public access at both the bucket and account levels, ensuring that your data is not inadvertently exposed to the public.

41. Presigned URL? — Temporary signed access.

    Ans: A presigned URL is a URL that grants temporary access to an S3 object. It is generated using AWS credentials and includes a signature that allows users to perform specific actions (such as GET or PUT) on the object for a limited time without requiring AWS credentials.

42. VPC Endpoint? — Private access to AWS services.

    Ans: A VPC Endpoint is a private connection between your VPC and supported AWS services or VPC endpoint services powered by AWS PrivateLink. It allows you to access AWS services without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.

43. VPC Peering? — Connect two VPCs.

    Ans: VPC Peering is a networking connection between two VPCs that enables you to route traffic between them using private IP addresses. It allows resources in different VPCs to communicate with each other as if they were within the same network.

44. Transit Gateway? — Hub for many VPCs.

    Ans: AWS Transit Gateway is a service that enables you to connect multiple VPCs and on-premises networks through a central hub. It simplifies network architecture by allowing you to manage connectivity between VPCs and on-premises networks in a scalable and efficient manner.

45. Elastic IP? — Static public IP.

    Ans: An Elastic IP address is a static, public IPv4 address designed for dynamic cloud computing. It can be associated with an EC2 instance or a network interface, allowing you to maintain a consistent IP address even if the underlying instance is stopped or terminated.

46. 🔥 Shared Responsibility? — AWS of cloud, you in cloud.

    Ans: The Shared Responsibility Model defines the division of security and compliance responsibilities between AWS and its customers. AWS is responsible for the security "of" the cloud, including the infrastructure, hardware, and software that run AWS services. Customers are responsible for security "in" the cloud, which includes managing their data, applications, and configurations within AWS services.

47. Well-Architected pillars? — Ops, Security, Reliability, Perf, Cost, Sustainability.

    Ans: The AWS Well-Architected Framework consists of six pillars: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, and Sustainability. These pillars provide guidance to help you design and operate reliable, secure, efficient, and cost-effective systems in the cloud.

48. Savings Plan? — Commit spend for discount.

    Ans: AWS Savings Plans are a flexible pricing model that offer significant savings on AWS usage in exchange for a commitment to a consistent amount of usage (measured in $/hour) for a one- or three-year term. They provide a way to reduce costs compared to on-demand pricing.

49. Trusted Advisor? — Cost/security/perf recommendations.

    Ans: AWS Trusted Advisor is an online resource that provides real-time guidance to help you provision your resources following AWS best practices. It offers recommendations in five categories: cost optimization, security, fault tolerance, performance, and service limits.

50. Organizations/SCP? — Multi-account governance guardrails.

    Ans: AWS Organizations is a service that allows you to centrally manage and govern multiple AWS accounts. Service Control Policies (SCPs) are a feature of AWS Organizations that enable you to define permission guardrails for your accounts, ensuring that they adhere to your organization's policies and compliance requirements.

## Terraform (51–85)
51. 🔥 IaC? — Infra defined as code.

    Ans: Infrastructure as Code (IaC) is the practice of managing and provisioning computing infrastructure through machine-readable configuration files, rather than through physical hardware configuration or interactive configuration tools.

52. Declarative? — Describe desired state.

    Ans: In a declarative approach, you define the desired state of your infrastructure, and the system automatically determines the necessary steps to achieve that state. Terraform uses a declarative language to describe infrastructure resources and their relationships.

53. Idempotent? — Same result each apply.

    Ans: Idempotence means that applying the same configuration multiple times will produce the same result, without causing unintended side effects. Terraform ensures that repeated applications of the same configuration will not change the infrastructure if it is already in the desired state.

54. Provider? — Plugin for a platform.

    Ans: A provider in Terraform is a plugin that allows Terraform to interact with a specific cloud platform or service. Providers define the resources and data sources available for that platform, enabling users to manage infrastructure across different environments.

55. 🔥 Resource vs data source? — Managed vs read-only existing.

    Ans: A resource in Terraform represents a managed infrastructure component that Terraform can create, update, or delete. A data source, on the other hand, is a read-only representation of existing infrastructure that allows you to retrieve information about resources that are not managed by Terraform.

56. Variable? — Input.

    Ans: A variable in Terraform is used to define input values that can be passed into a configuration. Variables allow you to parameterize your Terraform configurations, making them more flexible and reusable.

57. Output? — Exported value.

    Ans: An output in Terraform is a value that is exported from a configuration and can be used by other configurations or displayed to the user. Outputs are often used to provide information about the resources created, such as IP addresses or resource IDs.

58. Local? — Computed internal value.

    Ans: A local in Terraform is a named value that is computed within a configuration and can be used to simplify expressions or avoid repeating complex calculations. Locals are not exposed outside of the configuration and are primarily used for internal organization and readability.

59. 🔥 State file? — Record of managed infra.

    Ans: The state file in Terraform is a JSON file that keeps track of the resources managed by Terraform. It records the current state of the infrastructure, including resource IDs, metadata, and dependencies, allowing Terraform to determine what changes need to be made during subsequent runs.

60. 🔥 Remote backend? — Shared state (S3).

    Ans: A remote backend in Terraform is a configuration that allows the state file to be stored in a remote location, such as Amazon S3, rather than locally on the user's machine. This enables collaboration among team members, as they can access and update the shared state file, and provides additional features like state locking and versioning.

61. State locking? — DynamoDB prevents concurrent apply.

    Ans: State locking in Terraform is a mechanism that prevents concurrent modifications to the state file by using a locking system, such as DynamoDB. When one user is applying changes, the state file is locked, preventing other users from making changes until the lock is released, ensuring consistency and avoiding conflicts.

62. 🔥 terraform init/plan/apply/destroy? — Setup/preview/execute/teardown.

    Ans: `terraform init` initializes a Terraform configuration, `terraform plan` previews the changes that will be made, `terraform apply` executes the changes, and `terraform destroy` tears down the infrastructure.

63. fmt/validate? — Format/check.

    Ans: `terraform fmt` is used to format Terraform configuration files according to the standard style, and `terraform validate` is used to check the syntax and internal consistency of the configuration files.

64. 🔥 Module? — Reusable resource bundle.

    Ans: A module in Terraform is a container for multiple resources that are used together. Modules allow you to encapsulate and reuse configurations, making it easier to manage complex infrastructure by breaking it down into smaller, manageable components.

65. count vs for_each? — Index list vs keyed map.

    Ans: `count` is used to create multiple instances of a resource based on an integer value, typically for indexed lists. `for_each` is used to create multiple instances of a resource based on a map or set, allowing for more complex and flexible resource creation with unique keys.

66. 🔥 Drift? — Real infra differs from code.

    Ans: Drift occurs when the actual state of the infrastructure diverges from the desired state defined in the Terraform configuration. This can happen due to manual changes made outside of Terraform or changes made by other tools, leading to inconsistencies between the code and the real infrastructure.

67. import? — Adopt existing infra.

    Ans: The `terraform import` command allows you to bring existing infrastructure resources under Terraform management. It maps the existing resource to a Terraform resource in your configuration, enabling you to manage it going forward without recreating it.

68. state rm? — Stop managing without deleting.

    Ans: The `terraform state rm` command is used to remove a resource from the Terraform state file without deleting the actual resource in the infrastructure. This is useful when you want to stop managing a resource with Terraform while keeping it intact in your environment.

69. taint/-replace? — Force recreate.

    Ans: The `terraform taint` command marks a resource for recreation on the next apply, indicating that it is in a bad state or needs to be replaced. The `-replace` option can be used with `terraform apply` to force the replacement of a specific resource without marking it as tainted.

70. Workspace? — Multiple state instances.

    Ans: A workspace in Terraform allows you to have multiple instances of a state file, enabling you to manage different environments (e.g., development, staging, production) within the same configuration.

71. 🔥 create_before_destroy? — Avoid downtime on replace.

    Ans: The `create_before_destroy` lifecycle setting in Terraform ensures that a new resource is created before the old resource is destroyed during an update. This helps to avoid downtime by maintaining availability while replacing resources.

72. prevent_destroy? — Guard critical resources.

    Ans: The `prevent_destroy` lifecycle setting in Terraform prevents a resource from being destroyed, even if it is removed from the configuration. This is useful for protecting critical resources that should not be accidentally deleted.

73. ignore_changes? — Ignore external edits.

    Ans: The `ignore_changes` lifecycle setting in Terraform allows you to specify certain attributes of a resource that should be ignored during updates. This is useful when external changes are made to a resource that you do not want Terraform to overwrite.

74. depends_on? — Explicit ordering.

    Ans: The `depends_on` argument in Terraform allows you to specify explicit dependencies between resources, ensuring that one resource is created or updated only after another resource has been successfully created or updated. This helps manage the order of operations in complex configurations.

75. dynamic block? — Generate nested blocks.

    Ans: A dynamic block in Terraform allows you to generate nested blocks within a resource or module based on a collection of values. It is useful for creating multiple instances of a nested block dynamically, such as security group rules or tags, based on input variables or data sources.

76. 🔥 How store secrets? — Not in Git; env/Secrets Manager; sensitive.

    Ans: Secrets should not be stored in version control systems like Git. Instead, use environment variables, secret management services (e.g., AWS Secrets Manager, HashiCorp Vault), or Terraform's `sensitive` attribute to handle sensitive data securely.

77. tfvars? — Variable values file.

    Ans: A `.tfvars` file in Terraform is used to define variable values for a configuration. It allows you to specify values for input variables in a separate file, making it easier to manage and override variable values without modifying the main configuration files.

78. TF_VAR_x? — Env var for variable x.

    Ans: The `TF_VAR_x` environment variable is used to set the value of a Terraform variable named `x`. By exporting this environment variable, you can provide input values for Terraform variables without using a `.tfvars` file or command-line arguments.

79. Provisioner? — Run scripts (last resort).

    Ans: A provisioner in Terraform is used to execute scripts or commands on a resource after it has been created or updated. Provisioners are typically used as a last resort for tasks that cannot be accomplished through Terraform's declarative configuration, such as bootstrapping software or configuring resources.

80. null_resource? — Trigger arbitrary actions.

    Ans: A `null_resource` in Terraform is a resource that does not manage any infrastructure but can be used to trigger arbitrary actions, such as running provisioners or executing scripts. It is often used for tasks that do not fit into the standard resource model.

81. terraform graph? — Dependency graph.

    Ans: The `terraform graph` command generates a visual representation of the dependency graph for the resources in your Terraform configuration. It shows how resources are related and the order in which they will be created or updated.

82. Registry? — Shared modules.

    Ans: The Terraform Registry is a centralized repository for sharing and discovering Terraform modules. It allows users to find pre-built modules for various cloud providers and services, making it easier to reuse and share infrastructure code.

83. checkov/tflint? — Security/lint scan.

    Ans: Checkov is a static code analysis tool that scans Terraform configurations for security and compliance issues, while TFLint is a linter for Terraform that checks for best practices, potential errors, and style issues in your configuration files.

84. 🔥 CI/CD pattern? — plan on PR, apply on merge.

    Ans: A common CI/CD pattern for Terraform is to run `terraform plan` on pull requests (PRs) to review changes and `terraform apply` on merge to the main branch. This ensures that changes are reviewed before being applied to the infrastructure.

85. Why not edit state? — Corruption risk.

    Ans: Editing the Terraform state file directly can lead to corruption and inconsistencies between the actual infrastructure and the state file. It is recommended to use Terraform commands to manage resources and state to ensure that the state remains accurate and reliable.

## Docker & Kubernetes (86–140)
86. 🔥 Container vs VM? — Shares kernel vs full OS.

    Ans: A container shares the host operating system's kernel and runs isolated processes, making it lightweight and efficient. A virtual machine (VM) includes a full operating system and runs on a hypervisor, which provides complete isolation but with more overhead.

87. Image vs container? — Template vs running instance.

    Ans: An image is a static, read-only template that contains the application code, libraries, and dependencies needed to run a container. A container is a running instance of an image, which includes the application and its environment, allowing it to execute as an isolated process on the host system.

88. 🔥 Layer? — Cached filesystem diff per instruction.

    Ans: A layer in Docker is a filesystem diff that represents the changes made by a single instruction in a Dockerfile. Layers are cached and reused across builds, which helps to speed up the build process and reduce image size.

89. Registry? — Image store (ECR).

    Ans: A registry is a storage and distribution system for Docker images. It allows users to push, pull, and manage container images. Amazon Elastic Container Registry (ECR) is a fully managed Docker container registry that makes it easy to store, manage, and deploy Docker container images.

90. 🔥 Dockerfile? — Build recipe.

    Ans: A Dockerfile is a text file that contains a set of instructions for building a Docker image. It defines the base image, application code, dependencies, and configuration needed to create a containerized application.

91. FROM? — Base image.

    Ans: The `FROM` instruction in a Dockerfile specifies the base image to use for the new image being built. It sets the starting point for the build process and can be an official image from a registry or a custom image.

92. 🔥 CMD vs ENTRYPOINT? — Default args vs fixed executable.

    Ans: `CMD` specifies the default command to run when a container is started, but it can be overridden by providing a different command at runtime. `ENTRYPOINT` defines a fixed executable that will always run when the container starts, and any arguments provided at runtime will be passed to this executable.

93. COPY vs ADD? — Plain copy vs copy+untar+URL.

    Ans: The `COPY` instruction in a Dockerfile is used to copy files and directories from the host machine into the container's filesystem. The `ADD` instruction can also copy files, but it has additional functionality, such as automatically extracting tar archives and supporting remote URLs.

94. EXPOSE? — Documents port.

    Ans: The `EXPOSE` instruction in a Dockerfile is used to document the ports that a container listens on at runtime. It does not actually publish the ports; it serves as a hint for users and tools about which ports should be exposed.

95. 🔥 Multi-stage build? — Build then slim runtime.

    Ans: A multi-stage build in Docker allows you to use multiple `FROM` statements in a single Dockerfile, enabling you to separate the build environment from the runtime environment. This helps to create smaller, more efficient images by copying only the necessary artifacts from the build stage to the final image.

96. .dockerignore? — Exclude files from build.

    Ans: A `.dockerignore` file is used to specify files and directories that should be excluded from the Docker build context. This helps to reduce the size of the build context, speed up the build process, and prevent sensitive or unnecessary files from being included in the image.

97. Volume? — Persistent storage.

    Ans: A volume in Docker is a persistent storage mechanism that allows data to be stored outside of the container's filesystem. Volumes can be shared between containers and are managed by Docker, making them suitable for storing application data that needs to persist across container restarts or recreations.

98. Bind mount? — Host path mount.

    Ans: A bind mount in Docker is a way to mount a directory or file from the host machine into a container. This allows the container to access and modify files on the host system, providing a way to share data between the host and the container.

99. Docker network? — Container communication.

    Ans: A Docker network is a virtual network that allows containers to communicate with each other and with the host system. Docker provides several network drivers, such as bridge, host, overlay, and macvlan, to support different networking scenarios and use cases.

100. 🔥 Reduce image size? — Multi-stage, alpine, ignore, layers.

    Ans: To reduce Docker image size, you can use multi-stage builds, choose a minimal base image like Alpine, use a `.dockerignore` file to exclude unnecessary files, and minimize the number of layers by combining commands.

101. Non-root user? — Security best practice.

    Ans: Running containers as a non-root user is a security best practice that helps to minimize the potential impact of a security vulnerability. By using a non-root user, you limit the permissions and access that the container has, reducing the risk of privilege escalation and unauthorized access to the host system.

102. docker logs? — Container stdout/stderr.

    Ans: The `docker logs` command is used to fetch the logs of a container, which includes the standard output (stdout) and standard error (stderr) streams. This is useful for debugging and monitoring the behavior of running containers.

103. docker exec? — Run command in container.

    Ans: The `docker exec` command allows you to run a command inside a running container. It is useful for debugging, inspecting the container's environment, or performing administrative tasks without needing to start a new container.

104. 🔥 Pod? — Smallest K8s unit.

    Ans: A pod is the smallest deployable unit in Kubernetes, representing a single instance of a running process in a cluster. It can contain one or more containers that share the same network namespace, storage volumes, and configuration.

105. ReplicaSet? — Keep N replicas.

    Ans: A ReplicaSet is a Kubernetes resource that ensures a specified number of pod replicas are running at any given time. It helps maintain the desired state by automatically creating or deleting pods as needed.

106. 🔥 Deployment? — Rolling update + rollback.

    Ans: A Deployment is a Kubernetes resource that manages the deployment and scaling of ReplicaSets. It provides features such as rolling updates, which allow you to update pods gradually without downtime, and rollback capabilities to revert to a previous version if needed.

107. StatefulSet? — Stable id/storage.

    Ans: A StatefulSet is a Kubernetes resource that manages the deployment and scaling of stateful applications. It provides stable, unique network identifiers, persistent storage, and ordered deployment and scaling.

108. DaemonSet? — One pod per node.

    Ans: A DaemonSet is a Kubernetes resource that ensures that a copy of a specific pod runs on all (or some) nodes in the cluster. It is commonly used for deploying system-level services, such as log collectors or monitoring agents.

109. Job/CronJob? — Batch/scheduled.

    Ans: A Job is a Kubernetes resource that creates one or more pods to perform a specific task and ensures that the task completes successfully. A CronJob is a resource that schedules Jobs to run at specified times or intervals, similar to a cron job in Unix-like systems.

110. 🔥 Service? — Stable endpoint + LB.
    
    Ans: A Service in Kubernetes is an abstraction that defines a logical set of pods and provides a stable network endpoint (IP address and DNS name) for accessing those pods. Services can also provide load balancing to distribute traffic across the pods.

111. ClusterIP? — Internal only.

    Ans: ClusterIP is a type of Kubernetes Service that exposes the service on an internal IP address within the cluster. It allows communication between pods and services within the cluster but is not accessible from outside the cluster.

112. NodePort? — Port on each node.

    Ans: NodePort is a type of Kubernetes Service that exposes the service on a static port on each node's IP address. It allows external traffic to access the service by sending requests to any node in the cluster on the specified port.

113. LoadBalancer? — Cloud LB.

    Ans: LoadBalancer is a type of Kubernetes Service that provisions an external load balancer (usually provided by the cloud provider) to distribute incoming traffic across the pods in the service. It provides a single IP address for external access and handles load balancing automatically.

114. 🔥 Ingress? — HTTP routing + TLS.

    Ans: Ingress is a Kubernetes resource that manages external access to services within a cluster, typically HTTP and HTTPS traffic. It provides routing rules, SSL/TLS termination, and can be used to expose multiple services under a single IP address or domain name.

115. 🔥 ConfigMap vs Secret? — Config vs sensitive.

    Ans: A ConfigMap is a Kubernetes resource used to store non-sensitive configuration data in key-value pairs, which can be consumed by pods as environment variables or mounted as files. A Secret is a Kubernetes resource used to store sensitive information, such as passwords, tokens, or keys, in an encrypted format. Secrets provide additional security features, such as base64 encoding and access control.

116. 🔥 Liveness probe? — Restart if dead.

    Ans: A Liveness probe is a Kubernetes mechanism used to determine if a container is still running. If the liveness probe fails, the kubelet will kill the container, and it will be subject to the pod's restart policy.

117. 🔥 Readiness probe? — Remove from LB if not ready.

    Ans: A Readiness probe is a Kubernetes mechanism used to determine if a container is ready to accept traffic. If the readiness probe fails, the pod will be removed from the service's load balancer, preventing it from receiving traffic until it becomes ready again.

118. Startup probe? — Grace for slow start.

    Ans: A Startup probe is a Kubernetes mechanism used to determine if a container has started successfully. It provides a grace period for containers that take longer to start, allowing them to initialize before the liveness and readiness probes are applied.

119. requests/limits? — Guaranteed/max resources.

    Ans: In Kubernetes, resource requests and limits are used to manage the CPU and memory resources allocated to containers. Requests specify the minimum amount of resources required for a container to run, while limits define the maximum amount of resources a container can use. This helps ensure that containers have the necessary resources to operate while preventing them from consuming excessive resources that could impact other containers in the cluster.

120. 🔥 HPA? — Scale pods on metrics.

    Ans: A Horizontal Pod Autoscaler (HPA) is a Kubernetes resource that automatically adjusts the number of pods in a deployment or replica set based on observed CPU utilization or other select metrics. It helps ensure that applications have the right amount of resources to handle varying loads.

121. VPA? — Resize pod resources.

    Ans: A Vertical Pod Autoscaler (VPA) is a Kubernetes resource that automatically adjusts the CPU and memory resource requests and limits for containers in a pod based on observed usage. It helps optimize resource allocation for pods, ensuring they have the appropriate resources to run efficiently without over-provisioning.

122. Namespace? — Cluster partition.

    Ans: A Namespace is a Kubernetes resource that provides a way to divide cluster resources between multiple users or teams. It helps organize and manage resources within a cluster, allowing for resource isolation and access control.

123. 🔥 RBAC? — In-cluster permissions.

    Ans: Role-Based Access Control (RBAC) is a Kubernetes mechanism for managing access to resources within a cluster. It allows administrators to define roles with specific permissions and assign those roles to users or service accounts, controlling what actions they can perform on different resources.

124. ServiceAccount? — Pod identity.

    Ans: A ServiceAccount is a Kubernetes resource that provides an identity for processes running in a pod. It is used to authenticate and authorize access to the Kubernetes API and other resources, allowing pods to interact with the cluster securely.

125. 🔥 IRSA? — Pod IAM on EKS (no keys).

    Ans: IAM Roles for Service Accounts (IRSA) is a feature in Amazon EKS that allows you to associate an AWS IAM role with a Kubernetes service account. This enables pods running in the cluster to assume the IAM role and access AWS resources securely without needing to manage long-term AWS credentials or keys.

126. NetworkPolicy? — Pod firewall.

    Ans: A NetworkPolicy is a Kubernetes resource that defines rules for how pods can communicate with each other and with other network endpoints. It acts as a firewall for pods, controlling inbound and outbound traffic based on specified criteria.

127. PV/PVC? — Storage + claim.

    Ans: A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. A PersistentVolumeClaim (PVC) is a request for storage by a user, which specifies the desired size and access mode. PVCs are used to bind to PVs, allowing pods to use persistent storage.

128. StorageClass? — Dynamic volume type.

    Ans: A StorageClass is a Kubernetes resource that defines the parameters for dynamically provisioning PersistentVolumes (PVs). It allows administrators to specify different types of storage (e.g., SSD, HDD) and their associated properties, such as performance characteristics and reclaim policies.

129. 🔥 Helm? — K8s package manager.

    Ans: Helm is a package manager for Kubernetes that simplifies the deployment and management of applications on a Kubernetes cluster. It uses charts, which are collections of files that describe a related set of Kubernetes resources, allowing users to easily install, upgrade, and manage applications.

130. Kustomize? — Overlay config.

    Ans: Kustomize is a configuration management tool for Kubernetes that allows users to customize and manage Kubernetes resource configurations without modifying the original YAML files. It uses overlays and patches to create variations of base configurations, enabling easier management of different environments.

131. 🔥 Rolling update? — Gradual pod replace.

    Ans: A rolling update is a deployment strategy in Kubernetes that gradually replaces old pods with new ones, ensuring that the application remains available during the update process. It allows for zero-downtime updates by controlling the number of pods that are updated at a time.

132. Rollback? — `kubectl rollout undo`.

    Ans: Rollback in Kubernetes is the process of reverting a deployment to a previous version. This can be done using the `kubectl rollout undo` command, which allows you to restore the deployment to a known good state if an update causes issues.

133. 🔥 Self-healing? — Controller reconciles desired state.

    Ans: Self-healing in Kubernetes refers to the ability of controllers (such as Deployments, ReplicaSets, and StatefulSets) to automatically monitor and maintain the desired state of the cluster. If a pod or resource fails or is deleted, the controller will create new instances to replace them, ensuring that the application remains available and resilient.

134. 🔥 CrashLoopBackOff? — App keeps crashing.

    Ans: CrashLoopBackOff is a Kubernetes pod status that indicates a container is repeatedly crashing and restarting. This can occur due to application errors, misconfigurations, or resource constraints. The "BackOff" part means that Kubernetes is applying an exponential backoff strategy to delay subsequent restart attempts.

135. ImagePullBackOff? — Can't pull image.

    Ans: ImagePullBackOff is a Kubernetes pod status that indicates the container runtime is unable to pull the specified container image from the registry. This can happen due to incorrect image names, missing tags, authentication issues, or network problems.

136. Pending pod? — Can't schedule.

    Ans: A Pending pod in Kubernetes is a pod that has been created but has not yet been scheduled to run on a node. This can occur due to insufficient resources, node taints, or scheduling constraints that prevent the pod from being assigned to a suitable node.

137. OOMKilled? — Exceeded memory limit.

    Ans: OOMKilled is a Kubernetes pod status that indicates a container was terminated by the system because it exceeded its allocated memory limit. The Out of Memory (OOM) killer is invoked to free up memory, and the container is killed to prevent the node from running out of memory.

138. etcd? — Cluster state store.

    Ans: etcd is a distributed key-value store that is used by Kubernetes to store the cluster's state and configuration data. It provides a reliable way to persist and retrieve information about the cluster, including resource definitions, configurations, and metadata.

139. kubelet? — Runs pods on node.

    Ans: The kubelet is an agent that runs on each node in a Kubernetes cluster. It is responsible for managing the lifecycle of pods, ensuring that containers are running as expected, and reporting the status of the node and its pods back to the Kubernetes control plane.

140. kube-proxy? — Pod networking.

    Ans: kube-proxy is a network proxy that runs on each node in a Kubernetes cluster. It is responsible for maintaining network rules and facilitating communication between pods and services, enabling load balancing and service discovery within the cluster.


## Git & CI/CD (141–175)
141. 🔥 merge vs rebase? — Merge commit vs linear replay.

    Ans: Merge creates a new commit that combines the changes from two branches, preserving the history of both branches. Rebase moves or reapplies commits from one branch onto another, creating a linear history.

142. 🔥 fetch vs pull? — Download vs download+merge.

    Ans: `git fetch` downloads commits, files, and refs from a remote repository into your local repository without merging them into your current branch. `git pull` is a combination of `git fetch` followed by `git merge`, which updates your current branch with the changes from the remote branch.

143. 🔥 reset vs revert? — Rewrite history vs new inverse commit.

    Ans: `git reset` moves the current branch pointer to a specified commit, effectively rewriting history and discarding commits. `git revert` creates a new commit that undoes the changes made by a previous commit, preserving the history.

144. soft/mixed/hard reset? — Keep staged/working/discard.

    Ans: A soft reset (`git reset --soft`) moves the branch pointer to a specified commit but keeps the changes in the staging area. A mixed reset (`git reset --mixed`) moves the branch pointer and resets the staging area, but keeps the changes in the working directory. A hard reset (`git reset --hard`) moves the branch pointer, resets the staging area, and discards all changes in the working directory.

145. cherry-pick? — Apply one commit.

    Ans: `git cherry-pick` is a command that allows you to apply the changes introduced by a specific commit from one branch onto another branch. It creates a new commit on the target branch with the same changes as the original commit.

146. stash? — Shelve changes.

    Ans: `git stash` is a command that temporarily shelves (or stashes) changes in your working directory that are not yet ready to be committed. This allows you to switch branches or work on something else without losing your uncommitted changes. You can later apply the stashed changes back to your working directory.

147. 🔥 reflog? — Recover lost commits.

    Ans: `git reflog` is a command that shows a log of all the changes made to the tips of branches and other references in your repository. It allows you to recover lost commits by providing a history of where your branch pointers have been, even if those commits are no longer reachable through the current branch history.

148. tag? — Named release pointer.

    Ans: A tag in Git is a reference that points to a specific commit, often used to mark release points (e.g., v1.0, v2.0). Tags can be lightweight (just a name) or annotated (with metadata such as the tagger's name, date, and message).

149. 🔥 Merge conflict? — Same lines changed both sides.

    Ans: A merge conflict occurs when Git is unable to automatically resolve differences between two branches being merged because the same lines of code have been modified in both branches. In such cases, manual intervention is required to resolve the conflict and determine which changes to keep.

150. fast-forward? — Pointer moves, no merge commit.

    Ans: A fast-forward merge occurs when the current branch can be updated to match the target branch without creating a new merge commit. This happens when there are no divergent changes, and the current branch's pointer can simply be moved forward to the target branch's commit.

151. 🔥 Trunk-based? — Short branches to main.

    Ans: Trunk-based development is a software development practice where developers work on short-lived feature branches or directly on the main branch (trunk). The goal is to integrate changes frequently, reducing the complexity of long-lived branches and minimizing merge conflicts.

152. GitFlow? — develop/feature/release/hotfix.

    Ans: GitFlow is a branching model for Git that defines a strict branching strategy with specific branches for development, features, releases, and hotfixes. It provides a structured workflow for managing code changes and releases in a collaborative environment.

153. Protected branch? — Require checks/reviews.

    Ans: A protected branch in Git is a branch that has restrictions on who can push to it and what actions can be performed. It often requires code reviews, passing status checks, and may prevent force pushes or deletion, ensuring that the branch remains stable and secure.

154. CODEOWNERS? — Auto reviewers by path.

    Ans: A CODEOWNERS file in a Git repository specifies individuals or teams responsible for specific files or directories. When changes are made to those files, the designated code owners are automatically requested for review, helping to ensure that the right people review changes to critical parts of the codebase.

155. 🔥 CI? — Auto build+test per commit.

    Ans: Continuous Integration (CI) is a software development practice where code changes are automatically built and tested every time a commit is made to the version control system. This helps to identify integration issues early, improve code quality, and streamline the development process.

156. CD delivery vs deployment? — Manual vs auto to prod.

    Ans: Continuous Delivery (CD) is a software development practice where code changes are automatically prepared for a release to production, but the actual deployment requires manual approval. Continuous Deployment, on the other hand, automatically deploys every change that passes the automated tests to production without manual intervention.

157. Artifact? — Build output.

    Ans: An artifact is a file or set of files produced as a result of the build process in software development. Artifacts can include compiled binaries, libraries, documentation, configuration files, and other resources that are necessary for deploying or running an application.

158. 🔥 Pipeline stages? — Build/test/scan/package/deploy.

    Ans: Pipeline stages in a CI/CD pipeline typically include the following steps: Build (compiling the code), Test (running automated tests), Scan (security and quality checks), Package (creating deployable artifacts), and Deploy (releasing the application to the target environment).

159. 🔥 Workflow/job/step? — GitHub Actions units.

    Ans: In GitHub Actions, a workflow is a configurable automated process that runs one or more jobs. A job is a set of steps that execute on the same runner, and a step is an individual task within a job, such as running a command or an action.

160. runs-on? — Runner type.

    Ans: The `runs-on` keyword in GitHub Actions specifies the type of runner (virtual machine or container) that the job will run on. It can be set to predefined labels like `ubuntu-latest`, `windows-latest`, or custom self-hosted runners.

161. needs? — Job dependency.

    Ans: The `needs` keyword in GitHub Actions is used to define job dependencies, indicating that a job should only run after the specified jobs have completed successfully. This allows for controlling the order of execution and ensuring that prerequisite jobs are completed before dependent jobs start.

162. matrix? — Parallel variants.

    Ans: The `matrix` strategy in GitHub Actions allows you to run a job multiple times with different combinations of parameters, such as operating systems, programming language versions, or environment variables. This enables testing across various configurations in parallel.

163. 🔥 OIDC to AWS? — Keyless temp creds.

    Ans: OpenID Connect (OIDC) to AWS allows GitHub Actions to authenticate with AWS without using long-term credentials. By configuring OIDC, you can request temporary security credentials from AWS for your workflows, enabling secure access to AWS resources without storing sensitive keys in your repository.

164. Environment + approval? — Prod gate.

    Ans: In GitHub Actions, environments can be configured with protection rules, such as required reviewers or approval gates. This means that before a job can deploy to a production environment, it must receive approval from designated reviewers, ensuring that changes are reviewed and authorized before affecting critical systems.

165. 🔥 Blue-green? — Swap old/new.

    Ans: Blue-green deployment is a release management strategy that reduces downtime and risk by running two identical production environments, referred to as "blue" and "green." At any given time, one environment serves live production traffic while the other is idle. When deploying a new version, traffic is switched from the old environment to the new one, allowing for quick rollback if issues arise.

166. 🔥 Canary? — Gradual % rollout.

    Ans: Canary deployment is a release management strategy where a new version of an application is gradually rolled out to a small subset of users or servers before being deployed to the entire user base. This allows for monitoring and testing the new version in production with minimal risk, enabling quick detection of issues and rollback if necessary.

167. Rolling? — Gradual instance replace.

    Ans: Rolling deployment is a release management strategy where new versions of an application are deployed incrementally to a set of instances, replacing the old version one at a time. This approach minimizes downtime and allows for continuous availability of the application during the update process.

168. 🔥 Rollback? — Redeploy previous good.

    Ans: Rollback is the process of reverting an application or system to a previous stable state after a failed deployment or update. This can involve redeploying the last known good version of the application, restoring backups, or reverting configuration changes to ensure that the system returns to a functional state.

169. SAST? — Static code scan (CodeQL).

    Ans: Static Application Security Testing (SAST) is a method of analyzing source code or compiled code for security vulnerabilities without executing the program. Tools like CodeQL can be used to perform SAST, identifying potential security issues early in the development process.

170. SCA? — Dependency scan (Dependabot).

    Ans: Software Composition Analysis (SCA) is a method of analyzing an application's dependencies and third-party libraries for known security vulnerabilities. Tools like Dependabot can automatically scan and update dependencies to ensure that the application uses secure and up-to-date components.

171. Container scan? — Image CVEs (Trivy).

    Ans: Container scanning is the process of analyzing container images for known security vulnerabilities, misconfigurations, and compliance issues. Tools like Trivy can scan container images for Common Vulnerabilities and Exposures (CVEs) and provide reports on potential security risks.

172. IaC scan? — Checkov/tflint.

    Ans: Infrastructure as Code (IaC) scanning involves analyzing IaC templates and configurations for security vulnerabilities, misconfigurations, and best practices. Tools like Checkov and TFLint can be used to perform IaC scans, helping to ensure that infrastructure code is secure and compliant before deployment.

173. 🔥 GitOps? — Git as source of truth (ArgoCD).

    Ans: GitOps is a set of practices that use Git as the single source of truth for declarative infrastructure and application configurations. Tools like ArgoCD can automatically synchronize the desired state defined in Git with the actual state in the cluster, enabling continuous deployment and version control for infrastructure.

174. Quality gate? — SonarQube pass/fail.

    Ans: A quality gate is a set of conditions that a project must meet before it can be considered ready for release. In SonarQube, a quality gate evaluates code quality metrics such as code coverage, code smells, bugs, and security vulnerabilities, and determines whether the project passes or fails based on predefined thresholds.

175. Secret in logs? — Mask, never echo.

    Ans: Secrets should never be logged in plaintext. Always mask sensitive information in logs and avoid echoing secrets to the console or log files. Use secure storage solutions like AWS Secrets Manager or HashiCorp Vault to manage secrets.


## Linux, Observability & Security (176–200)
176. 🔥 755 vs 644? — rwxr-xr-x vs rw-r--r--.

    Ans: The numbers 755 and 644 represent file permissions in Linux. 755 means the owner can read, write, and execute, while the group and others can read and execute. 644 means the owner can read and write, while the group and others can only read.

177. chmod +x? — Make executable.

    Ans: The command `chmod +x` adds the executable permission to a file, allowing it to be run as a program or script.

178. 🔥 kill vs kill -9? — Graceful vs forced.

    Ans: The `kill` command sends a termination signal (SIGTERM) to a process, allowing it to exit gracefully and perform cleanup. The `kill -9` command sends a SIGKILL signal, which forcefully terminates the process without allowing it to clean up or handle the signal.

179. Zombie process? — Dead, parent didn't reap.

    Ans: A zombie process is a process that has completed execution but still has an entry in the process table because its parent process has not yet read its exit status. Zombie processes do not consume CPU or memory resources, but they do occupy a process ID (PID) until the parent process reaps them.

180. Orphan? — Parent died, init adopts.

    Ans: An orphan process is a process whose parent process has terminated or died. In Unix-like operating systems, orphan processes are adopted by the init process (PID 1), which becomes their new parent and is responsible for cleaning them up when they terminate.

181. Hard vs soft link? — Same inode vs pointer.

    Ans: A hard link is a directory entry that points directly to the inode of a file, allowing multiple filenames to refer to the same file content. A soft link (or symbolic link) is a special type of file that contains a reference (path) to another file or directory, and it can point to files on different filesystems.

182. 🔥 $?? — Last exit code.

    Ans: The `$?` variable in a shell script or command line environment holds the exit status of the last executed command. An exit code of 0 typically indicates success, while any non-zero value indicates an error or failure.

183. set -euo pipefail? — Strict error handling.

    Ans: The `set -euo pipefail` command in a shell script enables strict error handling. The `-e` option causes the script to exit immediately if any command returns a non-zero exit status. The `-u` option treats unset variables as an error and exits the script. The `-o pipefail` option ensures that the exit status of a pipeline is the exit status of the last command to exit with a non-zero status, rather than the last command in the pipeline.

184. 🔥 > vs >> vs 2>&1? — Overwrite/append/stderr merge.

    Ans: In shell scripting, `>` is used to redirect output to a file, overwriting its contents. `>>` appends output to the end of a file without overwriting existing content. `2>&1` redirects standard error (file descriptor 2) to standard output (file descriptor 1), allowing both stdout and stderr to be captured together.

185. awk vs sed vs grep? — Columns/substitute/search.

    Ans: `awk` is a text processing tool that allows you to manipulate and analyze data in columns, perform calculations, and format output. `sed` is a stream editor used for text substitution, deletion, and transformation of text in a file or input stream. `grep` is a command-line utility used to search for specific patterns or strings within files or input streams.

186. cron format? — min hour day month weekday.

    Ans: The cron format consists of five fields that specify the schedule for running a command or script. The fields are: minute (0-59), hour (0-23), day of the month (1-31), month (1-12), and day of the week (0-7, where both 0 and 7 represent Sunday). Each field can contain specific values, ranges, lists, or wildcards to define the desired schedule.

187. systemctl? — Manage services.

    Ans: `systemctl` is a command-line utility used to manage systemd services. It allows you to start, stop, restart, enable, disable, and check the status of services on a Linux system.

188. journalctl? — Service logs.

    Ans: `journalctl` is a command-line utility used to view and query logs collected by the systemd journal. It allows you to filter logs by service, time range, priority, and other criteria, providing a centralized way to access system and application logs.

189. 🔥 df vs du? — FS usage vs folder usage.

    Ans: The `df` command displays information about the disk space usage of file systems, including total size, used space, available space, and mount points. The `du` command shows the disk usage of files and directories, providing a summary of the space consumed by specific folders or files.

190. 🔥 Logs/metrics/traces? — Events/numbers/request path.

    Ans: Logs are records of events that have occurred in a system, providing detailed information about the state and behavior of applications. Metrics are numerical measurements that quantify the performance or health of a system, such as CPU usage, memory consumption, or request latency. Traces are records of the execution path of requests through a distributed system, allowing you to follow the flow of a request across multiple services and identify bottlenecks or failures.

191. CloudWatch vs CloudTrail? — Perf vs audit.

    Ans: Amazon CloudWatch is a monitoring and observability service that provides metrics, logs, and alarms to help you monitor the performance and health of your AWS resources and applications. Amazon CloudTrail is a service that enables governance, compliance, and operational auditing by recording API calls made on your AWS account, providing a history of actions taken by users, roles, or services.

192. 🔥 SLI/SLO/SLA? — Measure/target/contract.

    Ans: SLI (Service Level Indicator) is a quantitative measure of a specific aspect of service performance, such as latency or error rate. SLO (Service Level Objective) is a target value or range for an SLI that defines the desired level of service performance. SLA (Service Level Agreement) is a formal contract between a service provider and a customer that specifies the agreed-upon SLOs and the consequences if those objectives are not met.

193. Error budget? — 1 − SLO.

    Ans: An error budget is the allowable amount of errors or downtime that a service can experience while still meeting its Service Level Objectives (SLOs). It is calculated as 1 minus the SLO, representing the percentage of time or requests that can fail without violating the agreed-upon service level.

194. MTTR/MTBF? — Recovery/between failures.

    Ans: MTTR (Mean Time to Recovery) is the average time it takes to restore a system or service after a failure. MTBF (Mean Time Between Failures) is the average time between consecutive failures of a system or component, indicating its reliability and expected operational lifespan.

195. p50 vs p99? — Median vs tail latency.

    Ans: p50 (50th percentile) represents the median latency, meaning that 50% of requests are faster than this value. p99 (99th percentile) represents the tail latency, meaning that 99% of requests are faster than this value, and only 1% of requests take longer. Tail latency is often used to assess the performance of a system under high load or in edge cases.

196. RED/USE? — Rate-Errors-Duration / Util-Sat-Errors.

    Ans: RED (Rate, Errors, Duration) is a monitoring approach that focuses on measuring the rate of requests, the number of errors, and the duration of requests to assess system performance. USE (Utilization, Saturation, Errors) is another monitoring approach that evaluates resource utilization, saturation levels, and error rates to identify potential bottlenecks and performance issues in a system.

197. 🔥 Encryption rest vs transit? — KMS/SSE vs TLS.

    Ans: Encryption at rest refers to the protection of data stored on disk or in persistent storage, typically using services like AWS KMS (Key Management Service) or server-side encryption (SSE). Encryption in transit refers to the protection of data as it moves across networks, typically using protocols like TLS (Transport Layer Security) to secure communication between clients and servers.

198. 🔥 Where store secrets? — Secrets Manager, never code.

    Ans: Secrets should be stored in a secure secrets management service, such as AWS Secrets Manager or HashiCorp Vault, and never hard-coded in the application code.

199. Shift-left security? — Scan early in CI.

    Ans: Shift-left security is the practice of integrating security testing and vulnerability scanning early in the software development lifecycle, typically during the continuous integration (CI) process, to identify and address security issues sooner.

200. 🔥 Reduce cost? — Right-size, autoscale, spot, lifecycle.

    Ans: To reduce costs in cloud environments, you can right-size your resources to match actual usage, use autoscaling to adjust capacity based on demand, leverage spot instances for lower-cost compute, and implement lifecycle policies to manage resource usage efficiently.

201. 🔥 Observability vs monitoring? — Insights vs alerts.

    Ans: Observability is the ability to understand the internal state of a system based on the data it produces, providing insights into its behavior. Monitoring is the practice of collecting and analyzing metrics, logs, and traces to detect and respond to issues, often generating alerts when predefined thresholds are breached.

202. 🔥 Defense in depth? — Multiple security layers.

    Ans: Defense in depth is a security strategy that employs multiple layers of defense to protect systems and data. By implementing various security measures at different levels (e.g., network, application, endpoint), it reduces the likelihood of a successful attack and provides redundancy in case one layer is compromised.

203. 🔥 Principle of least privilege? — Grant only what's needed.

    Ans: The principle of least privilege is a security concept that recommends granting users, applications, and systems only the minimum level of access necessary to perform their tasks. This reduces the risk of unauthorized access and limits the potential impact of security breaches.

204. 🔥 Zero trust? — Verify every request, no implicit trust.

    Ans: Zero trust is a security model that assumes no implicit trust for any user, device, or network, regardless of whether they are inside or outside the organization's perimeter. It requires continuous verification of identity and access rights for every request, enforcing strict access controls and authentication mechanisms.

205. 🔥 Incident response? — Detect, analyze, contain, eradicate, recover.

    Ans: Incident response is a structured approach to handling security incidents, which includes the following phases: Detect (identify potential security events), Analyze (assess the impact and scope of the incident), Contain (limit the spread and impact of the incident), Eradicate (remove the root cause and affected components), and Recover (restore systems and services to normal operation while implementing lessons learned to prevent future incidents).

206. 🔥 Threat modeling? — Identify, assess, mitigate risks.

    Ans: Threat modeling is a proactive security practice that involves identifying potential threats to a system, assessing their impact and likelihood, and implementing mitigation strategies to reduce risks. It helps organizations understand their attack surface and prioritize security measures.

---
💡 Cover the right column, test yourself, star the misses.
