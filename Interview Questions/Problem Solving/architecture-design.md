# 💻 Problem Solving — Architecture & Design

> Whiteboard/HLD rounds for DevOps/cloud roles. Draw boxes, state trade-offs, mention HA, security, cost, observability. Use your resume stack (AWS + Terraform + ECS/EKS + CI/CD).

🟡 mid · 🔴 advanced · 🔥 common

---

## Core designs 🔥
1. 🟡🔥 `[WMT][PP]` Design a highly-available 3-tier web app on AWS.
    Ans: Route 53 → CloudFront → ALB → ECS/EKS → RDS Multi-AZ + ElastiCache. 
2. 🟡🔥 `[CTS][ACN]` Design a CI/CD pipeline from commit to production.
    Ans: GitHub Actions → build/test → SonarQube gate → Trivy scan → push ECR → deploy dev/stage/prod → ECS rolling/blue-green → auto-rollback on failure. IaC via Terraform, OIDC auth. 
3. 🟡 `[AMZN]` Design infrastructure for a containerized microservice (ECS/EKS).
    Ans: VPC with public/private subnets, ALB, ECS/EKS cluster, Fargate tasks, RDS/ElastiCache, CloudWatch logs/metrics, IAM roles, Secrets Manager. Auto-scaling on CPU/req. CI/CD via GitHub Actions.
4. 🔴 `[WMT]` Design a multi-region disaster-recovery setup.
    Ans: Active-passive with warm standby. Route 53 failover routing, S3 cross-region replication, RDS cross-region read replica (promote on failover), ECR replication, IaC to rebuild. Test failover regularly.
5. 🟡 `[CMCST]` Design centralized logging + monitoring for 20 microservices.
    Ans: CloudWatch Logs + Metrics + Alarms → SNS → dashboards. X-Ray for tracing. Centralized log aggregation via Kinesis Firehose or OpenSearch. Alerts on error rates, latency, resource usage. CI/CD pipeline includes logging config.
6. 🟡 `[PP]` Design secrets management across environments.
    Ans: Use AWS Secrets Manager for sensitive secrets (DB creds, API keys) with rotation. Use Parameter Store for non-sensitive config. Store secrets per environment (dev/stage/prod). IAM roles for least-privilege access. CI/CD injects secrets at runtime, never in code.
7. 🔴 `[AMZN]` Design an auto-scaling strategy for unpredictable traffic.
    Ans: Use ECS/EKS with Fargate for serverless containers. Configure Auto Scaling Groups (ASG) or Horizontal Pod Autoscaler (HPA) based on CPU/memory/requests. Use CloudWatch metrics to trigger scaling policies. Implement cooldown periods to avoid thrashing. Consider spot instances for cost savings. Use CloudFront to offload static content and reduce backend load.
8. 🟡 `[LTIM]` Design a Terraform repo structure for multi-env, multi-team.
    Ans: 
    ```
    modules/      (vpc, ecs, rds, alb — reusable)
    envs/dev/     (main.tf calls modules + dev.tfvars)
    envs/stage/
    envs/prod/
    backend: S3 + DynamoDB lock, state key per env
    ```
    Use remote state, per-env workspaces/dirs, module versioning, PR review + plan gate.

---

## 1️⃣ HA 3-tier web app (template answer) 🔥
```
Route 53 ─► CloudFront (CDN) ─► ALB (public subnets, 2 AZs)
                                   │
                         ECS/EKS tasks (private subnets, 2 AZs) ◄─ Auto Scaling
                                   │
                         RDS Multi-AZ (isolated subnets) + ElastiCache
```
- **HA:** 2+ AZs everywhere, ALB health checks, ASG self-heal, RDS Multi-AZ failover.
- **Security:** public/private/data subnet tiers, SGs least-open, S3 Block Public Access, IAM roles, TLS via ACM, secrets in Secrets Manager.
- **Scale:** ASG/HPA on CPU/req; CloudFront offloads static.
- **Observability:** CloudWatch logs/metrics/alarms→SNS, dashboards, X-Ray.
- **IaC:** all in Terraform modules; CI/CD via GitHub Actions (OIDC).
- **Cost:** right-size, spot for workers, S3 lifecycle.

## 2️⃣ CI/CD commit→prod 🔥
`commit → GitHub Actions: build + unit test → SonarQube gate → build image → Trivy scan → push ECR (SHA tag) → deploy to dev (auto) → integration tests → stage (auto) → prod (manual approval) → ECS rolling/blue-green → health check → auto-rollback on failure`. Terraform `plan` on PR / `apply` on merge. OIDC keyless auth, least-priv deploy role.

## 4️⃣ Multi-region DR
- Define **RTO/RPO**. Active-passive: primary region + warm standby.
- Route 53 failover routing; S3 cross-region replication; RDS cross-region read replica (promote on failover); ECR replication; Terraform to rebuild. Test failover regularly.

## 8️⃣ Terraform repo structure
```
modules/      (vpc, ecs, rds, alb — reusable)
envs/dev/     (main.tf calls modules + dev.tfvars)
envs/stage/
envs/prod/
backend: S3 + DynamoDB lock, state key per env
```
Remote state, per-env workspaces/dirs, module versioning, PR review + plan gate.

---
## 🧭 Framework to answer ANY design question
1. **Clarify** — scale, traffic, budget, compliance, RTO/RPO.
    Ans: Ask questions to clarify requirements, constraints, and expectations. Understand the scale of the system, expected traffic patterns, budget limitations, compliance requirements, and recovery objectives (RTO/RPO). 
2. **High level** — draw the boxes + request flow.
    Ans: Sketch a high-level architecture diagram showing the main components and their interactions. Include the flow of requests through the system, highlighting key services and data stores. This helps visualize the overall design and identify potential bottlenecks or single points of failure.
3. **Deep dive** — compute, storage, DB, networking choices + why.
    Ans: Dive into the specifics of each component, explaining the choices made for compute (EC2, ECS, EKS), storage (S3, EBS, EFS), databases (RDS, DynamoDB), and networking (VPC, subnets, ALB/NLB). Justify these choices based on performance, scalability, cost, and operational considerations.
4. **Cross-cutting** — HA, security, observability, cost, IaC, CI/CD.
    Ans: Address cross-cutting concerns such as high availability (HA) by designing for redundancy and failover, security by implementing least privilege access and encryption, observability through logging and monitoring, cost optimization strategies, and automation using Infrastructure as Code (IaC) and Continuous Integration/Continuous Deployment (CI/CD) pipelines.
5. **Trade-offs** — name alternatives (ECS vs EKS, Multi-AZ vs Multi-Region) and justify.
    Ans: Discuss alternative approaches and their trade-offs, such as choosing between ECS and EKS for container orchestration, or deciding between Multi-AZ and Multi-Region deployments for disaster recovery. Justify the selected approach based on the specific requirements and constraints of the system being designed.

💡 Always weave in: **HA · Security · Observability · Cost · Automation (IaC/CI-CD)** — the 5 DevOps lenses.
