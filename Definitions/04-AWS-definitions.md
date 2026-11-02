# 📖 AWS Core — Definitions & Examples ⭐

> Roadmap: [`../Roadmap/04-AWS-Core.md`](../Roadmap/04-AWS-Core.md) · Your platform — know every term here cold.

### 📚 Reference docs
- [AWS Documentation (all services)](https://docs.aws.amazon.com/) · [AWS Free Tier](https://aws.amazon.com/free/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [IAM docs](https://docs.aws.amazon.com/IAM/latest/UserGuide/) · [VPC docs](https://docs.aws.amazon.com/vpc/latest/userguide/) · [EC2](https://docs.aws.amazon.com/ec2/) · [ECS](https://docs.aws.amazon.com/ecs/) · [S3](https://docs.aws.amazon.com/s3/) · [RDS](https://docs.aws.amazon.com/rds/)
- [AWS Solutions Architect Associate (SAA-C03) exam guide](https://aws.amazon.com/certification/certified-solutions-architect-associate/) (you hold this)
- [AWS Skill Builder](https://skillbuilder.aws/) · [AWS Architecture Center](https://aws.amazon.com/architecture/) · [awsgeek visuals](https://www.awsgeek.com/)

---

## Fundamentals
**Region** — a geographic area (e.g. `us-east-1`). **Availability Zone (AZ)** — isolated datacenter(s) within a region; deploy across AZs for **High Availability**.

**Shared Responsibility Model** 🔥 — AWS secures **OF** the cloud (hardware, global infra); you secure **IN** the cloud (data, IAM, config, patching).

**Multi-AZ vs Multi-Region** 🔥 — Multi-AZ = HA within a region (failover). Multi-Region = Disaster Recovery + global latency.

**Well-Architected pillars** — Operational Excellence, Security, Reliability, Performance, Cost, Sustainability.

---

## IAM 🔥🔥
**IAM** — who can do what on which resource.
- **User** — a human/long-term identity. **Group** — collection of users. **Role** — assumable identity for services/workloads (temporary creds, no stored keys).
- **Policy** — JSON granting permissions: `Effect` (Allow/Deny), `Action`, `Resource`, `Condition`.
- **Least privilege** 🔥 — grant only what's needed (your resume line).
- **Give EC2/ECS access to S3** → attach an **IAM Role**, never hard-code keys.
- **STS / AssumeRole** — issues temporary credentials (used by OIDC from GitHub Actions).

```json
{ "Effect":"Allow", "Action":["s3:GetObject"], "Resource":"arn:aws:s3:::bucket/*" }
```

---

## VPC / Networking 🔥
**VPC** — your private virtual network (a CIDR like `10.0.0.0/16`).
**Subnet** — IP range in one AZ; **public** (route to Internet Gateway) or **private** (no direct internet).
**Internet Gateway (IGW)** — internet access for public subnets.
**NAT Gateway** — lets private subnets reach the internet **outbound** only.
**Route Table** — directs subnet traffic.

**Security Group vs NACL** 🔥🔥
| | Security Group | NACL |
|---|---|---|
| Level | instance | subnet |
| State | **stateful** (return traffic auto-allowed) | **stateless** (must allow both directions) |
| Rules | allow only | allow + **deny** |

**VPC Endpoint** — private connection to AWS services (e.g. S3) without internet.

---

## Compute
**EC2** — virtual machines (AMI + instance type + key pair + user-data).
**Auto Scaling Group (ASG)** 🔥 — maintains desired count, scales on metrics, replaces unhealthy instances (self-healing).
**ECS** 🔥 — AWS container orchestrator. **Task definition** = container blueprint; **Service** = keeps N tasks running.
- **EC2 launch type** (you manage nodes) vs **Fargate** (serverless, no nodes). 🔥
**ECR** — private Docker registry. **Lambda** — serverless functions (event-driven, pay-per-invoke). **EKS** — managed Kubernetes.

---

## Load Balancing / DNS / CDN
**ELB** — distributes traffic + health checks.
- **ALB (L7)** 🔥 — HTTP/HTTPS, path/host routing, best for web apps.
- **NLB (L4)** — TCP/UDP, ultra-low latency, static IP.
**Target Group** — set of targets (instances/IPs/containers) with health checks.
**Route 53** — DNS; routing policies (simple, weighted, latency, failover).
**CloudFront** 🔥 — CDN caching at edge locations; sits in front of S3/ALB; use **OAC** to lock S3 to CloudFront only.

---

## Storage
**S3** 🔥 — object storage in buckets (11 nines durability).
- **Storage classes** — Standard → Standard-IA → Glacier → Glacier Deep Archive (hot→cold, cheaper).
- **Lifecycle rules** — auto-transition/expire. **Versioning** — keep object versions. **Block Public Access** + bucket policy for security. **Presigned URL** — time-limited access.
**EBS** — block storage attached to one EC2. **EFS** — shared NFS across many instances.

---

## Databases
**RDS** 🔥 — managed relational DB (PostgreSQL/MySQL...).
- **Multi-AZ** — synchronous standby for failover (HA). **Read Replica** — async copies to scale reads.
- **Snapshots** — backups. **Parameter/Option groups** — config.
**Aurora** — cloud-native MySQL/Postgres-compatible, faster. **DynamoDB** — managed NoSQL, single-digit-ms. **ElastiCache** — managed Redis/Memcached.

---

## Messaging
**SQS** — managed queue (decouple, async). **SNS** 🔥 — pub/sub topics (CloudWatch alarms → SNS → email/Slack). **EventBridge** — event bus/rules.

---

## 🎯 Likely interview Qs
- SG vs NACL. Public vs private subnet. How does a NAT Gateway work?
- ECS EC2 vs Fargate. ALB vs NLB.
- How do you give an app access to S3 securely? (IAM Role)
- Multi-AZ vs Read Replica for RDS.
- Design a 3-tier HA architecture (draw VPC, AZs, ALB, ASG, RDS Multi-AZ).
- How do you secure an S3 bucket? (Block Public Access, OAC, SSE)
