# 🎤 Project Walkthrough — Rehearsed Stories

> **The most-asked part of a service/consulting interview** (TCS, Infosys, Accenture, Deloitte, EY): *"Walk me through a project you worked on."* They probe your resume claims. Rehearse each story out loud until it's 3–4 minutes, smooth, and you can answer any follow-up.
> Your resume projects: **QOMOI** (current, AWS+Terraform), **UNFI** (Cognizant), **World Bank Group** (Cognizant).

---

## 🧭 The structure to use every time (memorize this flow)
1. **Context** (20s) — what the project/product was, your role, team size.
2. **Problem** (20s) — what was painful/manual/slow/insecure.
3. **What you did** (90s) — the architecture + your specific contributions (use "I", not "we").
4. **Tech & why** (30s) — the stack and *why those choices*.
5. **Result** (20s) — the quantified outcome (your resume numbers).
6. **Learning / what you'd improve** (20s) — shows maturity.

> 💡 Lead with "I", give numbers, be ready for "why did you choose X over Y?"

---

## 📌 Project 1 — QOMOI (current, "Cloud Infrastructure Projects", Oct 2025–Present)
**Stack:** AWS, Terraform, GitHub Actions, Docker, PostgreSQL, CloudFront, ECS

**Rehearsed story:**
> "QOMOI is a cloud-hosted product. When I joined, infrastructure was provisioned manually in the AWS console and the app was hosted on Render, which was costly and inconsistent across environments. **I designed the AWS infrastructure as code using Terraform** — VPC with public/private subnets, ECS for the containerized workloads, RDS PostgreSQL, S3, and CloudFront in front. I built **reusable Terraform modules** so spinning up a new environment went from days to hours. I **containerized the workloads with Docker** using multi-stage builds to remove environment-specific issues, and **automated the build-and-deploy with GitHub Actions** — build, test, scan, push to ECR, deploy to ECS, with a health check. I also **migrated hosting from Render to AWS**, set up **CloudWatch monitoring and alarms**, and applied **IAM least-privilege** across the resources.
> **Results:** Terraform cut provisioning effort by ~70%, the CI/CD automation reduced release effort by over 80%, the Render→AWS migration cut costs ~35%, and CloudWatch alerting cut incident detection time ~50%.
> If I were to improve it, I'd add automated rollback on failed health checks and bring in drift detection on a schedule."

**Likely follow-ups (have answers ready):**
- Why Terraform over CloudFormation? → multi-cloud, modular, large community, state-based plan/preview.
- How did you structure the Terraform? → modules + per-env dirs, remote S3 backend + DynamoDB lock.
- How did you handle secrets? → Secrets Manager / SSM, never in code, OIDC for GitHub Actions.
- What was the hardest bug? → (prepare one real example — a networking/SG or state-lock issue).
- How did you measure the 70%/80%/35%/50%? → before/after time & cost comparison.

---

## 📌 Project 2 — UNFI (Cognizant, "System Engineer – DevOps/AWS", Feb 2023–Aug 2025)
**Stack:** AWS, GitHub Actions, Docker, Terraform, GitHub

**Rehearsed story:**
> "At Cognizant I worked on the UNFI account as a DevOps/System Engineer. My focus was **automating CI/CD pipelines** and **provisioning AWS infrastructure with Terraform**. I **built GitHub Actions pipelines** that automated application deployments, which reduced manual deployment effort by ~60%. I **developed reusable Terraform modules** for provisioning EC2, RDS, IAM and VPC resources, cutting environment setup effort roughly in half. I **containerized applications with Docker** to improve release consistency, and **configured CloudWatch dashboards and alerts** for critical workloads, which reduced production issue identification time by ~40%.
> **Results:** −60% manual deployment effort, −50% environment setup, −40% issue identification time."

**Likely follow-ups:**
- What stages were in your pipeline? → checkout → build → test → image → push → deploy → verify.
- How did you handle multiple environments? → Terraform modules + tfvars per env.
- What did the CloudWatch dashboards track? → CPU, memory, latency, error rate, request count.
- How did you provision IAM safely? → least-privilege roles per service.

---

## 📌 Project 3 — World Bank Group (Cognizant, "Cloud & DevOps Support", Dec 2021–Feb 2023)
**Stack:** AWS, GitHub, Linux, Shell Scripting

**Rehearsed story:**
> "This was my first DevOps role — cloud and DevOps support for the World Bank Group account. I **supported application deployments across dev, test and production**, **resolved CI/CD pipeline and deployment failures** to improve release success rates, **automated routine operational tasks with shell scripting** (reducing manual effort ~30%), and **monitored application and infrastructure health** using logs, metrics and alerts to help resolve incidents faster.
> This is where I built my Linux, scripting and troubleshooting foundations before moving into full infrastructure automation."

**Likely follow-ups:**
- What did you automate with shell scripts? → log rotation, health checks, backups, cleanup.
- How did you troubleshoot a failed deployment? → logs → metrics → recent changes → rollback.
- How did you handle a production incident? → (prepare one STAR example).

---

## 🎯 Cross-project questions they love
1. 🔥 Which project are you most proud of and why?
2. 🔥 What was the biggest technical challenge you faced?
3. 🔥 Tell me about a production incident and how you handled it.
4. A time you disagreed with a design decision — what did you do?
5. How do you handle tight deadlines / multiple priorities?
6. What would you do differently if you redid a project?
7. How did you collaborate with developers / other teams?

## ⚠️ Preparation rules
- **Rehearse aloud**, not in your head. Record yourself once.
- **Never say "we" for your own work** — use "I designed / I built / I automated".
- **Memorize your numbers** (70/80/60/50/40/35/30%) and how you got them.
- **Prepare 2 failure stories** — interviewers love "tell me a time something broke."
- **Tie every answer back to a result.**
