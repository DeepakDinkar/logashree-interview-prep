# 🏢 Vocal — Company-Wise Question Banks (Set 2)

> Real questions grouped by company so you can drill the exact style each asks. No answers here — train recall, then verify in [`../../Definitions/`](../../Definitions/). 🔥 = reported frequently.
> Covers AWS DevOps / SRE / Cloud / Platform roles (4+ yrs).

---

## TCS 🔥 (service — breadth, fundamentals, scripting)
1. What is DevOps? Explain the DevOps lifecycle.

    Ans: DevOps is a set of practices that combines software development (Dev) and IT operations (Ops) to shorten the development lifecycle and provide continuous delivery with high software quality. The DevOps lifecycle consists of several stages:
    - **Planning:** Define the project requirements and plan the development process.
    - **Coding:** Write the application code and perform version control using tools like Git.
    - **Building:** Compile the code and build the application using build tools like Maven or Grad
le.
    - **Testing:** Conduct automated and manual testing to ensure the application meets quality standards.
    - **Release:** Deploy the application to production or staging environments.

2. 🔥 Difference between continuous integration, delivery, and deployment.

    Ans: Continuous Integration (CI) is the practice of automatically integrating code changes from multiple contributors into a shared repository several times a day, followed by automated testing. Continuous Delivery (CD) extends CI by automatically deploying code changes to a staging or production environment after passing tests, but requires manual approval for production deployment. Continuous Deployment goes a step further by automatically deploying every change that passes automated tests to production without manual intervention.

3. What is the difference between Git merge and rebase?

    Ans: Git merge combines the histories of two branches, creating a new commit that represents the merge. It preserves the original branch history and creates a non-linear history. Git rebase, on the other hand, moves or combines a sequence of commits to a new base commit, creating a linear history. Rebase can make the commit history cleaner but can also rewrite history, which may cause issues if not used carefully.

4. How do you revert a pushed commit?   

    Ans: To revert a pushed commit, you can use the `git revert` command followed by the commit hash. This creates a new commit that undoes the changes made by the specified commit without altering the commit history. For example:
    ```
    git revert <commit-hash>
    ```
    After running this command, you will need to push the new commit to the remote repository:
    ```
    git push origin <branch-name>
    ```

5. 🔥 Explain `chmod 755`. How do Linux permissions work?

    Ans: The `chmod 755` command sets the permissions of a file or directory in Linux. The number `755` represents the permission settings for the owner, group, and others. In this case:
- The first digit `7` means the owner has read (4), write (2), and execute (1) permissions, totaling 7.
- The second digit `5` means the group has read (4) and execute (1) permissions, totaling 5.
- The third digit `5` means others have read (4) and execute (1) permissions, totaling

6. Write a shell script to find the largest file in a directory.

```bash
#!/bin/bash
# Check if a directory is provided as an argument
if [ -z "$1" ]; then

    echo "Usage: $0 <directory>"
        exit 1
    fi
```

```bash
# Find the largest file in the specified directory
largest_file=$(find "$1" -type f -exec ls -s {} + | sort -n -r | head -n 1 | awk '{print $2}')
echo "The largest file in the directory is: $largest_file"
```

7. What is a cron job? Schedule a job for every 15 minutes.

    Ans: A cron job is a scheduled task in Unix-like operating systems that runs automatically at specified intervals. It is managed by the cron daemon, which reads the crontab (cron table) file to determine when to execute the jobs.
    ```
    To schedule a job to run every 15 minutes, you can add the following line to your crontab file:
    */15 * * * * /path/to/your/script.sh
    This means the script will run at every 15-minute interval (e.g., 00, 15, 30, 45 minutes past the hour).
    ```

8. What is the difference between a process and a thread (OS level)?

    Ans: A process is an independent program in execution that has its own memory space, resources, and execution context. Each process runs in isolation from other processes. A thread, on the other hand, is a smaller unit of execution within a process that shares the same memory space and resources of the parent process. Threads are lightweight and allow for concurrent execution within a single process, making them more efficient for tasks that require shared data.

9. 🔥 What is Infrastructure as Code? Why Terraform?

    Ans: Infrastructure as Code (IaC) is the practice of managing and provisioning computing infrastructure through machine-readable configuration files, rather than through manual processes. It allows for version control, automation, and consistency in infrastructure management. Terraform is a popular IaC tool that enables users to define and provision infrastructure across various cloud providers using a declarative configuration language. It supports multi-cloud environments, has a large community, and provides features like state management and resource graphing.

10. Difference between Docker image and container.

    Ans: A Docker image is a lightweight, standalone, and executable package that contains all the necessary code, libraries, dependencies, and configuration files needed to run an application. It is a static snapshot of an application at a specific point in time. A Docker container, on the other hand, is a runtime instance of a Docker image. It is a live, running environment that encapsulates the application and its dependencies, allowing it to run consistently across different environments. Containers are isolated from each other and the host system, providing a secure and efficient way to deploy applications.

11. What are the stages of your CI/CD pipeline?

    Ans: The stages of a CI/CD pipeline typically include:
- **Source:** Code is committed to a version control system (e.g., Git).
- **Build:** The code is compiled and built into an executable or package.
- **Test:** Automated tests are run to validate the code's functionality and quality.
- **Deploy:** The application is deployed to a staging or production environment.
- **Monitor:** The application's performance and health are monitored in production.

12. How do you monitor an application in production?

    Ans: Monitoring an application in production involves tracking its performance, availability, and health using various tools and techniques. This can include:
- **Logging:** Collecting and analyzing logs to identify errors and issues.
- **Metrics:** Gathering performance metrics (e.g., response time, CPU usage, memory usage) to monitor the application's health.
- **Alerts:** Setting up alerts to notify the team of any critical issues or anomalies.
- **Tracing:** Implementing distributed tracing to track requests across different services and identify bottlenecks.
- **Dashboards:** Creating visual dashboards to provide real-time insights into the application's performance and health.

13. What is a load balancer? Types in AWS.

    Ans: A load balancer is a device or software that distributes incoming network traffic across multiple servers to ensure no single server becomes overwhelmed, improving application availability and reliability. In AWS, there are three main types of load balancers:
- **Application Load Balancer (ALB):** Operates at the application layer (Layer 7) and is ideal for HTTP/HTTPS traffic. It provides advanced routing features, such as host-based and path-based routing.
- **Network Load Balancer (NLB):** Operates at the transport layer (Layer 4) and is designed for high-performance, low-latency traffic. It can handle millions of requests per second and is suitable for TCP/UDP traffic.
- **Classic Load Balancer (CLB):** Operates at both the application and transport layers (Layer 4 and Layer 7) and is suitable for simple load balancing of HTTP/HTTPS and TCP traffic. It is being phased out in favor of ALB and NLB.

14. Explain VPC, subnet, and security group.
    
    Ans: A Virtual Private Cloud (VPC) is a logically isolated network within the AWS cloud where you can launch AWS resources. A subnet is a range of IP addresses within a VPC, allowing you to segment your network for better organization and security. A security group acts as a virtual firewall for your instances, controlling inbound and outbound traffic at the instance level.

15. What is Auto Scaling and how does it work?

    Ans: Auto Scaling is a feature in AWS that automatically adjusts the number of EC2 instances in a group based on demand. It helps maintain application availability and allows you to scale your resources up or down according to traffic patterns. Auto Scaling works by defining scaling policies and metrics (e.g., CPU utilization, request count) that trigger the addition or removal of instances. When the defined thresholds are met, Auto Scaling launches new instances or terminates existing ones to match the desired capacity.

## Infosys 🔥 (service — Git, AWS basics, Terraform)
16. 🔥 Difference between `git fetch` and `git pull`.

    Ans: `git fetch` retrieves the latest changes from a remote repository but does not merge them into your local branch. It updates your local copy of the remote branches, allowing you to review changes before integrating them. `git pull`, on the other hand, is a combination of `git fetch` and `git merge`. It fetches the latest changes from the remote repository and automatically merges them into your current branch, which can lead to conflicts if there are overlapping changes.

17. How do you resolve a merge conflict?

    Ans: To resolve a merge conflict, follow these steps:
1. Identify the conflicting files by running `git status`.
2. Open the conflicting files in a text editor and look for conflict markers (e.g.,
    `<<<<<<<`, `=======`, `>>>>>>>`).
3. Manually edit the files to resolve the conflicts by choosing which changes to keep or combining them as needed.
4. After resolving the conflicts, save the files and stage them using `git add <file>`.
5. Commit the changes with a message indicating that the conflicts have been resolved using `git commit -m "Resolved merge conflicts"`.
6. Finally, push the changes to the remote repository using `git push`.

18. What is a Terraform module? Why use it?

    Ans: A Terraform module is a container for multiple resources that are used together. It allows you to group related resources and reuse them across different parts of your infrastructure. Modules can be created locally or sourced from the Terraform Registry. Using modules promotes code reusability, maintainability, and organization, making it easier to manage complex infrastructure setups. By encapsulating resources into modules, you can also enforce best practices and standardize configurations across your projects.

19. 🔥 What is Terraform state? Where do you store it?

    Ans: Terraform state is a file that keeps track of the current state of your infrastructure managed by Terraform. It contains information about the resources that have been created, updated, or deleted, allowing Terraform to determine what changes need to be applied during subsequent runs. The state file is typically stored locally in a file named `terraform.tfstate`, but it can also be stored remotely in a backend (e.g., AWS S3, HashiCorp Consul, or Terraform Cloud) for collaboration and versioning. Storing the state remotely is recommended for team environments to ensure consistency and prevent conflicts.

20. Explain the difference between Security Group and NACL.

    Ans: Security Groups (SG) and Network Access Control Lists (NACLs) are both used to control traffic in AWS, but they operate at different levels. Security Groups act as virtual firewalls for EC2 instances, controlling inbound and outbound traffic at the instance level. They are stateful, meaning if you allow an inbound request, the response is automatically allowed. NACLs, on the other hand, operate at the subnet level and are stateless, meaning you need to explicitly allow both inbound and outbound traffic. NACLs provide an additional layer of security by controlling traffic to and from subnets.

21. What are S3 storage classes?

    Ans: Amazon S3 offers several storage classes to optimize cost and performance based on access patterns and data durability requirements. The main S3 storage classes include:
- **S3 Standard:** Designed for frequently accessed data, offering low latency and high throughput.
- **S3 Intelligent-Tiering:** Automatically moves data between two access tiers (frequent and
    infrequent) based on changing access patterns, optimizing costs.
- **S3 Standard-IA (Infrequent Access):** Suitable for data that is accessed less frequently but requires rapid access when needed. It offers lower storage costs compared to S3 Standard.
- **S3 One Zone-IA:** Similar to Standard-IA but stores data in a
    single availability zone, offering lower costs but less durability.

22. How do you secure an S3 bucket?

    Ans: To secure an S3 bucket, you can follow these best practices:
- **Bucket Policies:** Use bucket policies to define access permissions for users and roles.
- **IAM Policies:** Attach IAM policies to users, groups, or roles to control access to
    the bucket.
- **Access Control Lists (ACLs):** Use ACLs to manage access at the object level.
- **Enable Versioning:** Enable versioning to protect against accidental deletions or overwrites.
- **Enable Server-Side Encryption:** Use server-side encryption (SSE) to encrypt data
    at rest.
- **Enable MFA Delete:** Require multi-factor authentication (MFA) for delete operations to add an extra layer of security.

23. What is the difference between ALB and NLB?

    Ans: Application Load Balancer (ALB) and Network Load Balancer (NLB) are two types of load balancers in AWS that serve different purposes:
- **ALB:** Operates at the application layer (Layer 7) and is designed
    for HTTP/HTTPS traffic. It provides advanced routing features, such as host-based and path-based routing, and supports WebSocket and HTTP/2 protocols. ALB is ideal for applications that require content-based routing and SSL termination.
- **NLB:** Operates at the transport layer (Layer 4) and is designed for high-performance, low-latency traffic. It can handle millions of requests per second and is suitable for TCP/UDP traffic. NLB is ideal for applications that require extreme performance and static IP addresses.

24. Explain IAM roles vs users.

    Ans: IAM (Identity and Access Management) roles and users are both used to manage access to AWS resources, but they serve different purposes:
- **IAM Users:** Represent individual identities with long-term credentials (username and password or access keys
). Users are typically associated with a single person and are used for direct access to AWS resources.
- **IAM Roles:** Represent a set of permissions that can be assumed by trusted entities, such
    as IAM users, applications, or AWS services. Roles do not have long-term credentials and are used for temporary access to resources. Roles are ideal for granting permissions to applications or services that need to interact with AWS resources without exposing long-term credentials.

25. What is a Dockerfile? Explain each instruction.

    Ans: A Dockerfile is a text file that contains a series of instructions on how to build a Docker image. Each instruction in a Dockerfile creates a layer in the image. Common instructions include:
- **FROM:** Specifies the base image to use for the Docker image.
- **RUN:** Executes commands in the container during the build process.
- **COPY:** Copies files from the host machine to the container.
- **ADD:** Similar to COPY but can also extract tar files and fetch files from URLs.
- **CMD:** Specifies the default command to run when the container starts.
- **ENTRYPOINT:** Configures a container to run as an executable.
- **ENV:** Sets environment variables in the container.
- **EXPOSE:** Informs Docker that the container listens on a specific network port.
- **WORKDIR:** Sets the working directory for subsequent instructions.
- **VOLUME:** Creates a mount point for external storage.

26. How do you reduce Docker image size?

    Ans: To reduce Docker image size, you can follow these best practices:
- **Use a minimal base image:** Start with a lightweight base image (e.g., Alpine
) to reduce the overall size of the image.
- **Combine RUN commands:** Combine multiple RUN commands into a single command to reduce the number of
    layers in the image.
- **Remove unnecessary files:** Clean up temporary files, package caches, and other unnecessary files during the build process.
- **Use multi-stage builds:** Use multi-stage builds to separate the build environment from the final
runtime environment, allowing you to include only the necessary artifacts in the final image.
- **Leverage .dockerignore:** Use a .dockerignore file to exclude files and directories
that are not needed in the image, reducing the build context size.

27. Kubernetes: what is a pod, deployment, service?

    Ans: In Kubernetes:
- **Pod:** A pod is the smallest deployable unit in Kubernetes that represents a single instance of a running process in a cluster. It can contain one or more containers that share the same network namespace and storage volumes. Pods are ephemeral and can be created, scaled, and destroyed as needed.
- **Deployment:** A deployment is a higher-level abstraction that manages a set of pods and ensures the desired state is maintained. It provides features like rolling updates, scaling, and self-healing.
- **Service:** A service is an abstraction that defines a logical set of pods and a policy to access them. It provides stable IP addresses and DNS names, load balancing, and service discovery.

28. How does a rolling update work?

    Ans: A rolling update is a deployment strategy in Kubernetes that gradually replaces old versions of pods with new ones without downtime. During a rolling update, the deployment controller creates new pods with the updated version while simultaneously terminating the old pods. The process continues until all old pods are replaced with new ones. This approach ensures that a minimum number of pods are always available to serve requests, maintaining application availability throughout the update process. Rolling updates can be configured with parameters like `maxUnavailable` and `maxSurge` to control the pace of the update and the number of pods that can be unavailable at any given time.

29. What is CloudWatch? How do you set an alarm?

    Ans: Amazon CloudWatch is a monitoring and observability service that provides data and actionable insights for AWS resources, applications, and services. It collects metrics, logs, and events, allowing you to monitor performance, troubleshoot issues, and set alarms for specific conditions.

30. Write a script to check if a service is running and restart it.

```bash
#!/bin/bash
SERVICE_NAME="your_service_name"

if systemctl is-active --quiet $SERVICE_NAME; then
    echo "$SERVICE_NAME is running."
else
    echo "$SERVICE_NAME is not running. Restarting..."
    systemctl restart $SERVICE_NAME
fi
```

## Cognizant (CTS) 🔥 (service — Docker/K8s, CI/CD depth)
31. 🔥 Difference between CMD and ENTRYPOINT.

    Ans: In a Dockerfile, both CMD and ENTRYPOINT are used to specify the command that will be executed when a container starts, but they serve different purposes:
- **CMD:** Provides default arguments for the container's main process. It can be overridden by specifying a different command when running the container. CMD is typically used to provide default behavior for the container.
- **ENTRYPOINT:** Configures the container to run as an executable, making it more rigid. ENTRYPOINT cannot be easily overridden, and it is used to define the main command that should always be executed when the container starts. You can still pass additional arguments to the ENTRYPOINT command, but the main command itself remains fixed. 

32. What is a multi-stage Docker build?

    Ans: A multi-stage Docker build is a technique that allows you to use multiple `FROM` statements in a single Dockerfile to create intermediate images for building your application. This approach helps reduce the final image size by separating the build environment from the runtime environment. In a multi-stage build, you can compile your application in one stage and then copy only the necessary artifacts (e.g., binaries, configuration files) into a smaller base image in a subsequent stage. This results in a leaner final image that contains only what is needed to run the application, improving security and performance.

33. 🔥 Liveness vs readiness probe.

    Ans: In Kubernetes, liveness and readiness probes are used to monitor the health of containers within pods:
- **Liveness Probe:** Determines if a container is still running. If the liveness probe fails, Kubernetes will restart the container. This is useful for detecting and recovering from situations where a container is alive but stuck in a non-responsive state.
- **Readiness Probe:** Determines if a container is ready to accept traffic. If the readiness probe fails, Kubernetes will remove the pod from the service endpoints, preventing it from receiving traffic until it becomes ready again. This is useful for ensuring that only healthy and fully initialized containers receive traffic, improving the overall reliability of the application.

34. ConfigMap vs Secret in Kubernetes.

    Ans: In Kubernetes, ConfigMaps and Secrets are both used to manage configuration data for applications, but they serve different purposes and have different security characteristics:
- **ConfigMap:** ConfigMaps are used to store non-sensitive configuration data in key-value pairs
. They can be used to configure application settings, environment variables, or command-line arguments. ConfigMaps are not encrypted and are suitable for storing data that does not require confidentiality.
- **Secret:** Secrets are used to store sensitive information, such as passwords, API keys, or certificates. They are encoded in base64 and can be encrypted at rest, providing an additional layer of security. Secrets should be used for any data that needs to be kept confidential and should not be exposed in plain text.

35. How do you roll back a Kubernetes deployment?

    Ans: To roll back a Kubernetes deployment, you can use the `kubectl rollout undo` command. This command allows you to revert the deployment to a previous revision. Here are the steps to roll back a deployment:
1. Check the rollout history of the deployment to see the available revisions:
   ```
   kubectl rollout history deployment <deployment-name>
   ```
2. Identify the revision you want to roll back to.
3. Execute the rollback command:
    ```
    kubectl rollout undo deployment <deployment-name> --to-revision=<revision-number>
    ```

36. What is `git cherry-pick`? When used?

    Ans: `git cherry-pick` is a Git command that allows you to apply a specific commit from one branch onto another branch. It is used when you want to selectively apply changes from a commit without merging the entire branch. This is useful in scenarios where you need to backport a bug fix or feature from one branch to another without bringing in unrelated changes. To use `git cherry-pick`, you can run the following command:
```
git cherry-pick <commit-hash>
```

37. `git reset` soft vs mixed vs hard.

    Ans: The `git reset` command is used to undo changes in the Git history and working directory. It has three main modes: soft, mixed, and hard:
- **Soft Reset (`git reset --soft <commit>`):** Moves the HEAD pointer to the specified commit without changing the index or working directory. The changes from the reset commits remain staged for commit.
- **Mixed Reset (`git reset --mixed <commit>`):** Moves the HEAD pointer to the specified commit and resets the index, but does not change the working directory. The changes from the reset commits are unstaged and remain in the working directory.
- **Hard Reset (`git reset --hard <commit>`):** Moves the HEAD pointer to the specified commit and resets both the index and working directory. All changes from the reset commits are discarded, and the working directory is updated to match the specified commit. This is a destructive operation and should be used with caution, as it can permanently delete uncommitted changes.

38. How do you handle secrets in a pipeline?

    Ans: Handling secrets in a pipeline involves securely managing sensitive information such as API keys, passwords, and tokens. Here are some best practices for handling secrets in a CI/CD pipeline:
- **Use Secret Management Tools:** Utilize secret management tools like HashiCorp Vault, AWS Secrets Manager, or Azure Key Vault to securely store and retrieve secrets.
- **Environment Variables:** Store secrets as environment variables in the CI/CD platform, ensuring they are not hardcoded in the codebase or configuration files.
- **Encrypted Files:** Use encrypted files or configuration files to store secrets, and decrypt them at runtime using secure methods.
- **Access Control:** Implement strict access control policies to limit who can access secrets and ensure that only authorized personnel or services can retrieve them.
- **Audit Logging:** Enable audit logging to track access and usage of secrets, helping to identify any unauthorized access or potential security breaches.
- **Rotate Secrets Regularly:** Regularly rotate secrets to minimize the risk of exposure and ensure that compromised secrets are quickly replaced.

39. What is blue-green deployment?
    
    Ans: Blue-green deployment is a release management strategy that reduces downtime and risk by running two identical production environments, referred to as "blue" and "green." At any given time, one environment (e.g., blue) is live and serving production traffic, while the other environment (e.g., green) is idle or used for testing the new version of the application. When a new version is ready for deployment, it is deployed to the idle environment (green). Once the new version is verified and tested, traffic is switched from the live environment (blue) to the new environment (green), making it live. This approach allows for quick rollbacks if issues arise, as traffic can be redirected back to the previous environment (blue) with minimal disruption.

40. Explain Terraform `count` vs `for_each`.

    Ans: In Terraform, `count` and `for_each` are both used to create multiple instances of a resource, but they have different use cases and behaviors:
- **count:** The `count` meta-argument is used to create a specified number of identical resource instances. It is best suited for scenarios where you want to create a fixed number of resources based on a simple integer value. The instances are indexed numerically (0, 1, 2, ...), and you can reference them using the `count.index` variable. For example:
```hcl
resource "aws_instance" "example" {
  count = 3
  ami           = "ami-123456"
  instance_type = "t2.micro"
}
- **for_each:** The `for_each` meta-argument is used to create multiple resource instances based on a map or set of values. It is more flexible than `count` and allows you to create resources with unique identifiers. Each instance can be referenced using the key from the map or set. This is useful when you want to create resources with different configurations or names. For example:
```hcl
resource "aws_instance" "example" {
  for_each = {
    "instance1" = "ami-123456"
    "instance2" = "ami-789012"
  }
  ami           = each.value
  instance_type = "t2.micro"
}
```

41. What is drift in Terraform? How detect it?

    Ans: Drift in Terraform refers to the situation where the actual state of the infrastructure diverges from the state defined in the Terraform configuration files. This can occur when changes are made directly to the infrastructure outside of Terraform, such as manual modifications in the cloud provider's console or through other tools. Drift can lead to inconsistencies and unexpected behavior in your infrastructure.
To detect drift in Terraform, you can use the `terraform plan` command. This command compares the current state of the infrastructure with the desired state defined in the configuration files and generates an execution plan that highlights any differences. If there are discrepancies, Terraform will indicate which resources have drifted and what changes would be made to bring the infrastructure back in line with the configuration. Additionally, you can use the `terraform state` commands to inspect the current state and identify any resources that may have drifted from their expected configuration.

42. How do you debug a CrashLoopBackOff pod?

    Ans: To debug a CrashLoopBackOff pod in Kubernetes, follow these steps:
1. **Check Pod Status:** Use the command `kubectl get pods` to check the status of the pod and confirm that it is in a CrashLoopBackOff state.
2. ** View Pod Logs:** Use the command `kubectl logs <pod-name>` to view the logs of the crashing container. This can provide insights into why the container is failing to start.
3. ** Describe the Pod:** Use the command `kubectl describe pod <pod-name>` to get detailed information about the pod, including events, container status, and any error messages that may indicate the cause of the crash.
4. **Check Container Configuration:** Review the container's configuration, including environment variables, command, and resource limits, to ensure they are set correctly.
5. **Check for Resource Constraints:** Ensure that the pod has sufficient CPU and memory resources allocated. If the pod is being killed due to resource constraints, consider adjusting the resource requests and limits.
6. **Check for Dependency Issues:** Verify that any dependencies required by the container (e.g., services, databases) are available and accessible.
7. **Test Locally:** If possible, run the container image locally to see if it starts successfully. This can help identify issues that may not be apparent in the Kubernetes environment.
8. **Iterate and Fix:** Based on the findings from the logs and pod description, make necessary changes to the container configuration or application code, and redeploy the pod to see if the issue is resolved.

43. What is a namespace in Kubernetes?

    Ans: A namespace in Kubernetes is a logical partitioning of cluster resources that allows for the organization and management of resources within a single cluster. Namespaces provide a way to create multiple virtual clusters within a physical cluster, enabling resource isolation, access control, and resource quota management. Each namespace can have its own set of resources, such as pods, services, and deployments, and can be used to separate environments (e.g., development, staging, production) or teams within an organization. By default, Kubernetes has a "default" namespace, but additional namespaces can be created as needed.

44. Difference between `kubectl apply` and `kubectl create`.

    Ans: In Kubernetes, `kubectl apply` and `kubectl create` are both used to manage resources, but they serve different purposes:
- **kubectl create:** This command is used to create a new resource in the cluster based on the provided configuration file. It will fail if the resource already exists, and it does not support updating existing resources. For example:
```
kubectl create -f deployment.yaml
- **kubectl apply:** This command is used to create or update a resource in the cluster based on the provided configuration file. It allows for declarative management of resources, meaning you can define the desired state of the resource, and Kubernetes will make the necessary changes to achieve that state. If the resource already exists, `kubectl apply` will update it to match the configuration file. For example:
```
kubectl apply -f deployment.yaml
```
```
45. How do you manage multiple environments in Terraform?

    Ans: Managing multiple environments in Terraform can be achieved using workspaces, directory structures, or separate state files. Here are some common approaches:
- **Workspaces:** Terraform workspaces allow you to create multiple instances of your infrastructure within the same configuration. Each workspace has its own state file, enabling you to manage different environments (e.g., development, staging, production) without duplicating configuration files. You can switch between workspaces using the command `terraform workspace select <workspace-name>`.
- **Directory Structure:** You can organize your Terraform configurations into separate directories for each environment. Each directory can have its own set of configuration files and state files, allowing you to manage environments independently. For example:
```
├── dev/
│   ├── main.tf
│   └── terraform.tfstate
├── staging/
│   ├── main.tf
│   └── terraform.tfstate
└── prod/
    ├── main.tf
    └── terraform.tfstate
- **Separate State Files:** You can use different state files for each environment by specifying the `-backend-config` option when initializing Terraform. This allows you to maintain separate state files for each environment, ensuring that changes in one environment do not affect others. For example:
```
terraform init -backend-config="path=dev/terraform.tfstate"
terraform init -backend-config="path=staging/terraform.tfstate"
terraform init -backend-config="path=prod/terraform.tfstate"

## Wipro / Capgemini / Hexaware (service — mixed)
46. What is the shared responsibility model?

    Ans: The shared responsibility model is a framework that defines the division of security and compliance responsibilities between cloud service providers (CSPs) and their customers. In this model, the CSP is responsible for the security of the cloud infrastructure, including physical data centers, networking, and hardware, while the customer is responsible for securing their applications, data, and configurations within the cloud environment. The specific responsibilities may vary depending on the type of cloud service (IaaS, PaaS, SaaS) being used. Understanding the shared responsibility model is crucial for ensuring that both parties fulfill their obligations to maintain a secure and compliant cloud environment.

47. 🔥 How do you achieve high availability on AWS?

    Ans: Achieving high availability on AWS involves designing your architecture to minimize downtime and ensure that your applications remain accessible even in the event of failures. Here are some strategies to achieve high availability:
- **Multi-AZ Deployments:** Deploy your applications across multiple Availability Zones (AZs)
    to ensure redundancy and fault tolerance. This allows your application to continue operating even if one AZ experiences an outage.
- **Load Balancing:** Use Elastic Load Balancers (ELBs) to distribute incoming traffic across multiple instances or services, ensuring that no single instance becomes a bottleneck or point of failure.
- **Auto Scaling:** Implement Auto Scaling groups to automatically adjust the number of instances based on demand
, ensuring that your application can handle traffic spikes and maintain performance.
- **Database Replication:** Use database replication and failover mechanisms (e.g., Amazon R
DS Multi-AZ) to ensure that your database remains available in the event of a failure.
- **Monitoring and Alerts:** Set up monitoring and alerting using Amazon CloudWatch to detect issues
    and respond quickly to potential failures.

48. What is a NAT Gateway vs Internet Gateway?

    Ans: In AWS, a NAT Gateway and an Internet Gateway serve different purposes in networking:
- **NAT Gateway:** A NAT (Network Address Translation) Gateway allows instances in a private subnet to access the internet for outbound traffic while preventing inbound traffic from the internet. It translates private IP addresses to a public IP address, enabling instances in private subnets to communicate with external services without exposing them to the internet. NAT Gateways are typically used for scenarios where instances need to download updates or access external APIs without being directly reachable from the internet.
- **Internet Gateway:** An Internet Gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in a VPC and the internet. It enables instances in public subnets to send and receive traffic from the internet. An Internet Gateway is required for instances to have public IP addresses and be accessible from the internet.

49. RDS Multi-AZ vs Read Replica.

    Ans: In AWS, RDS Multi-AZ and Read Replica are two different features that serve different purposes for database availability and scalability:
- **RDS Multi-AZ:** Multi-AZ deployments provide high availability and failover support
for RDS instances. In a Multi-AZ setup, AWS automatically provisions and maintains a synchronous standby replica in a different Availability Zone (AZ). If the primary instance fails, RDS automatically fails over to the standby replica, minimizing downtime and ensuring data durability. Multi-AZ is primarily used for disaster recovery and high availability.
- **Read Replica:** Read Replicas are used to improve read scalability and performance for RDS instances. They are asynchronous copies of the primary database that can be used to offload read traffic from the primary instance. Read Replicas can be created in the same region or across different regions, and they can be promoted to become standalone databases if needed. Read Replicas are primarily used for read-heavy workloads and reporting purposes, rather than for high availability.

50. What is EC2 user data?

    Ans: EC2 user data is a feature in Amazon EC2 that allows you to provide custom scripts or configuration data to an instance at launch time. User data can be used to automate the initial setup and configuration of an instance, such as installing software, configuring services, or running initialization scripts. The user data is executed only once during the first boot of the instance, and it can be provided in various formats, including shell scripts, cloud-init directives, or other supported formats. User data is typically specified when launching an instance through the AWS Management Console, CLI, or SDKs.

51. Difference between stop and terminate an EC2 instance.

    Ans: In AWS, stopping and terminating an EC2 instance are two different actions with distinct consequences:
- **Stop:** When you stop an EC2 instance, the instance is shut down, and its state is preserved. The instance can be restarted later, and it will retain its instance ID, private IP address, and any attached EBS volumes. Stopping an instance does not incur charges for the instance while it is stopped, but you will still be charged for any attached EBS volumes.
- **Terminate:** When you terminate an EC2 instance, the instance is permanently deleted, and it cannot be restarted. All associated resources, such as EBS volumes (unless they are configured to be retained), are also deleted. Terminating an instance results in the loss of the instance ID, private IP address, and any data stored on the instance's ephemeral storage. Termination is a permanent action, and you will not be able to recover the instance or its data after termination.

52. What is EBS vs EFS vs instance store?

    Ans: In AWS, EBS (Elastic Block Store), EFS (Elastic File System), and instance store are different types of storage options with distinct characteristics:
- **EBS (Elastic Block Store):** EBS provides block-level storage volumes that can be attached to EC2 instances. EBS volumes are persistent, meaning they retain data even after the instance is stopped or terminated. They are suitable for use cases that require low-latency access to data, such as databases and file systems. EBS volumes can be resized, backed up using snapshots, and encrypted for security.
- **EFS (Elastic File System):** EFS is a fully managed, scalable,
    and elastic file storage service that provides a shared file system accessible by multiple EC2 instances. EFS is designed for use cases that require concurrent access to a file system from multiple instances, such as web servers, content management systems, and big data applications. EFS automatically scales storage capacity based on demand and supports NFS (Network File System) protocol for compatibility with various operating systems.
- **Instance Store:** Instance store provides temporary block-level storage for EC2 instances. The data on an instance store is ephemeral, meaning it is lost when the instance is stopped, terminated, or fails. Instance store is suitable for use cases that require high IOPS and low latency, such as caching, temporary storage, or scratch data.

53. How do you back up an RDS database?

    Ans: To back up an RDS database, you can use the following methods:
- **Automated Backups:** Enable automated backups for your RDS instance. AWS automatically takes daily snapshots of your database and retains transaction logs for point-in-time recovery. You can configure the retention period for automated backups, and AWS will manage the backup process for you.
- **Manual Snapshots:** You can create manual snapshots of your RDS database at any time. Manual snapshots are user-initiated and can be retained indefinitely until you choose to delete them. To create a manual snapshot, you can use the AWS Management Console, CLI, or SDKs. For example, using the CLI:
```
aws rds create-db-snapshot --db-instance-identifier <instance-id> --db-snapshot-identifier <snapshot-name>
```
- **Exporting Data:** You can also export your RDS database data to other storage services, such as Amazon S3, for backup purposes. This can be done using database-specific tools or services, such as AWS Database Migration Service (DMS) or native database export features.

54. Explain Terraform workspaces.

    Ans: Terraform workspaces are a feature that allows you to manage multiple instances of your infrastructure within the same configuration. Each workspace has its own state file, enabling you to maintain separate environments (e.g., development, staging, production) without duplicating configuration files. Workspaces provide a way to isolate changes and manage different versions of your infrastructure while using the same Terraform codebase.

    To create and switch between workspaces, you can use the following commands:
- **Create a new workspace:**
```
terraform workspace new <workspace-name>
- **List existing workspaces:**
```
terraform workspace list
- **Switch to an existing workspace:**
```
terraform workspace select <workspace-name>
```
    Workspaces are particularly useful for managing environments that share the same infrastructure code but require different configurations or state management. For example, you can have separate workspaces for development, staging, and production, allowing you to test changes in one environment without affecting others. 

55. What is `terraform import`?

    Ans: `terraform import` is a command that allows you to bring existing infrastructure resources into Terraform's management. It enables you to import resources that were created outside of Terraform (e.g., manually through the cloud provider's console or CLI) into your Terraform state file, allowing you to manage them using Terraform configuration files.

    The basic syntax for importing a resource is as follows:
```
terraform import <resource_type>.<resource_name> <resource_id>
```
    For example, to import an existing AWS EC2 instance into Terraform, you would use:
```
terraform import aws_instance.example i-1234567890abcdef0
    After importing the resource, you will need to create the corresponding Terraform configuration for that resource in
    your `.tf` files to ensure that Terraform can manage it properly. The imported resource will now be tracked in the Terraform state, and you can make changes to it using Terraform commands.
```

56. How do you structure a Terraform project?

    Ans: Structuring a Terraform project involves organizing your configuration files, modules, and state management to ensure maintainability, scalability, and clarity. Here are some best practices for structuring a Terraform project:
- **Directory Structure:** Organize your project into directories based on environments, modules, or components
. For example:
```
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── staging/
│   │   ├── main.tf
│   │   ├── variables.tf    
│   │   └── outputs.tf
│   └── prod/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── modules/
│   ├── network/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── compute/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
- **Use Modules:** Create reusable modules for common infrastructure components (e.g., VPC, EC2 instances, RDS databases) to promote code reuse and maintainability. Modules can be stored in a separate `modules` directory or published to a module registry for sharing across projects.
- ** State Management:** Use remote state backends (e.g., S3 with DynamoDB for locking) to store and manage your Terraform state files securely. This allows multiple team members to collaborate on the same infrastructure without conflicts and ensures that the state is versioned and backed up.
- **Variables and Outputs:** Define variables in `variables.tf` files to parameterize your configurations and make them flexible. Use `outputs.tf` files to expose important information about your infrastructure, such as resource IDs or endpoints, that can be consumed by other modules or applications.
- **Environment-Specific Configurations:** Use separate configuration files or workspaces for different environments (e.g., development, staging, production) to isolate changes and manage environment-specific settings. This allows you to test changes in one environment without affecting others.
```

57. What is GitOps?

    Ans: GitOps is a modern approach to continuous delivery and infrastructure management that leverages Git as the single source of truth for declarative infrastructure and application configurations. In a GitOps workflow, all changes to the infrastructure and application state are made through pull requests in a Git repository. The desired state of the system is defined in code, and automated processes continuously reconcile the actual state of the system with the desired state stored in Git.

    Key principles of GitOps include:
- **Declarative Configuration:** Infrastructure and application configurations are defined in a declarative manner, specifying the desired state rather than the steps to achieve it. This allows for easier versioning, auditing, and rollback of changes.
- **Version Control:** Git serves as the single source of truth for all
    configurations, enabling teams to track changes, collaborate, and maintain a history of modifications.
- **Automated Reconciliation:** Continuous reconciliation processes (e.g., using tools like Argo CD or Flux) monitor the Git repository for changes and automatically apply them to the target environment, ensuring that the actual state matches the desired state.
- **Observability and Auditing:** GitOps provides visibility into the state of the system,
    allowing teams to audit changes, track deployments, and identify issues quickly. By using Git as the source of truth, teams can easily roll back to previous configurations if needed.

58. Explain Helm charts.

    Ans: Helm is a package manager for Kubernetes that simplifies the deployment and management of applications by using Helm charts. A Helm chart is a collection of files that describe a related set of Kubernetes resources, such as deployments, services, config maps, and secrets. Charts allow you to define, install, and upgrade applications in a consistent and repeatable manner.

    Key components of a Helm chart include:
- **Chart.yaml:** This file contains metadata about the chart, such as its name, version, description, and dependencies. It serves as the entry point for the chart and provides essential information for managing the application.
- **values.yaml:** This file contains default configuration values for the chart. Users can override these values during installation or upgrade to customize the deployment according to their needs. The values.yaml file allows for flexibility and reusability of the chart across different environments.
- **templates/**: This directory contains the Kubernetes resource templates that define the desired state of the application. The templates use the Go templating language to dynamically generate Kubernetes manifests based on the values provided in the values.yaml file.
- **charts/**: This directory can contain sub-charts, which are Helm charts that are dependencies of the main chart. Sub-charts allow for modularity and reusability of components across different applications.
- **README.md:** This file provides documentation and usage instructions for the chart, helping users understand how to deploy and configure the application.

59. What is a sidecar container?

    Ans: A sidecar container is a design pattern in Kubernetes where an additional container runs alongside the main application container within the same pod. The sidecar container extends or enhances the functionality of the main application by providing auxiliary services, such as logging, monitoring, proxying, or configuration management. Sidecar containers share the same network namespace and storage volumes as the main container, allowing them to communicate and collaborate effectively.

    Common use cases for sidecar containers include:
- **Logging and Monitoring:** A sidecar container can collect logs or metrics from the main application container and forward them to a centralized logging or monitoring system.
- **Service Proxying:** A sidecar container can act as a reverse proxy or service mesh sidecar, handling traffic routing, load balancing, and service discovery for the main application.
- ** Configuration Management:** A sidecar container can manage configuration files or secrets for the main application, ensuring that they are up-to-date and securely injected into the application at runtime.
- **Security and Authentication:** A sidecar container can handle authentication, authorization, or encryption tasks for the main application, providing an additional layer of security without modifying the main application code.

60. How do you handle logging in containers?

    Ans: Handling logging in containers involves capturing, storing, and analyzing log data generated by applications running within containers. Here are some best practices for managing logs in containerized environments:
- **Use Standard Output and Error:** Configure your application to write logs to standard output (stdout) and standard error (stderr) streams. This allows the container runtime (e.g., Docker, Kubernetes) to capture and manage the logs effectively.
- **Centralized Logging:** Implement a centralized logging solution to aggregate logs from multiple containers and services. Tools like Elasticsearch, Logstash, Kibana (ELK stack), Fluentd, or Loki can be used to collect, store, and visualize logs from different sources in a unified manner.
- **Log Rotation and Retention:** Set up log rotation and retention policies to manage log file sizes and prevent disk space exhaustion. This can be achieved using tools like logrotate or by configuring the logging driver in the container runtime to handle log rotation automatically.
- **Structured Logging:** Use structured logging formats (e.g., JSON) to make it easier to parse and analyze log data. Structured logs can be enriched with metadata, such as timestamps, log levels, and contextual information, which can help in troubleshooting and monitoring.
- **Monitoring and Alerting:** Integrate logging with monitoring and alerting systems to detect anomalies, errors, or performance issues in real-time. This allows you to proactively respond to issues and maintain the health of your applications.

## LTIMindtree / Tech Mahindra / Mphasis (service — CI/CD, automation)
61. 🔥 Walk through a Jenkins or GitHub Actions pipeline you built.

    Ans: A Jenkins or GitHub Actions pipeline is a series of automated steps that define the process of building, testing, and deploying an application. Here’s a walkthrough of a typical CI/CD pipeline I built using GitHub Actions:
1. **Trigger:** The pipeline is triggered by a push or pull request to the main branch of the repository. This ensures that any changes to the codebase initiate the CI/CD process.
2. **Checkout Code:** The first step in the pipeline is to check out the code from the repository using the `actions/checkout` action. This allows the pipeline to access the latest code for building and testing.
3. **Set Up Environment:** The next step is to set up the required environment for the application. This may include installing dependencies, setting up environment variables, and configuring any necessary tools or services.
4. **Build:** The build step compiles the application code and generates any necessary artifacts. This may involve running build scripts, compiling source code, or packaging the application into a deployable format (e.g., Docker image, JAR file).
5. **Test:** The test step runs automated tests to validate the functionality and quality of the application. This may include unit tests, integration tests, and end-to-end tests. Test results are collected and reported to ensure that any issues are identified early in the development process.
6. **Static Code Analysis:** The pipeline may include a static code analysis step using tools like SonarQube or ESLint to check for code quality, security vulnerabilities, and adherence to coding standards. This helps maintain a high level of code quality and reduces the risk of introducing bugs or security issues.
7. **Build Artifacts:** If the build and tests are successful, the pipeline generates build artifacts (e.g., Docker images, JAR files) and stores them in an artifact repository (e.g., GitHub Packages, Nexus, Artifactory) for later deployment.
8. **Deploy:** The final step in the pipeline is to deploy the application to the target environment (e.g., staging, production). This may involve deploying a Docker image to a Kubernetes cluster, updating a serverless function, or deploying to a cloud service. Deployment can be automated using tools like Terraform, Ansible, or Helm, depending on the infrastructure and application architecture.
9. **Notification:** After the deployment, the pipeline sends notifications (e.g., via email, Slack, or Microsoft Teams) to inform the team about the status of the build and deployment process. This helps keep the team informed and allows for quick action in case of any issues.
10. **Monitoring and Rollback:** Post-deployment, the pipeline may include monitoring steps to ensure that the application is running as expected. If any issues are detected, the pipeline can trigger an automated rollback to the previous stable version of the application to minimize downtime and impact on users.

62. How do you run quality gates (SonarQube) in CI?

    Ans: Running quality gates in CI using SonarQube involves integrating SonarQube analysis into your CI/CD pipeline to assess code quality and enforce quality standards. Here’s how to set up and run quality gates in a CI pipeline:
1. **Set Up SonarQube:** Install and configure a SonarQube server, either on-premises or using a cloud-based service. Create a project in SonarQube for your application and configure the necessary settings, such as quality gate thresholds and rules.
2. ** Install SonarQube Scanner:** Add the SonarQube Scanner to your CI/CD pipeline. This can be done by installing the SonarQube Scanner CLI or using a plugin for your CI/CD tool (e.g., Jenkins, GitHub Actions, GitLab CI). The scanner is responsible for analyzing the code and sending the results to the SonarQube server.
3. **Configure the CI/CD Pipeline:** In your CI/CD pipeline configuration (e.g., Jenkinsfile, GitHub Actions workflow), add a step to run the SonarQube analysis. This typically involves executing the SonarQube Scanner command with the appropriate parameters, such as the project key, authentication token, and source code directory. For example, in a GitHub Actions workflow:
```yaml
- name: SonarQube Analysis
  uses: sonarsource/sonarcloud-github-action@v1
  with:
    projectKey: your_project_key
    organization: your_organization
    token: ${{ secrets.SONAR_TOKEN }}
4. **Run the Pipeline:** Trigger the CI/CD pipeline by pushing code changes or creating a pull request. The SonarQube analysis step will run as part of the pipeline, analyzing the code and sending the results to the SonarQube server.
5. **Check Quality Gate Results:** After the analysis is complete, check the SonarQube dashboard for the quality gate results. The quality gate will indicate whether the code meets the defined quality standards or if there are issues that need to be addressed. If the quality gate fails, the pipeline can be configured to fail the build, preventing the code from being merged or deployed until the issues are resolved.
6. **Address Issues:** If the quality gate fails, review the issues reported by SonarQube and make the necessary code changes to address them. This may involve fixing bugs, improving code quality, or adhering to coding standards. After making the changes, rerun the pipeline to ensure that the quality gate passes before proceeding with the deployment.
```

63. GitFlow vs trunk-based — which and why?

    Ans: GitFlow and trunk-based development are two different branching strategies used in version control systems like Git, each with its own advantages and use cases.
- **GitFlow:** GitFlow is a branching model that uses multiple long-lived branches to manage the development and release process. It typically includes branches for features, releases, hotfixes, and the main development branch (usually called `develop`). GitFlow is well-suited for projects with a structured release cycle, where features are developed in isolation and merged into the main branch for release. It provides a clear separation of concerns and allows for parallel development of features and bug fixes. However, it can introduce complexity and overhead in managing multiple branches, especially in fast-paced development environments.
- **Trunk-Based Development:** Trunk-based development is a simpler branching strategy that encourages developers to work on a single main branch (often called `trunk` or `main`) and make frequent, small commits. Feature branches are short-lived and merged back into the main branch quickly, often multiple times a day. This approach promotes continuous integration, reduces merge conflicts, and encourages collaboration among team members. Trunk-based development is well-suited for agile and DevOps practices, where rapid iteration and continuous delivery are prioritized. It allows for faster feedback, easier code reviews, and a more streamlined development process.
In summary, the choice between GitFlow and trunk-based development depends on the project's requirements, team size, and development practices. GitFlow may be preferred for projects with a structured release cycle and multiple teams working on different features, while trunk-based development is ideal for fast-paced, collaborative environments that prioritize continuous integration and delivery.

64. How do you implement automated rollback?

    
    Ans: Implementing automated rollback in a CI/CD pipeline involves setting up mechanisms to revert to a previous stable version of the application or infrastructure in case of deployment failures or issues detected post-deployment. Here’s how to implement automated rollback:
1. **Versioning and Artifact Management:** Ensure that your build artifacts (e.g., Docker images, JAR files) are versioned and stored in an artifact repository (e.g., Nexus, Artifactory, Docker Registry). This allows you to easily identify and retrieve previous stable versions of the application for rollback purposes.
2. **Health Checks and Monitoring:** Implement health checks and monitoring for your application to detect issues after deployment. This can include application-level health endpoints, performance metrics, and error monitoring tools (e.g., Prometheus, Grafana, New Relic). Set up alerts to notify the team of any failures or anomalies that may require a rollback.
3. **Rollback Strategy:** Define a rollback strategy based on the deployment method and infrastructure. For example, in a Kubernetes environment, you can use rolling updates with a rollback option, or in a serverless environment, you can deploy a previous version of the function. Ensure that the rollback process is automated and can be triggered based on specific conditions (e.g., failed health checks, high error rates).
4. **Pipeline Configuration:** In your CI/CD pipeline configuration (e.g., Jenkinsfile, GitHub Actions workflow), add steps to handle rollback. This may involve checking the health of the deployed application, and if issues are detected, triggering the rollback process to revert to the previous stable version. For example, in a GitHub Actions workflow:
```yaml
- name: Check Application Health
  run: |
    # Run health checks and set a status variable
    if [ "$HEALTH_CHECK_FAILED" = true ]; then
      echo "Deployment failed, initiating rollback..."
      # Trigger rollback to previous stable version
      # e.g., kubectl rollout undo deployment/my-app
    fi
5. **Testing Rollback:** Regularly test the rollback process in a staging or test environment to ensure that it works as expected and can be executed quickly in case of a production issue. This helps identify any potential issues with the rollback process and ensures that the team is familiar with the steps involved.
6. **Documentation and Communication:** Document the rollback process and communicate it to the team. Ensure that all team members are aware of the rollback procedures and know how to execute them in case of an emergency. This includes providing clear instructions on how to trigger the rollback, what artifacts to use, and any dependencies or configurations that need to be considered during the rollback process.
```

65. What branching strategy do you follow?

    Ans: The branching strategy I follow depends on the project requirements, team size, and development practices. However, I typically prefer a trunk-based development approach for most projects due to its simplicity and focus on continuous integration and delivery. Here’s how I implement trunk-based development:
1. **Single Main Branch:** I maintain a single main branch (often called `main` or `trunk`) where all development work is integrated. This branch serves as the source of truth for the application and is always kept in a deployable state.
2. **Short-Lived Feature Branches:** Developers create short-lived feature branches for new features, bug fixes, or improvements. These branches are created from the main branch and are merged back into the main branch as soon as the work is complete and tested. This encourages frequent integration and reduces the risk of merge conflicts.
3. **Frequent Commits and Pull Requests:** Developers are encouraged to make small, frequent commits to their feature branches and submit pull requests for code review. This allows for faster feedback, easier code reviews, and quicker integration of changes into the main branch. It also promotes collaboration and knowledge sharing among team members.
4. **Continuous Integration:** I set up a CI/CD pipeline that automatically builds, tests, and deploys the application whenever changes are pushed to the main branch. This ensures that the application is always in a deployable state and allows for rapid iteration and delivery of new features. The pipeline includes automated tests, static code analysis, and deployment steps to ensure that the code meets quality standards before being deployed to production.

66. How do you cache dependencies in CI?

    Ans: Caching dependencies in CI/CD pipelines is an effective way to speed up build times and reduce the time spent downloading and installing dependencies for each build. Here’s how to implement dependency caching in a CI pipeline:
1. **Identify Dependencies:** Determine which dependencies are required for your application and can be cached. This may include package managers (e.g., npm, pip, Maven, Gradle) and their associated lock files (e.g., package-lock.json, requirements.txt, pom.xml). These files define the specific versions of dependencies that need to be installed, ensuring consistency across builds.
2. **Configure Caching in the CI/CD Tool:** Most CI/CD tools provide built-in support for caching dependencies. For example, in GitHub Actions, you can use the `actions/cache` action to cache dependencies. In Jenkins, you can use plugins or custom scripts to manage caching. Here’s an example of caching dependencies in a GitHub Actions workflow:
```yaml
- name: Cache Node.js dependencies
  uses: actions/cache@v2
  with:
    path: ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
```
3. **Restore Cache:** Before installing dependencies, check if a cache exists for the current build. If a cache is found, restore it to avoid downloading dependencies again. This can significantly reduce build times, especially for large projects with many dependencies.

67. What is a reusable workflow in GitHub Actions?

    Ans: A reusable workflow in GitHub Actions is a workflow that can be defined once and then invoked by other workflows across different repositories or within the same repository. This allows for the centralization of common CI/CD processes, promoting code reuse, consistency, and maintainability. Reusable workflows are defined in a separate YAML file and can be called using the `workflow_call` event.

    Key features of reusable workflows include:
- **Centralized Logic:** Reusable workflows allow you to define common build, test, or deployment steps in a single location, reducing duplication and ensuring that best practices are consistently applied across multiple workflows.
- **Parameters and Inputs:** Reusable workflows can accept inputs and parameters, allowing you to customize their behavior based on the context in which they are called. This makes them flexible and adaptable to different use cases.
- **Versioning:** You can version reusable workflows by using tags or branches, allowing you to control which version of the workflow is used in different contexts. This helps manage changes and ensures that updates to the reusable workflow do not inadvertently break dependent workflows.
- **Invocation:** To invoke a reusable workflow, you can use the `uses` keyword in another workflow file, specifying the path to the reusable workflow and any required inputs. For example:
```yaml
jobs:
  call-reusable-workflow:
    uses: owner/repo/.github/workflows/reusable-workflow.yml@v1
    with:
      input1: value1
      input2: value2
```

68. How do you trigger a pipeline on a schedule?

    Ans: To trigger a pipeline on a schedule, you can use the scheduling features provided by your CI/CD tool. Most CI/CD platforms support cron-like syntax to define scheduled triggers. Here’s how to set up scheduled triggers in popular CI/CD tools:
- **GitHub Actions:** You can use the `schedule` event in your workflow YAML file to define a cron schedule. For example, to run a workflow every day at midnight:
```yaml
on:
  schedule:
    - cron: '0 0 * * *' # Runs at midnight UTC every day
- **Jenkins:** In Jenkins, you can configure a job to run on a schedule using the "Build Triggers" section. You can specify a cron expression to define the schedule. For example, to run a job every day at midnight, you would enter `H 0 * * *` in the "Build periodically" field.
- **GitLab CI/CD:** In GitLab, you can create a scheduled pipeline by navigating to the "CI/CD" section of your project, selecting "Schedules," and defining a new schedule with a cron expression. You can specify the branch to run the pipeline on and any variables needed for the scheduled run.
- **CircleCI:** In CircleCI, you can define scheduled workflows in the `.circleci/config.yml` file using the `triggers` key. For example, to run a workflow every day at midnight:
```yaml
workflows:
  version: 2
  scheduled_workflow:
    triggers:
      - schedule:
          cron: "0 0 * * *" # Runs at midnight UTC every day
```
69. Explain artifact promotion across environments.

    Ans: Artifact promotion across environments is the process of moving build artifacts (e.g., binaries, Docker images, configuration files) from one environment to another in a controlled and systematic manner. This practice is commonly used in CI/CD pipelines to ensure that the same tested and validated artifacts are deployed across different stages of the software development lifecycle, such as development, staging, and production.

    Key steps in artifact promotion include:
1. **Build and Test:** The CI/CD pipeline starts by building the application and running automated tests to ensure that the artifacts meet quality standards. This may include unit tests, integration tests, and static code analysis. Once the build is successful and tests pass, the artifacts are generated and stored in an artifact repository (e.g., Nexus, Artifactory, Docker Registry).
2. **Artifact Storage:** The generated artifacts are stored in a centralized artifact repository, which serves as a single source of truth for all environments. The repository allows for versioning, access control, and traceability of artifacts, ensuring that the same artifacts can be promoted across different environments without discrepancies.
3. **Promotion Process:** The promotion process involves moving the artifacts from one environment to another (e.g., from development to staging, and then to production) based on predefined criteria. This can be done manually or automatically, depending on the organization's policies and the CI/CD pipeline configuration. The promotion process may include additional testing, validation, or approval steps to ensure that the artifacts are suitable for deployment in the target environment.
4. **Deployment:** Once the artifacts are promoted to the target environment, they are deployed using automated deployment tools or scripts. The deployment process may involve updating configuration files, applying database migrations, or restarting services to ensure that the application is running correctly in the new environment. Monitoring and logging should be in place to track the deployment process and detect any issues that may arise during or after the deployment.
5. **Rollback and Version Control:** In case of issues during deployment or after promotion, the CI/CD pipeline should have a rollback mechanism in place to revert to the previous stable version of the artifacts. Version control and proper tagging of artifacts in the repository allow for easy identification and retrieval of previous versions, ensuring that the system can be restored to a known good state if necessary.

70. How do you secure credentials in Jenkins/GitHub Actions?

    Ans: Securing credentials in Jenkins and GitHub Actions is crucial to protect sensitive information, such as API keys, passwords, and tokens, from unauthorized access. Here’s how to secure credentials in both platforms:
- **Jenkins:**
1. **Use Jenkins Credentials Plugin:** Install and configure the Jenkins Credentials Plugin to securely store and manage credentials. This plugin allows you to create and manage credentials in a centralized manner, making them available to jobs and pipelines without exposing them in the code.
2. **Store Credentials in Jenkins:** Add credentials (e.g., username/password, secret text, SSH keys) in the Jenkins credentials store.
3. **Access Credentials in Pipelines:** In your Jenkins pipeline (e.g., Jenkinsfile), use the `withCredentials` block to access the stored credentials securely. For example:
```groovy
withCredentials([usernamePassword(credentialsId: 'my-credentials-id', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
    // Use USERNAME and PASSWORD in your build steps
}
```
4. **Restrict Access:** Limit access to the Jenkins credentials store by configuring role-based access control (RBAC) and ensuring that only authorized users and jobs can access sensitive credentials.
- ** GitHub Actions:**
1. **Use GitHub Secrets:** Store sensitive information in GitHub Secrets, which are encrypted and can be accessed securely in workflows. Navigate to the repository settings, select "Secrets and variables," and add your secrets (e.g., API keys, tokens) there.
2. **Access Secrets in Workflows:** In your GitHub Actions workflow YAML file, access the secrets using the `${{ secrets.SECRET_NAME }}` syntax. For example:
```yaml
- name: Use Secret
  run: echo "Using secret: ${{ secrets.MY_SECRET }}"
```
3. **Limit Secret Exposure:** Avoid printing secrets in logs or exposing them in any way. Use them only in the necessary steps of the workflow. Additionally, consider using environment variables or temporary credentials to minimize the risk of exposure.
4. **Rotate Secrets Regularly:** Implement a process for rotating secrets regularly to reduce the risk of compromise. Update the secrets in GitHub and Jenkins as needed, and ensure that any applications or services using those secrets are updated accordingly.

## Accenture / Deloitte / EY (consulting — design + governance)
71. 🔥 Design a CI/CD pipeline for a microservices app.

    Ans: Designing a CI/CD pipeline for a microservices application involves creating a series of automated steps that facilitate the building, testing, and deployment of multiple services independently. Here’s a high-level design for such a pipeline:
1. **Source Code Management:** Use a version control system (e.g., Git) to manage the source code for each microservice. Each microservice should have its own repository or be organized in a monorepo with clear directory structures.
2. **CI/CD Tool Selection:** Choose a CI/CD tool (e.g., Jenkins, GitHub Actions, GitLab CI/CD) that supports parallel builds and deployments for multiple services. Ensure that the tool can handle the complexity of managing multiple microservices and their dependencies.
3. **Pipeline Structure:** Create a separate pipeline for each microservice, allowing for independent builds and deployments. Each pipeline should include the following stages:
   - **Build Stage:** Compile the code, run unit tests, and package the microservice into a deployable artifact (e.g., Docker image, JAR file). Use a build tool (e.g., Maven, Gradle, npm) appropriate for the technology stack of the microservice.
   - **Test Stage:** Run integration tests, end-to-end tests, and static code analysis to ensure the quality and functionality of the microservice. Use testing frameworks and tools that are compatible with the microservice’s technology stack.
   - **Artifact Storage:** Store the built artifacts in a centralized artifact repository (e.g., Nexus, Artifactory, Docker Registry) for versioning and traceability. This allows for easy retrieval of artifacts for deployment across different environments.
   - **Deployment Stage:** Deploy the microservice to the target environment (e.g., development, staging, production) using automated deployment scripts or tools. Implement strategies like blue-green deployments or canary releases to minimize downtime and reduce risk.

72. How do you enforce tagging and cost governance?

    Ans: Enforcing tagging and cost governance involves implementing policies and automation to ensure that all resources are properly tagged with relevant metadata (e.g., project, environment, owner) and monitoring usage and costs. This can be achieved using tools like AWS Tag Policies, AWS Config, and cost allocation reports to track and manage resource usage and expenses effectively.

73. How do you implement least-privilege IAM at scale? (SCPs, boundaries)

    Ans: Implementing least-privilege IAM at scale involves defining and enforcing access controls that grant users and services only the permissions necessary to perform their tasks. This can be achieved using AWS Organizations, Service Control Policies (SCPs), IAM policies, and permission boundaries. By organizing accounts into organizational units (OUs) and applying SCPs, you can restrict access to specific services and actions across multiple accounts. Additionally, using permission boundaries allows you to set limits on the maximum permissions a user or role can have, ensuring that they cannot exceed their intended access level.

74. What is AWS Organizations? Why multi-account?

    
    Ans: AWS Organizations is a service that allows you to centrally manage and govern multiple AWS accounts within an organization. It provides features for account management, consolidated billing, and policy enforcement across accounts. Multi-account strategies are beneficial for isolating workloads, improving security, managing costs, and enabling better resource allocation. By using multiple accounts, you can separate environments (e.g., development, staging, production), apply different security policies, and track costs more effectively.

75. How do you ensure compliance (CIS, PCI) in infra?

    Ans: Ensuring compliance with standards like CIS (Center for Internet Security) and PCI (Payment Card Industry) in infrastructure involves implementing security best practices, continuous monitoring, and automated compliance checks. This can be achieved using tools like AWS Config, AWS Security Hub, and third-party compliance solutions to assess the configuration of resources against established benchmarks. Regular audits, vulnerability scanning, and remediation processes should be in place to maintain compliance. Additionally, implementing Infrastructure as Code (IaC) with predefined security policies can help enforce compliance during the provisioning of resources.

76. Explain disaster recovery strategies and RTO/RPO.

    Ans: Disaster recovery (DR) strategies involve planning and implementing measures to ensure business continuity in the event of a disaster or system failure. Key components of DR strategies include:

77. How do you manage secrets across many teams?

    Ans: Managing secrets across many teams involves using centralized secret management solutions that provide secure storage, access control, and auditing capabilities. Tools like HashiCorp Vault, AWS Secrets Manager, and Azure Key Vault allow teams to store, retrieve, and rotate secrets securely. Access to secrets can be controlled using fine-grained policies, and secrets can be injected into applications at runtime without hardcoding them in source code.

78. What is policy-as-code? (OPA, Sentinel)

    Ans: Policy-as-code is an approach to defining and enforcing policies using code, allowing for automated and consistent policy management across infrastructure and applications. Tools like Open Policy Agent (OPA) and HashiCorp Sentinel enable organizations to write policies in a declarative language, which can be version-controlled, tested, and integrated into CI/CD pipelines. This approach ensures that policies are applied consistently, reduces human error, and allows for automated compliance checks.

79. How do you handle drift at an enterprise scale?

    Ans: Handling drift at an enterprise scale involves implementing continuous monitoring and automated remediation processes to detect and correct configuration drift in infrastructure. This can be achieved using Infrastructure as Code (IaC) tools like Terraform, AWS CloudFormation, or Ansible, which allow for version-controlled infrastructure definitions. Regular audits and drift detection tools can identify discrepancies between the desired state and the actual state of resources. Automated remediation scripts or policies can then be triggered to bring resources back into compliance with the defined configurations.

80. How do you do capacity planning?

    Ans: Capacity planning involves forecasting future resource requirements based on historical usage patterns, business growth, and anticipated workload changes. This process includes analyzing metrics such as CPU, memory, storage, and network utilization to determine the current capacity and identify potential bottlenecks. Tools like AWS CloudWatch, Azure Monitor, and Google Cloud Monitoring can provide insights into resource usage trends. Based on this analysis, organizations can make informed decisions about scaling infrastructure, optimizing resource allocation, and ensuring that sufficient capacity is available to meet future demands.

## Comcast / PayPal / Walmart (product — depth, scale, SRE)
81. 🔥 How does a request reach a pod end-to-end? (Ingress→Service→kube-proxy→pod)

    Ans: When a request reaches a pod in a Kubernetes cluster, it goes through several components in the following order:
1. **Ingress Controller:** The request first hits the Ingress controller, which is responsible for routing external traffic to the appropriate service within the cluster based on defined Ingress rules. The Ingress controller can handle SSL termination, load balancing, and path-based routing.
2. **Service:** The Ingress controller forwards the request to the appropriate Kubernetes Service, which acts as an abstraction layer that defines a logical set of pods and provides a stable endpoint (IP address and port) for accessing those pods. The Service uses label selectors to identify the pods that belong to it.
3. **kube-proxy:** The Service forwards the request to the kube-proxy, which is responsible for maintaining network rules on each node in the cluster. The kube-proxy uses either iptables or IPVS to route the request to one of the pods that match the Service's label selector. It performs load balancing to distribute incoming requests across the available pods.
4. **Pod:** Finally, the request reaches the selected pod, where it is processed by the application running inside the container. The pod handles the request, performs the necessary operations, and sends back a response through the same path in reverse order, ultimately returning the response to the client that initiated the request.

82. 🔥 How does Kubernetes self-healing + HPA work internally?

    Ans: Kubernetes self-healing and Horizontal Pod Autoscaler (HPA) work together to ensure that applications running in a cluster remain available and can scale based on demand. Here’s how they work internally:
1. **Self-Healing:** Kubernetes continuously monitors the health of pods and nodes in the cluster
. If a pod becomes unhealthy or fails, the Kubernetes control plane detects the issue through liveness and readiness probes. The control plane then automatically reschedules the pod on a healthy node, ensuring that the desired number of replicas is maintained. This self-healing mechanism helps maintain application availability and resilience.
2. **Horizontal Pod Autoscaler (HPA):** HPA automatically adjusts the number of
    pod replicas based on observed metrics, such as CPU utilization or custom metrics. The HPA controller continuously monitors the specified metrics for the target deployment or replica set. When the observed metric exceeds the defined threshold, the HPA increases the number of replicas to handle the increased load. Conversely, when the metric falls below the threshold, the HPA reduces the number of replicas to optimize resource usage. This dynamic scaling ensures that applications can handle varying workloads efficiently while maintaining performance and cost-effectiveness.

83. StatefulSet vs Deployment — when stable identity/storage?

    
    Ans: In Kubernetes, StatefulSet and Deployment are two different types of controllers used to manage the lifecycle of pods, each serving different use cases based on the requirements for stable identity and storage.

84. How do you do canary deployments with metrics?

    Ans: Canary deployments involve releasing a new version of an application to a small subset of users or traffic before rolling it out to the entire user base. This allows for testing the new version in production while minimizing risk. To implement canary deployments with metrics, follow these steps:
1. **Set Up Metrics Collection:** Use monitoring tools (e.g., Prometheus, Grafana, Datadog) to collect relevant metrics for both the current version and the canary version of the application. Metrics may include response time, error rates, CPU/memory usage, and user engagement.
2. **Deploy Canary Version:** Deploy the new version of the application to a small percentage of the user base or traffic. This can be done using feature flags, routing rules, or load balancers to direct a portion of traffic to the canary version while the majority of traffic continues to go to the stable version.
3. **Monitor Metrics:** Continuously monitor the metrics for both the stable and canary versions. Compare the performance, error rates, and other key indicators to determine if the canary version is performing as expected. Set up alerts to notify the team if any metrics exceed predefined thresholds, indicating potential issues with the canary deployment.
4. **Analyze Results:** After a sufficient observation period, analyze the collected metrics to assess the performance and stability of the canary version. If the canary version meets the desired criteria and shows no significant issues, it can be promoted to the stable version for all users. If issues are detected, the canary deployment can be rolled back to the previous stable version, minimizing the impact on users.

85. 🔥 Explain SLI, SLO, SLA, and error budgets.

    Ans: SLI (Service Level Indicator), SLO (Service Level Objective), SLA (Service Level Agreement), and error budgets are key concepts in Site Reliability Engineering (SRE) that help organizations define, measure, and manage the reliability of their services.
- **SLI (Service Level Indicator):** An SLI is a quantitative measure of a specific aspect of a service's performance or reliability. It is typically expressed as a percentage or ratio and is used to track the performance of a service against defined objectives. Common SLIs include availability, latency, error rate, and throughput. For example, an SLI for availability might be defined as the percentage of successful requests over a given time period.
- **SLO (Service Level Objective):** An SLO is a target or goal for a specific SLI that defines the desired level of service performance. It represents the acceptable threshold for a service's performance and is used to set expectations for both the service provider and the users. For example, an SLO for availability might be set at 99.9%, meaning that the service should be available for 99.9% of the time over a specified period. SLOs help organizations prioritize reliability efforts and make informed decisions about resource allocation and risk management.
- **SLA (Service Level Agreement):** An SLA is a formal agreement between a service provider and its customers that outlines the expected level of service performance, including specific SLIs, SLOs, and any associated penalties or remedies in case of non-compliance.

86. How do you reduce MTTR? Walk through incident response.

    Ans: Reducing Mean Time to Recovery (MTTR) involves implementing effective incident response processes, monitoring, and automation to quickly identify, diagnose, and resolve issues. Here’s a walkthrough of an incident response process to reduce MTTR:
1. **Detection and Alerting:** Implement robust monitoring and alerting systems to detect incidents as early as possible. Use tools like Prometheus, Grafana, Datadog, or New Relic to monitor application performance, infrastructure health, and key metrics. Set up alerts for anomalies, errors, or threshold breaches to notify the relevant teams immediately.
2. **Incident Triage:** When an alert is received, perform an initial triage to assess the severity and impact of the incident. Determine whether it is a critical issue that requires immediate attention or a lower-priority problem that can be addressed later. Assign the incident to the appropriate team or individual based on their expertise and the nature of the issue. Document the incident details, including the time of occurrence, affected systems, and any relevant logs or metrics.
3. **Investigation and Diagnosis:** Conduct a thorough investigation to identify the root cause of the incident. Analyze logs, metrics, and traces to gather information about the issue. Use debugging tools, profiling, and monitoring dashboards to pinpoint the source of the problem. Collaborate with team members to share insights and findings, and consider using a structured approach like the "Five Whys" technique to uncover the underlying cause of the incident.
4. **Mitigation and Resolution:** Once the root cause is identified, implement mitigation strategies to minimize the impact of the incident. This may involve rolling back a deployment, applying a hotfix, or rerouting traffic to healthy instances. Ensure that the resolution is tested and validated before fully restoring services. Communicate with stakeholders and affected users about the status of the incident and any expected downtime or service interruptions.

87. How do you debug high p99 latency?

    Ans: Debugging high p99 latency involves identifying and addressing the root causes of performance issues that affect the 99th percentile of response times. Here’s a systematic approach to debug high p99 latency:
1. **Monitor and Collect Metrics:** Use monitoring tools (e.g., Prometheus, Grafana, Datadog) to collect detailed metrics on response times, request rates, error rates, and resource utilization. Focus on the p99 latency metric to understand the distribution of response times and identify patterns or anomalies.
2. **Analyze Logs and Traces:** Review application logs and distributed traces to identify slow requests and potential bottlenecks. Use tools like ELK Stack (Elasticsearch, Logstash, Kibana), Jaeger, or Zipkin to visualize and analyze traces, which can help pinpoint the specific services or components contributing to high latency. Look for patterns such as specific endpoints, user actions, or time periods that correlate with increased latency.
3. **Identify Bottlenecks:** Investigate potential bottlenecks in the system, such as database queries, external API calls, or resource contention. Use profiling tools to analyze CPU, memory, and I/O usage, and identify any components that may be causing delays. Consider factors like network latency, thread contention, and garbage collection pauses that may impact performance.
4. **Optimize Code and Infrastructure:** Based on the findings, optimize the code, database queries, or infrastructure to reduce latency. This may involve refactoring inefficient code, optimizing database indexes, implementing caching strategies, or scaling resources to handle increased load. Test the changes in a staging environment before deploying them to production to ensure that they effectively reduce p99 latency without introducing new issues.
5. **Continuous Monitoring and Feedback:** After implementing optimizations, continue to monitor p99 latency and other performance metrics to ensure that the changes have a positive impact. Set up alerts for any future spikes in latency and establish a feedback loop to continuously improve performance. Regularly review and update the monitoring and alerting configurations.

88. What are the golden signals? RED vs USE.

    Ans: The golden signals are a set of key metrics that are critical for monitoring the health and performance of a system. They help identify issues and provide insights into the overall reliability of services. The two commonly referenced frameworks for golden signals are RED (Rate, Errors, Duration) and USE (Utilization, Saturation, Errors).

89. How do you design multi-region failover?

    Ans: Designing multi-region failover involves creating a resilient architecture that can handle failures in one region by automatically redirecting traffic to another region. Here’s a high-level approach to designing multi-region failover:
1. **Active-Active vs Active-Passive:** Decide whether to use an active-active or active-passive failover strategy. In an active-active setup, both regions handle traffic simultaneously, while in an active-passive setup, one region is primary and the other is on standby.
2. **Data Replication:** Implement data replication between regions to ensure that data is synchronized and available in both locations. Use database replication, distributed file systems, or cloud-native services that support cross-region replication. Ensure that the replication strategy meets the required RPO (Recovery Point Objective) and RTO (Recovery Time Objective) for your application.
3. **Traffic Routing:** Use DNS-based routing or global load balancers to direct traffic to the appropriate region based on availability and health checks. Configure health checks to monitor the status of each region and automatically reroute traffic in case of a failure.

90. 🔥 How do you keep secrets out of source and inject at deploy? (Vault, OIDC)

    Ans: Keeping secrets out of source code and injecting them at deploy time is essential for maintaining security and preventing unauthorized access. Here’s how to achieve this using tools like HashiCorp Vault and OpenID Connect (OIDC):
1. **Use a Secret Management Tool:** Implement a secret management tool like HashiCorp Vault
    to securely store and manage secrets. Vault provides features such as dynamic secrets, access control policies, and audit logging to ensure that secrets are protected and only accessible to authorized users and applications.
2. **Integrate with CI/CD Pipeline:** Configure your CI/CD pipeline to retrieve secrets from Vault at deploy time. Use Vault’s API or CLI to fetch the required secrets and inject them into the deployment process without exposing them in source code or logs. For example, you can use environment variables or configuration files to pass secrets to your application during deployment.
3. **Use OIDC for Authentication:** Implement OIDC to authenticate your CI/CD pipeline with
    Vault or other secret management tools. OIDC allows your pipeline to obtain temporary credentials or tokens that can be used to access secrets securely. This eliminates the need to store long-lived credentials in source code or configuration files.

91. How do you scan images and IaC in the pipeline?

    Ans: Scanning images and Infrastructure as Code (IaC) in the pipeline involves integrating security scanning tools into the CI/CD process to identify vulnerabilities, misconfigurations, and compliance issues before deployment. Here’s how to implement this:
1. **Container Image Scanning:** Use container image scanning tools (e.g., Trivy, Clair, Anchore) to analyze Docker images for known vulnerabilities and security issues. Integrate the scanning step into the CI/CD pipeline after the image is built but before it is pushed to a registry. Configure the scanner to generate reports and fail the build if critical vulnerabilities are detected.
2. **IaC Scanning:** Use IaC scanning tools (e.g., Checkov, Terraform Validator, TFLint) to analyze your Infrastructure as Code templates (e.g., Terraform, CloudFormation, Ansible) for security misconfigurations and compliance violations. Integrate the scanning step into the CI/CD pipeline before applying the IaC changes to the infrastructure. Configure the scanner to generate reports and fail the build if critical issues are found.
3. **Automated Reporting and Alerts:** Set up automated reporting and alerting mechanisms to notify the development and security teams of any vulnerabilities or misconfigurations detected during the scanning process. This allows for timely remediation and ensures that security is integrated into the development lifecycle.

92. Optimistic vs pessimistic locking (for a payments DB).

    Ans: Optimistic and pessimistic locking are two concurrency control mechanisms used to manage access to shared resources in a database, particularly in scenarios like a payments database where data integrity is critical.
- **Optimistic Locking:** In optimistic locking, multiple transactions can access the same resource concurrently without acquiring locks. Instead, each transaction reads the data and performs its operations, but before committing, it checks whether the data has been modified by another transaction since it was read. If a conflict is detected (i.e., the data has changed), the transaction is rolled back, and the application can retry the operation. Optimistic locking is suitable for scenarios with low contention, as it allows for higher concurrency and reduces the overhead of locking. It is often implemented using version numbers or timestamps to track changes.
- **Pessimistic Locking:** In pessimistic locking, a transaction acquires a lock on the resource it is accessing, preventing other transactions from modifying it until the lock is released. This approach ensures that only one transaction can modify the resource at a time, reducing the risk of conflicts and maintaining data integrity. Pessimistic locking is suitable for scenarios with high contention, where the likelihood of concurrent modifications is high. However, it can lead to reduced concurrency and potential deadlocks if not managed properly. Pessimistic locking is often implemented using database-level locks or explicit lock statements.

93. How do you handle a thundering-herd / cache stampede?

    Ans: A thundering herd or cache stampede occurs when multiple requests simultaneously attempt to access a resource that is not available in the cache, leading to a sudden spike in load on the backend system. This can overwhelm the system and cause performance degradation or outages. Here are strategies to handle a thundering herd/cache stampede:
1. **Cache Expiration and Staggered Refresh:** Implement cache expiration policies with staggered refresh times to prevent all requests from expiring at the same time. This can be achieved by adding random jitter to the cache expiration time, ensuring that requests are spread out over time and reducing the likelihood of a sudden spike in load.
2. **Request Coalescing:** Use request coalescing techniques to group multiple requests for the same resource into a single request to the backend. This can be achieved by implementing a locking mechanism or a queue that allows only one request to fetch the resource while other requests wait for the result to be cached. Once the resource is fetched and cached, all waiting requests can be served from the cache, reducing the load on the backend.
3. **Rate Limiting and Throttling:** Implement rate limiting and throttling mechanisms to control the number of requests hitting the backend system. This can help prevent overwhelming the system during periods of high traffic and ensure that requests are processed in a controlled manner. Use tools like API gateways or load balancers to enforce rate limits and throttle requests based on predefined thresholds.
4. **Circuit Breaker Pattern:** Implement a circuit breaker pattern to temporarily block requests to the backend when it is under heavy load or experiencing failures. This allows the system to recover and prevents further strain on the backend. Once the backend stabilizes, the circuit breaker can be reset, allowing requests to flow again. This pattern helps maintain system stability and prevents cascading failures.

94. How does OIDC between GitHub Actions and AWS work?

    Ans: OpenID Connect (OIDC) is an authentication protocol that allows GitHub Actions to securely authenticate with AWS without the need for long-lived credentials. Here’s how OIDC between GitHub Actions and AWS works:
1. **OIDC Provider Configuration:** In AWS, configure an OIDC identity provider that trusts GitHub Actions. This involves creating an IAM role with a trust policy that allows GitHub Actions to assume the role using OIDC. The trust policy specifies the GitHub Actions OIDC provider URL and the conditions under which the role can be assumed (e.g., specific repository, branch, or workflow).
2. **GitHub Actions Workflow Configuration:** In your GitHub Actions workflow, configure the job to use the OIDC token for authentication. GitHub Actions automatically generates a short-lived OIDC token for the workflow run, which can be used to assume the AWS IAM role. The token is included in the request to AWS when making API calls or accessing resources.
3. **Assuming the Role:** When the GitHub Actions workflow needs to access AWS resources, it uses the OIDC token to assume the IAM role configured in AWS. The AWS Security Token Service (STS) validates the OIDC token and issues temporary security credentials (access key, secret key, and session token) that the workflow can use to interact with AWS services. These temporary credentials have a limited lifespan, reducing the risk of exposure and ensuring that access is granted only for the duration of the workflow run.
4. **Accessing AWS Resources:** With the temporary credentials obtained through OIDC, the GitHub Actions workflow can securely access AWS resources, such as S3 buckets, DynamoDB tables, or Lambda functions, without the need for hardcoded credentials. The workflow can perform actions like deploying applications, managing infrastructure, or retrieving secrets from AWS services, all while maintaining security and compliance with best practices.

95. How do you design an idempotent deployment?

    Ans: Designing an idempotent deployment involves creating a deployment process that can be executed multiple times without causing unintended side effects or changes to the system. This ensures that the deployment can be safely retried in case of failures or interruptions. Here’s how to design an idempotent deployment:
1. **Use Declarative Configuration:** Adopt a declarative approach to define the desired state of the system using tools like Kubernetes manifests, Terraform, or Ansible playbooks. This allows the deployment process to focus on achieving the specified state rather than executing a series of imperative commands, making it easier to ensure idempotency.
2. **Check for Existing Resources:** Before creating or modifying resources, check if they already exist and are in the desired state. If the resource exists and matches the desired configuration, skip the creation or modification step. This prevents duplicate resources and ensures that the deployment process does not introduce unintended changes.

## Amazon / Google / Microsoft (big tech — fundamentals + depth + LPs)
96. 🔥 Design the infrastructure for a highly-available web service.
97. Explain TCP vs UDP; what happens when you type a URL.
98. How does DNS resolution work end-to-end?
99. 🔥 How does Linux handle a process from fork to exit?
100. What happens during a `kubectl apply` internally?
101. Design a logging + metrics pipeline for 100 microservices.
102. How do you achieve zero-downtime database migrations?
103. How would you detect and mitigate a memory leak in production?
104. Explain consistency, availability, partition tolerance (CAP).
105. 🔥 (Behavioral/LP) Tell me about a time you took ownership of an outage.

---
💡 Drill 10/day. Mark the ones you stumble on and move them to a "weak" list.
