# 📖 Security & Cost — Definitions & Examples

> Roadmap: [`../Roadmap/10-Security-Cost.md`](../Roadmap/10-Security-Cost.md)

### 📚 Reference docs
- [AWS Security best practices](https://docs.aws.amazon.com/security/) · [IAM best practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
- [Secrets Manager](https://docs.aws.amazon.com/secretsmanager/) · [SSM Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html) · [KMS](https://docs.aws.amazon.com/kms/)
- [GuardDuty](https://docs.aws.amazon.com/guardduty/) · [AWS Config](https://docs.aws.amazon.com/config/) · [Security Hub](https://docs.aws.amazon.com/securityhub/) · [AWS WAF](https://docs.aws.amazon.com/waf/)
- [Cost Optimization pillar](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html) · [Cost Explorer](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html) · [Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/) · [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks) · [Trivy](https://trivy.dev/) · [Checkov](https://www.checkov.io/)

---

## Security
**Least privilege** 🔥🔥 — grant only the permissions needed; start from deny. (Your resume: least-privilege across 10+ resources.)
**IAM Role vs User** 🔥 — role = temporary, assumable, no stored keys (for services/CI); user = long-lived human identity. Prefer roles.
**Permission boundary / SCP** — max permissions cap for a principal / whole account (Organizations).

**Secrets management** 🔥🔥
- **Secrets Manager** — stores secrets with **automatic rotation**; costs per secret.
- **SSM Parameter Store (SecureString)** — cheaper key/value config + secrets, KMS-encrypted.
- **KMS** — manages encryption keys.
- Rule: **never** commit secrets to code/Git/`.tfvars`; inject at deploy (GitHub Secrets + OIDC, or pull from Secrets Manager).

**Encryption** 🔥 — **at rest** (KMS, S3 SSE, EBS/RDS encryption) and **in transit** (TLS via ACM certs).
**Network security** — least-open Security Groups, private subnets for app/DB, **WAF** (filter web attacks), VPC endpoints.
**S3 security** — Block Public Access + bucket policy + SSE; serve via CloudFront OAC.

**Shift-left / scanning in CI** 🔥 — scan before deploy:
- **SAST** (CodeQL) — static code analysis.
- **SCA / dependency** (Dependabot) — vulnerable libraries.
- **Container scan** (Trivy / ECR) — image CVEs.
- **IaC scan** (Checkov / tflint) — Terraform misconfig.
**GuardDuty** — threat detection. **Config** — compliance rules. **Security Hub** — aggregates findings. **CloudTrail** — audit.

## Cost optimization 🔥
- **Right-sizing** — match instance size to real usage.
- **Auto Scaling** — pay only for needed capacity.
- **Pricing models** — On-Demand (flexible), **Reserved/Savings Plans** (commit, cheaper), **Spot** (spare capacity, up to 90% off, interruptible).
- **S3 lifecycle** → Glacier for cold data.
- **Kill waste** — unattached EBS, idle Elastic IPs, old snapshots.
- **Visibility** — Cost Explorer, **Budgets** + alerts, **Trusted Advisor**, tagging for ownership.
(Your resume: cut infra cost 35% via Render→AWS migration + right-sizing.)

---

## 🎯 Likely interview Qs
- Explain least privilege; tell your IAM story.
- IAM role vs user vs policy.
- Where do you store secrets? Secrets Manager vs Parameter Store.
- How do you keep secrets out of source and inject at deploy?
- Encryption at rest vs in transit.
- How do you secure an S3 bucket?
- Shift-left security: what scans run in your pipeline?
- How did you reduce AWS cost? (right-size, autoscale, spot/reserved, lifecycle)
- Shared Responsibility Model.
