# 4. AWS CORE ⭐ — Roadmap

> Your platform. Resume services: **EC2, VPC, IAM, RDS, ELB, ECS, S3, Auto Scaling, CloudFront, CloudWatch**. Backed by SA-Associate + Cloud Practitioner.

```
AWS CORE
│
├── 1. FUNDAMENTALS
│   ├── Regions (us-east-1) + Availability Zones (AZs)
│   ├── Account / Organizations
│   ├── Shared Responsibility Model
│   ├── Well-Architected (6 pillars)
│   └── Pricing — pay-as-you-go, reserved, spot, savings plans
│
├── 2. IAM ⭐  (Identity & Access Management)
│   ├── Users / Groups / Roles
│   ├── Policies (JSON: Effect, Action, Resource, Condition)
│   ├── Managed vs Inline policies
│   ├── Roles for EC2/ECS/EKS (no keys)
│   ├── Least privilege ⭐
│   └── MFA, access keys, STS / AssumeRole
│
├── 3. VPC / NETWORKING ⭐
│   ├── VPC (CIDR), Subnets (public/private per AZ)
│   ├── Internet Gateway / NAT Gateway
│   ├── Route Tables
│   ├── Security Groups (stateful) vs NACLs (stateless)
│   ├── Elastic IP, ENI
│   ├── VPC Peering / Transit Gateway
│   └── VPC Endpoints (private S3 access)
│
├── 4. COMPUTE
│   ├── EC2 — instances, AMIs, instance types, key pairs, user-data
│   ├── Auto Scaling Groups ⭐ — launch template, scaling policies
│   ├── ECS ⭐ — clusters, task definitions, services (EC2 & Fargate)
│   ├── ECR — container registry
│   ├── Lambda — serverless functions
│   └── EKS — managed Kubernetes (see section 7)
│
├── 5. LOAD BALANCING + DNS + CDN
│   ├── ELB/ALB (L7) vs NLB (L4) ⭐
│   ├── Target Groups + health checks
│   ├── Route 53 — DNS, routing policies, failover
│   └── CloudFront ⭐ — CDN, edge caching, OAI/OAC with S3
│
├── 6. STORAGE
│   ├── S3 ⭐ — buckets, storage classes, lifecycle, versioning
│   ├── S3 static hosting + CloudFront
│   ├── EBS — block storage for EC2
│   ├── EFS — shared NFS
│   └── Presigned URLs
│
├── 7. DATABASES
│   ├── RDS ⭐ — PostgreSQL/MySQL, Multi-AZ, read replicas
│   ├── Aurora
│   ├── DynamoDB — NoSQL
│   ├── ElastiCache — Redis/Memcached
│   └── Backups, snapshots, parameter groups
│
├── 8. MESSAGING / INTEGRATION
│   ├── SQS (queue), SNS (pub/sub) ⭐ alarms→SNS
│   ├── EventBridge
│   └── API Gateway
│
├── 9. OBSERVABILITY  (see section 9)
│   ├── CloudWatch Logs / Metrics / Alarms / Dashboards ⭐
│   ├── CloudTrail (audit)
│   └── X-Ray (tracing)
│
└── 10. SECURITY & COST  (see section 10)
    ├── KMS, Secrets Manager, Parameter Store
    ├── GuardDuty, Config, Security Hub
    └── Cost Explorer, Budgets, Trusted Advisor
```

## 🔑 Decision reflexes
| Question | Answer |
|----------|--------|
| VM vs container vs serverless | EC2 → ECS/EKS → Lambda (less ops, more managed) |
| ECS launch types | EC2 (manage nodes) vs **Fargate** (serverless, no nodes) |
| ALB vs NLB | ALB = L7/HTTP + path routing; NLB = L4/TCP, ultra-low latency |
| SG vs NACL | SG = stateful, instance-level, allow-only; NACL = stateless, subnet-level, allow+deny |
| S3 class choice | Standard → Standard-IA → Glacier (hot→cold, cheaper) |
| RDS HA | Multi-AZ (failover) vs Read Replica (scale reads) |
| Give EC2 S3 access | **IAM Role** attached (never hard-code keys) |

## 🏗️ Resume scenario you built
> *"Designed VPC + ECS + CloudFront + S3 with Terraform, reduced provisioning effort 70%."*
Public subnet (ALB) → private subnet (ECS tasks) → RDS in isolated subnet. CloudFront in front of S3/ALB. IAM least-privilege roles per service.

## 🎯 Interview focus
- Draw a 3-tier VPC (public/private/data subnets across 2 AZs).
- Multi-AZ vs Multi-Region (HA vs DR).
- How Auto Scaling + ALB + health checks self-heal.
- Securing S3 (block public access, bucket policy, OAC with CloudFront).
- IAM role vs user vs policy; least privilege story.

→ Definitions: [`../Definitions/04-AWS-definitions.md`](../Definitions/04-AWS-definitions.md)
