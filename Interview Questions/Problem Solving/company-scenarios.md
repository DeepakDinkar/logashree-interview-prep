# 🏢 Problem Solving — Company Scenario Rounds (Set 2)

> Longer "design/implement/debug" prompts as actually posed in rounds. Practice speaking the approach aloud. 🔥 = common.

🟡 mid · 🔴 advanced

---

## Amazon 🔥 (ownership, dive-deep, real systems)
1. 🔴🔥 Design the deployment pipeline for a service deployed to 10 regions. How do you roll out safely?

    Ans: Use a phased rollout strategy with canary deployments in each region. Monitor key metrics and logs for errors, latency, and resource usage. Implement automated rollback on failure. Use feature flags to control exposure. Ensure CI/CD pipeline includes automated tests, security scans, and compliance checks.

2. 🔴 A service's error rate jumps after a deploy only in `eu-west-1`. Walk me through your investigation.

    Ans: Start by checking the deployment logs and monitoring metrics for `eu-west-1`. Compare the configuration and environment variables with other regions. Look for recent changes in code, dependencies, or infrastructure. Check for network issues, service dependencies, and any region-specific configurations. Use distributed tracing to identify where the errors are occurring. Roll back the deployment if necessary and implement fixes before redeploying.

3. 🔴🔥 Design auto-scaling for a service with a daily 10x traffic spike at 9 AM.

    Ans: Implement a combination of scheduled and dynamic auto-scaling. Use scheduled scaling to preemptively scale up the service before the 9 AM spike. Configure dynamic scaling policies based on CPU, memory, and request metrics to handle unexpected load. Ensure that the scaling policies are tested under load conditions. Use load balancers to distribute traffic evenly across instances. Monitor the scaling events and adjust thresholds as needed to optimize performance and cost.

4. 🟡 Write a script that finds and kills processes using > 2 GB RAM.

    Ans: Use a shell script that utilizes the `ps` command to list processes and their memory usage. Filter processes using `awk` to find those exceeding 2 GB of RAM, and then use the `kill` command to terminate them. Ensure to log the actions taken for auditing purposes. Example:
    ```bash
    #!/bin/bash
    ps aux --sort=-%mem | awk '$4>2 {print $2}' | while read pid; do
        echo "Killing process $pid using more than 2GB RAM"
        kill -9 $pid
    done
    ```

5. 🔴 Your Terraform apply is stuck because the state lock is held by a crashed job. What do you do?

    Ans: First, check the state lock status using `terraform state list` and identify the lock holder. If the job has crashed, you can manually unlock the state using `terraform force-unlock <LOCK_ID>`. Ensure that no other Terraform operations are running before doing this. After unlocking, verify the state integrity and proceed with the apply. Consider implementing a remote backend with state locking to prevent future issues.

6. 🔴 Design zero-downtime schema migration for a live database.

    Ans: Use a phased approach for schema migration. First, create a new version of the database schema alongside the existing one. Implement backward-compatible changes to allow both old and new versions to coexist. Use feature flags to control access to the new schema. Gradually migrate data and update application code to use the new schema. Monitor for errors and performance issues during the migration. Once all traffic is using the new schema, deprecate the old schema. Ensure proper backups and rollback plans are in place before starting the migration.

7. 🟡 A Lambda occasionally times out at 15 min. How do you diagnose and fix?

    Ans: Start by reviewing the Lambda function's logs in CloudWatch to identify the specific operations causing the timeout. Check for any external API calls or database queries that may be taking longer than expected. Optimize the code to reduce execution time, such as improving algorithms or using more efficient data structures. Consider breaking the function into smaller, more manageable functions or using asynchronous processing with AWS Step Functions. If necessary, increase the timeout limit in the Lambda configuration, but ensure that this is a last resort after optimization.

## Walmart 🔥 (scale, Kubernetes, reliability)
8. 🔴🔥 Design a multi-cluster Kubernetes setup across regions with failover.

    Ans: Implement a multi-cluster architecture using Kubernetes Federation or a service mesh like Istio to manage cross-cluster communication. Use a global load balancer (e.g., AWS Global Accelerator or Cloudflare) to route traffic to the nearest healthy cluster. Set up health checks and monitoring for each cluster to detect failures. Implement automated failover by redirecting traffic to a backup cluster in case of a primary cluster failure. Ensure that data replication and state management are handled appropriately, using tools like Velero for backups and disaster recovery. Use CI/CD pipelines to deploy applications consistently across clusters, and implement security best practices for inter-cluster communication.

9. 🔴 Pods are being OOMKilled under load. Diagnose and remediate.

    Ans: Start by checking the pod logs and Kubernetes events to identify which pods are being OOMKilled. Review the resource requests and limits defined in the pod specifications to ensure they are appropriate for the workload. Use monitoring tools like Prometheus and Grafana to analyze memory usage patterns over time. If necessary, increase the memory limits for the affected pods or optimize the application code to reduce memory consumption. Consider implementing horizontal pod autoscaling to handle increased load and prevent OOMKills. Additionally, review the node resources and ensure that there is sufficient memory available for all running pods.

10. 🟡🔥 Implement a canary rollout on EKS with automatic rollback on error-rate.

    Ans: Use Kubernetes Deployment with a canary strategy. Deploy a small percentage of pods with the new version alongside the existing version. Monitor metrics such as error rate, latency, and resource usage. If the error rate exceeds a predefined threshold, automatically rollback to the previous version. Use tools like Argo Rollouts or Flagger to automate the canary deployment and rollback process.

11. 🔴 A node goes NotReady and pods don't reschedule. Why? What do you check?

    Ans: Check the node status using `kubectl get nodes` and review the events for any issues. Verify that the node has sufficient resources (CPU, memory) and that the kubelet is running properly. Check for network connectivity issues between the node and the control plane. Review the pod specifications to ensure they have appropriate resource requests and limits. If the node is part of a cluster with taints, ensure that pods are not being blocked from scheduling due to taints. Additionally, check for any issues with the underlying infrastructure (e.g., EC2 instance health) that may be causing the node to go NotReady.

12. 🟡 Write a Kubernetes NetworkPolicy allowing only the frontend to reach the backend.

    Ans: Create a NetworkPolicy resource that specifies the allowed ingress traffic to the backend pods. Define the frontend pods as the only source of allowed traffic. Example YAML:
    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-frontend-to-backend
      namespace: backend-namespace
    spec:
      podSelector:
        matchLabels:
          app: backend
      policyTypes:
      - Ingress
      ingress:
      - from:
        - podSelector:
            matchLabels:
              app: frontend
    ```

13. 🔴 Design a cost-optimized EKS cluster (spot + on-demand mix). How?

    Ans: Use a combination of on-demand and spot instances to balance cost and reliability. Configure the EKS cluster with a node group for on-demand instances to handle baseline workloads and critical services. Create a separate node group for spot instances to handle variable workloads and non-critical services. Implement auto-scaling policies to dynamically adjust the number of spot instances based on demand. Use instance diversification by selecting multiple instance types for the spot node group to reduce the risk of interruptions. Monitor spot instance availability and set up automated fallback to on-demand instances in case of spot interruptions. Additionally, use cost monitoring tools like AWS Cost Explorer to track and optimize spending.

14. 🟡 How do you drain a node for maintenance without downtime?
    
    Ans: Use the `kubectl drain` command to safely evict pods from the node while ensuring that they are rescheduled on other available nodes. The command will cordon the node to prevent new pods from being scheduled and then gracefully terminate existing pods, respecting their termination grace periods. Ensure that the application is designed for high availability, with multiple replicas running across different nodes. Monitor the rescheduling process to confirm that all pods are successfully moved to healthy nodes before performing maintenance on the drained node.

## PayPal 🔥 (security, payments, correctness)
15. 🔴🔥 Design a secrets-management solution for 50 microservices across 3 envs.

    Ans: Use a centralized secrets management system like HashiCorp Vault or AWS Secrets Manager. Store secrets in a secure, encrypted manner and implement access controls based on service identity and environment. Use dynamic secrets where possible to reduce the risk of long-lived credentials. Integrate the secrets management system with CI/CD pipelines to automate secret injection during deployment. Implement auditing and logging to track access to secrets. Ensure that secrets are rotated regularly and that services are designed to handle secret updates without downtime.

16. 🔴 How do you ensure an idempotent deploy for a payments service?

    Ans: Implement idempotency keys for all payment requests to ensure that repeated requests do not result in duplicate transactions. Use a unique identifier for each request and store the state of processed requests in a database. Before processing a new request, check if the idempotency key already exists and return the previous response if it does. Ensure that the deployment process itself is idempotent by using infrastructure-as-code tools like Terraform or CloudFormation, which can manage resource states and prevent unintended changes. Additionally, implement thorough testing and validation to confirm that deployments do not introduce side effects.

17. 🟡🔥 How do you keep secrets out of Docker images and Git history?

    Ans: Use environment variables or secret management tools to inject secrets at runtime rather than baking them into Docker images. Avoid committing secrets to Git by using `.gitignore` to exclude files containing sensitive information. Use tools like Git hooks or pre-commit checks to prevent accidental commits of secrets. For CI/CD pipelines, use secure storage for secrets and inject them during the build or deployment process. Additionally, consider using Docker's build-time secrets feature to pass secrets securely during the image build process without including them in the final image.

18. 🔴 Design a secure CI/CD pipeline — list every security control.

    
    Ans: Implement the following security controls in the CI/CD pipeline:
    - Use version control with access controls and branch protection.
    - Implement code scanning for vulnerabilities and static analysis.
    - Use signed commits and tags to verify code integrity.
    - Integrate dependency scanning to identify known vulnerabilities in libraries.
    - Use secrets management to securely handle sensitive information.
    - Implement automated testing, including unit, integration, and security tests.
    - Use container image scanning for vulnerabilities before deployment.
    - Enforce least privilege access for pipeline users and service accounts.
    - Implement audit logging for all pipeline activities.
    - Use secure communication protocols (e.g., HTTPS, SSH) for all interactions.
    - Regularly update and patch CI/CD tools and dependencies.

19. 🟡 A certificate expired in prod at 2 AM. How do you prevent recurrence?

    Ans: Implement automated certificate management using tools like AWS Certificate Manager or Let's Encrypt with auto-renewal. Set up monitoring and alerting for certificate expiration, with notifications sent to the responsible team well in advance of the expiration date. Maintain an inventory of all certificates in use and their expiration dates. Use a centralized dashboard to track certificate status across environments. Additionally, implement a process for regular audits of certificates to ensure compliance and timely renewal.

20. 🔴 Design network isolation so the payments subnet has no internet egress.

    Ans: Create a dedicated VPC for the payments service with private subnets that do not have a route to an internet gateway. Use NAT gateways or NAT instances in separate public subnets for any necessary outbound traffic from other services, but ensure that the payments subnet does not have access to these NAT resources. Implement security groups and network ACLs to restrict traffic to only allow necessary communication between the payments service and other internal services. Use VPC endpoints for AWS services that the payments service needs to access, such as S3 or DynamoDB, to avoid internet egress. Regularly audit the network configuration to ensure compliance with isolation requirements.

21. 🟡 Rotate database credentials with zero downtime.

    Ans: Use a secrets management system that supports dynamic credential rotation, such as AWS Secrets Manager or HashiCorp Vault. Implement a process where the application retrieves the database credentials at runtime rather than storing them in configuration files. When rotating credentials, generate new credentials and update the secrets management system. The application should be designed to handle credential changes gracefully, such as by using connection pooling with automatic reconnection. Ensure that the old credentials remain valid for a short overlap period to allow existing connections to complete before they are revoked. Monitor the application for any connection issues during the rotation process.

## Comcast / Cisco (platform, observability)
22. 🔴🔥 Design centralized logging + metrics for 100 microservices (cost-aware).

    Ans: Implement a centralized logging and metrics solution using a combination of open-source tools and managed services. Use Fluentd or Logstash to collect logs from all microservices and forward them to a centralized log storage solution like Elasticsearch or Amazon OpenSearch Service. For metrics, use Prometheus to scrape metrics from each microservice and store them in a time-series database. Use Grafana for visualization and dashboarding of both logs and metrics. Implement log retention policies and data lifecycle management to control costs, such as archiving older logs to S3 or Glacier. Use sampling and filtering techniques to reduce the volume of logs collected, focusing on error logs and critical events. Ensure that the logging and metrics infrastructure is scalable, highly available, and secure, with proper access controls in place.

23. 🟡 Set up alerting that avoids alert fatigue — what rules?

    Ans: Implement alerting rules that focus on actionable events and avoid noise. Use thresholds based on historical data and trends rather than static values. Group related alerts into a single notification to reduce the number of alerts sent. Implement alert suppression during known maintenance windows or when certain conditions are met. Use severity levels to prioritize alerts and ensure that critical issues are addressed promptly. Regularly review and refine alerting rules based on feedback from the operations team to ensure they remain relevant and effective. Additionally, consider using anomaly detection techniques to identify unusual patterns that may indicate issues without triggering false positives.

24. 🔴 p99 latency doubled but p50 is flat. Find the root cause.

    Ans: Start by analyzing the latency distribution and identifying which requests are contributing to the increased p99 latency. Use distributed tracing tools like AWS X-Ray or OpenTelemetry to trace requests across services and identify any bottlenecks or slow components. Check for any recent changes in code, configuration, or infrastructure that may have introduced performance regressions. Review resource utilization metrics (CPU, memory, I/O) for the affected services to identify any contention or saturation issues. Investigate external dependencies, such as third-party APIs or databases, that may be causing delays. Once the root cause is identified, implement optimizations or fixes to address the issue and monitor the latency metrics to ensure improvement.


25. 🟡 Write a CloudWatch Logs Insights query to find the top 10 error messages.
    
    Ans: Use the following CloudWatch Logs Insights query to find the top 10 error messages:
```sql
fields @timestamp, @message
| filter @message like /error/i
| stats count() as errorCount by @message
| sort errorCount desc
| limit 10
```

26. 🔴 Design an SLO + error-budget policy for a tier-1 API.

    Ans: Define the SLO based on key performance indicators such as availability, latency, and error rate. For example, set an SLO of 99.9% availability and a maximum error rate of 0.1% over a rolling 30-day period. Establish an error budget that allows for a certain number of errors or downtime within the defined SLO. Implement monitoring and alerting to track the SLO metrics in real-time. If the error budget is exceeded, trigger a review process to identify the root cause and implement corrective actions. Communicate the SLO and error budget policy to all stakeholders and ensure that it is integrated into the development and operational processes.

27. 🟡 How do you trace a request across 6 services? (X-Ray/OpenTelemetry)

    Ans: Use distributed tracing tools like AWS X-Ray or OpenTelemetry to instrument each of the 6 services. Ensure that each service generates trace IDs and propagates them through the request headers. Configure the tracing tool to collect and visualize the traces, allowing you to see the flow of requests across services. Use the trace data to identify latency, errors, and bottlenecks in the request path. Implement logging and metrics collection alongside tracing to provide additional context for debugging and performance analysis. Regularly review and optimize the tracing configuration to ensure comprehensive coverage and minimal overhead.

## Accenture / Deloitte / EY (enterprise governance)
28. 🟡🔥 Design a multi-account AWS structure for an enterprise (Organizations/landing zone).

    Ans: Implement a multi-account AWS structure using AWS Organizations to create a hierarchical account structure. Create separate accounts for different environments (e.g., development, staging, production) and for different business units or teams. Use Service Control Policies (SCPs) to enforce governance and compliance across accounts. Implement a landing zone with centralized logging, monitoring, and security controls. Use AWS Control Tower to automate account provisioning and enforce best practices. Establish cross-account roles and permissions to enable secure access between accounts while maintaining least privilege. Regularly review and audit the account structure to ensure it aligns with organizational policies and compliance requirements.

29. 🟡 Enforce mandatory tags and block untagged resources. How?

    Ans: Use AWS Service Control Policies (SCPs) to enforce mandatory tagging across all accounts in the organization. Create a policy that denies the creation of resources without the required tags. Implement AWS Config rules to continuously monitor resource compliance with tagging policies and trigger alerts for non-compliant resources. Use AWS Lambda functions to automatically remediate untagged resources by applying default tags or notifying the responsible team. Integrate tagging requirements into the CI/CD pipeline to ensure that resources are tagged correctly during deployment. Regularly review and update the tagging policies to reflect changes in organizational requirements.

30. 🔴 Implement policy-as-code to deny public S3 buckets org-wide.

    Ans: Use AWS Config and AWS Organizations to implement policy-as-code for denying public S3 buckets across the organization. Create a Config rule that checks for public access on S3 buckets and triggers a non-compliance notification if a bucket is found to be public. Use AWS Organizations Service Control Policies (SCPs) to enforce a policy that denies the creation of public S3 buckets. Implement automated remediation using AWS Lambda to either block the creation of public buckets or automatically change the bucket's permissions to private. Integrate these policies into the CI/CD pipeline to ensure that any new S3 buckets created during deployment are compliant with the organization's security requirements. Regularly audit and review the policies to ensure they remain effective and up-to-date with best practices.

31. 🟡 Build a Terraform repo structure for 5 teams and 3 environments.

    Ans: Organize the Terraform repo into a modular structure that separates concerns by team and environment. Create a top-level directory for each team, with subdirectories for each environment (e.g., dev, staging, prod). Within each environment directory, include Terraform configuration files for the resources specific to that environment. Use Terraform modules to encapsulate reusable components and share them across teams. Implement a version control strategy with branches for each environment and use pull requests for code reviews. Include a README file in each directory to document the purpose and usage of the configurations. Use Terraform workspaces or separate state files for each environment to manage state independently.

32. 🔴 Design a DR plan with RTO 1 hr, RPO 5 min for an RDS-backed app.

    Ans: Implement a multi-region architecture for the RDS-backed application. Use Amazon RDS Multi-AZ deployments to ensure high availability and automatic failover within the primary region. Set up cross-region read replicas to maintain a near real-time copy of the database in a secondary region. Configure automated backups and enable point-in-time recovery to meet the RPO of 5 minutes. Implement a failover strategy that includes DNS failover using Route 53 to redirect traffic to the secondary region in case of a primary region outage. Regularly test the DR plan through simulated failover exercises to ensure that the RTO of 1 hour can be met. Document the DR procedures and ensure that all team members are trained on the recovery process.

33. 🟡 How do you enforce least-privilege across 200 IAM roles?

    Ans: Implement a least-privilege access model by conducting a thorough audit of all 200 IAM roles to identify the permissions currently granted. Use AWS IAM Access Analyzer to analyze and review the permissions for each role, identifying any excessive or unnecessary permissions. Create custom IAM policies that grant only the required permissions for each role based on their specific job functions. Implement role-based access control (RBAC) to group users and assign them to roles with appropriate permissions. Regularly review and update IAM policies to ensure they remain aligned with the principle of least privilege. Use AWS CloudTrail to monitor and log all IAM activity for auditing purposes.

## TCS / Infosys / Cognizant (service — hands-on basics)
34. 🟢🔥 Write a shell script to rotate logs older than 30 days and gzip them.

```bash
#!/bin/bash
LOG_DIR="/path/to/logs"
find "$LOG_DIR" -type f -name "*.log" -mtime +30 -exec gzip {} \;
``` 
35. 🟢 Write a Dockerfile for a Python Flask app (production-ready).

```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.9-slim
# Set the working directory
WORKDIR /app
# Copy the current directory contents into the container at /app
COPY . /app
# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt
# Make port 80 available to the world outside this container
EXPOSE 80
# Define environment variable
ENV FLASK_APP=app.py
# Run the application
CMD ["flask", "run", "--host=0.0.0.0"]
```

36. 🟡🔥 Write Terraform to create a VPC with 2 public + 2 private subnets.

    Ans: Use `data.aws_availability_zones` to spread subnets across 2 AZs. Public subnets route to an Internet Gateway; private subnets route outbound through a NAT Gateway. Use `for_each`/`count` or explicit blocks for clarity.
```hcl
provider "aws" {
  region = "us-east-1"
}

variable "azs" { default = ["us-east-1a", "us-east-1b"] }

resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true
  tags = { Name = "main-vpc" }
}

# Public subnets (2)
resource "aws_subnet" "public" {
  count                   = 2
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.${count.index}.0/24"       # 10.0.0.0/24, 10.0.1.0/24
  availability_zone       = var.azs[count.index]
  map_public_ip_on_launch = true
  tags = { Name = "public-${count.index}" }
}

# Private subnets (2)
resource "aws_subnet" "private" {
  count             = 2
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.${count.index + 10}.0/24"        # 10.0.10.0/24, 10.0.11.0/24
  availability_zone = var.azs[count.index]
  tags = { Name = "private-${count.index}" }
}

# Internet Gateway for public subnets
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id
  tags   = { Name = "main-igw" }
}

# NAT Gateway (in a public subnet) for private outbound
resource "aws_eip" "nat" { domain = "vpc" }

resource "aws_nat_gateway" "nat" {
  allocation_id = aws_eip.nat.id
  subnet_id     = aws_subnet.public[0].id
  depends_on    = [aws_internet_gateway.igw]
  tags          = { Name = "main-nat" }
}

# Public route table -> IGW
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id
  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }
}
resource "aws_route_table_association" "public" {
  count          = 2
  subnet_id      = aws_subnet.public[count.index].id
  route_table_id = aws_route_table.public.id
}

# Private route table -> NAT
resource "aws_route_table" "private" {
  vpc_id = aws_vpc.main.id
  route {
    cidr_block     = "0.0.0.0/0"
    nat_gateway_id = aws_nat_gateway.nat.id
  }
}
resource "aws_route_table_association" "private" {
  count          = 2
  subnet_id      = aws_subnet.private[count.index].id
  route_table_id = aws_route_table.private.id
}
```

37. 🟡 Write a GitHub Actions workflow to build and push an image to ECR.

    Ans: Use **OIDC** (keyless) to assume an IAM role — no stored AWS keys. Log in to ECR, build, tag with the commit SHA, and push. Create `.github/workflows/docker-build.yml`:
```yaml
name: Build and Push Docker Image to ECR
on:
  push:
    branches: [main]

permissions:
  id-token: write      # required for OIDC
  contents: read

env:
  AWS_REGION: us-east-1
  ECR_REPOSITORY: my-app

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Configure AWS credentials (OIDC)
        uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: arn:aws:iam::123456789012:role/github-actions-ecr
          aws-region: ${{ env.AWS_REGION }}

      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v2

      - name: Build, tag, and push image
        env:
          REGISTRY: ${{ steps.login-ecr.outputs.registry }}
          IMAGE_TAG: ${{ github.sha }}
        run: |
          docker build -t $REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG .
          docker push $REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG
          # also tag latest
          docker tag $REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG $REGISTRY/$ECR_REPOSITORY:latest
          docker push $REGISTRY/$ECR_REPOSITORY:latest
```

38. 🟢🔥 Write SQL for the 3rd highest salary and to find duplicates.

    Ans: For the Nth highest salary, use `DENSE_RANK()` (handles ties correctly) or `OFFSET/LIMIT` on distinct salaries. For duplicates, `GROUP BY` the column(s) and keep groups with `COUNT(*) > 1`.
```sql
-- 3rd highest salary (DENSE_RANK handles ties)
SELECT salary
FROM (
  SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
  FROM employees
) t
WHERE rnk = 3;

-- Simpler alternative on distinct salaries
SELECT DISTINCT salary
FROM employees
ORDER BY salary DESC
OFFSET 2 LIMIT 1;      -- OFFSET N-1

-- Find duplicate emails
SELECT email, COUNT(*) AS cnt
FROM users
GROUP BY email
HAVING COUNT(*) > 1;

-- Delete duplicates, keep the lowest id
DELETE FROM users a
USING users b
WHERE a.email = b.email
  AND a.id > b.id;
```

39. 🟡 Debug: `terraform apply` says "resource already exists". Fix it.

    Ans: This means the resource exists in AWS but **not in Terraform state** (created manually, in another workspace, or state was lost). Terraform tries to create it again and AWS rejects the duplicate. Steps:
    1. **Confirm** the resource really exists in the console/CLI and matches your config.
    2. **Import it into state** instead of recreating:
       ```bash
       terraform import aws_s3_bucket.my_bucket my-existing-bucket-name
       # then
       terraform plan   # should show no changes (or only drift to reconcile)
       ```
    3. If it was a **leftover** you don't want, delete it in AWS (or `terraform state rm` the stale entry) and re-apply.
    4. **Root cause / prevent:** use a **remote backend (S3 + DynamoDB lock)** so state isn't lost or duplicated across machines; avoid manual console changes; align workspaces.

40. 🟡 A container runs locally but fails in ECS. List what you'd check.

    Ans: Work through environment differences between laptop and ECS:
    - **Logs first:** CloudWatch Logs for the task (`awslogs`/FireLens), `stoppedReason` on the stopped task, and container exit code.
    - **Image/arch:** did you push the right tag to ECR? Built for the right CPU arch (ARM vs x86 — Apple Silicon builds `arm64`; use `--platform linux/amd64` or Fargate ARM).
    - **Env vars & secrets:** locally in `.env`, but in ECS they come from the task definition / Secrets Manager / SSM — missing values cause crashes.
    - **IAM:** task role missing permissions (S3, Secrets Manager, etc.); execution role missing ECR pull / CloudWatch Logs permissions.
    - **Networking:** security groups, subnet (private needs NAT), target group health check path/port, container port vs mapping.
    - **Resources:** task CPU/memory too low → OOMKilled; raise limits.
    - **Health check:** ALB/ECS health check failing → task killed and recycled (looks like "won't start").
    - **Dependencies:** DB/endpoint reachable from the VPC? Localhost dependencies (a local DB) won't exist in ECS.

---
## 🧭 How to answer design prompts (say this structure)
1. **Clarify** requirements + constraints (scale, budget, RTO/RPO, compliance).
2. **Sketch** the architecture + request flow.
3. **Justify** each component choice vs alternatives.
4. **Cover the 5 lenses:** HA · Security · Observability · Cost · Automation.
5. **Call out failure modes** + how you detect/recover.

💡 For debug prompts: **"mitigate first (rollback), then root-cause."**
