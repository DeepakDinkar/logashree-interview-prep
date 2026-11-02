# 10. SECURITY & COST — Roadmap

> Resume: *"Applied IAM least-privilege across 10+ resources, improved security compliance; reduced infra cost 35%."* Security + cost = senior-signal topics.

```
SECURITY & COST
│
├── 1. IAM SECURITY ⭐
│   ├── least privilege (start deny, grant minimal)
│   ├── roles over users/keys
│   ├── MFA, key rotation
│   ├── permission boundaries, SCPs
│   └── Access Analyzer
│
├── 2. SECRETS MANAGEMENT ⭐
│   ├── Secrets Manager (auto-rotation)
│   ├── SSM Parameter Store (SecureString)
│   ├── KMS (encryption keys)
│   ├── never in code / Git / tfvars
│   └── GitHub Secrets + OIDC
│
├── 3. NETWORK SECURITY
│   ├── Security Groups (least ports)
│   ├── private subnets for app/DB
│   ├── WAF (web app firewall)
│   ├── VPC endpoints (no public egress)
│   └── TLS everywhere (ACM certs)
│
├── 4. DATA SECURITY
│   ├── encryption at rest (KMS, S3 SSE, EBS)
│   ├── encryption in transit (TLS)
│   ├── S3 Block Public Access
│   └── backups + versioning
│
├── 5. SCANNING & COMPLIANCE
│   ├── SAST (CodeQL), dependency (Dependabot)
│   ├── container scan (Trivy / ECR)
│   ├── IaC scan (Checkov, tflint)
│   ├── GuardDuty (threat detect)
│   ├── Config (compliance rules)
│   └── Security Hub (aggregate)
│
├── 6. AUDIT
│   ├── CloudTrail (API audit)
│   ├── CloudWatch logs retention
│   └── tagging for ownership
│
└── 7. COST OPTIMIZATION ⭐
    ├── right-sizing instances
    ├── Auto Scaling (pay for what you use)
    ├── Spot + Reserved + Savings Plans
    ├── S3 lifecycle → Glacier
    ├── delete unused (EIP, EBS, snapshots)
    ├── Cost Explorer + Budgets + alerts
    └── Trusted Advisor + tagging
```

## 🔑 IAM least-privilege policy (example)
```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": ["s3:GetObject"],
    "Resource": "arn:aws:s3:::my-bucket/*"
  }]
}
```
Only `GetObject` on one bucket — not `s3:*` on `*`.

## 🔑 Decision reflexes
| Question | Answer |
|----------|--------|
| Where to store DB password | Secrets Manager / SSM SecureString (never code) |
| Give app AWS access | IAM Role (EC2/ECS/IRSA), not keys |
| Secrets Manager vs Parameter Store | rotation + cost vs cheap/simple config |
| Reduce cost | right-size, autoscale, spot/reserved, S3 lifecycle, kill idle |
| Encrypt S3 | SSE-S3 / SSE-KMS + Block Public Access |

## 🎯 Interview focus
- Tell your **least-privilege** story (your 10+ resources line).
- How you keep secrets out of source + inject at deploy.
- Shift-left security in CI/CD (scan before deploy).
- How you cut cost 35% (right-sizing, autoscale, Render→AWS migration).
- Shared Responsibility Model (AWS secures OF the cloud, you secure IN it).

→ Definitions: [`../Definitions/10-Security-Cost-definitions.md`](../Definitions/10-Security-Cost-definitions.md)
