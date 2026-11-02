# 🗺️ AWS DevOps Engineer — Roadmap (Logashree, 4+ yrs)

> Built from the resume: **AWS** (EC2, VPC, IAM, RDS, ELB, ECS, S3, Auto Scaling, CloudFront, CloudWatch) · **Terraform** · **Git/GitHub** · **GitHub Actions** · **Docker** · **Kubernetes** · **Linux/Shell** · AI-assisted (Copilot, Amazon Q, ChatGPT, Claude).
> Certs: **AWS Solutions Architect – Associate**, **AWS Cloud Practitioner**.

This roadmap mirrors the **real flow of work** on an AWS DevOps team: write code → version it → build an image → provision infra → deploy → observe → secure.

---

## 🔁 The AWS DevOps Flow (end-to-end)

```
Developer commits code (Git / GitHub)
        │
        ▼
GitHub Actions CI  ──►  Build + Unit Test + SAST/Scan  ──►  Build Docker image
        │                                                        │
        ▼                                                        ▼
Push image to Amazon ECR                             Terraform provisions infra
        │                                            (VPC, ECS/EKS, RDS, ELB, S3, IAM)
        ▼                                                        │
GitHub Actions CD  ──►  Deploy to ECS / EKS  ◄──────────────────┘
        │
        ▼
ELB/ALB routes traffic ──► Auto Scaling adjusts capacity ──► CloudFront caches edge
        │
        ▼
CloudWatch logs + metrics + alarms ──► SNS notifies ──► Rollback if unhealthy
```

---

## 📚 Roadmap Sections (read in order)

| # | File | What it covers | Resume tie-in |
|---|------|----------------|---------------|
| 1 | [`01-Linux.md`](./01-Linux.md) | Filesystem, processes, permissions, networking, logs | Linux |
| 2 | [`02-Git-GitHub.md`](./02-Git-GitHub.md) | Branching, merge/rebase, PR workflow, GitHub | Git, GitHub |
| 3 | [`03-Shell-Scripting.md`](./03-Shell-Scripting.md) | Bash, variables, loops, cron, automation | Shell Scripting |
| 4 | [`04-AWS-Core.md`](./04-AWS-Core.md) ⭐ | IAM, VPC, EC2, ECS, RDS, S3, ELB, Auto Scaling, CloudFront | **AWS** |
| 5 | [`05-Terraform.md`](./05-Terraform.md) ⭐ | IaC, resources, modules, state, remote backend | **Terraform** |
| 6 | [`06-Docker.md`](./06-Docker.md) | Images, Dockerfile, multi-stage, ECR | Docker |
| 7 | [`07-Kubernetes.md`](./07-Kubernetes.md) | Pods, deployments, services, EKS | Kubernetes |
| 8 | [`08-CICD-GitHub-Actions.md`](./08-CICD-GitHub-Actions.md) ⭐ | Workflows, OIDC, deploy to ECS/EKS, rollback | **GitHub Actions** |
| 9 | [`09-Observability-CloudWatch.md`](./09-Observability-CloudWatch.md) ⭐ | Logs, metrics, alarms, dashboards, SNS | **CloudWatch** |
| 10 | [`10-Security-Cost.md`](./10-Security-Cost.md) | IAM least-privilege, secrets, scanning, cost control | IAM, security |
| 11 | [`11-AI-Assisted-Engineering.md`](./11-AI-Assisted-Engineering.md) ⭐ | Copilot, Amazon Q, responsible AI use, GenAI basics | **AI-Assisted Engineering** |

⭐ = your strongest / most-asked areas.

---

## 🎯 How to use for interview prep
1. **Roadmap** (this folder) → the map of everything you must know.
2. **[`../Definitions/`](../Definitions/)** → exact definitions + examples to say out loud.
3. **[`../Interview Questions/`](../Interview%20Questions/)** → real company Q&A: Vocal / Problem Solving / Tricky.

> Night before: skim this index → the two ⭐ sections you're weakest on → `Vocal` top 🔥 questions.

---
*Created: 2026-10-30 · For: Logashree S — AWS DevOps Engineer*
