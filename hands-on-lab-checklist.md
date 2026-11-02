# 🧪 Hands-On Lab Checklist — Build It Yourself

> **Reading ≠ doing.** This is the single highest-impact prep. Spin up an [AWS Free Tier](https://aws.amazon.com/free/) account and actually build these. Every one maps to a resume claim you must defend. ⚠️ **Set a billing budget/alarm first** and tear down resources after each lab to stay free.

> ✅ Tick each when you've done it *by hand* and can explain every step.

---

## 🔰 Setup (do once)
- [ ] Create AWS free-tier account + enable MFA on root.
- [ ] Create an IAM admin user (don't use root daily).
- [ ] Set a **Budget + billing alarm** at $1 (avoid surprise charges).
- [ ] Install AWS CLI, Terraform, Docker, kubectl locally.
- [ ] `aws configure` with your IAM user keys.

---

## 🟢 Lab 1 — Linux & Shell (foundation)
- [ ] Launch an EC2 (t2.micro), SSH in.
- [ ] Check processes (`top`), disk (`df -h`), ports (`ss -tulpn`).
- [ ] Write a shell script: health-check a URL, alert if disk >80%.
- [ ] Schedule it with cron.
- [ ] *Defends:* "automated routine ops with shell scripting."

## 🟢 Lab 2 — Git & GitHub
- [ ] Create a repo, make branches, open a PR, merge it.
- [ ] Trigger a merge conflict on purpose and resolve it.
- [ ] Practice `reset`, `revert`, `cherry-pick`, `stash`, `reflog`.
- [ ] Set branch protection + required checks on `main`.

## 🟡 Lab 3 — Docker → ECR
- [ ] Write a multi-stage Dockerfile for a small app.
- [ ] `docker build`, `run`, `logs`, `exec`.
- [ ] Create an ECR repo; tag + push your image.
- [ ] *Defends:* "containerized workloads, removed env-specific issues."

## 🟡 Lab 4 — Terraform (your ⭐ skill)
- [ ] Write TF for a VPC (2 public + 2 private subnets).
- [ ] Add an EC2 + Security Group.
- [ ] Set up a **remote S3 backend + DynamoDB lock**.
- [ ] Refactor into a **reusable module**; use `for_each`.
- [ ] Run `plan`/`apply`/`destroy`; try `terraform import`.
- [ ] Break state on purpose, recover it.
- [ ] *Defends:* "Terraform modules, −70% provisioning, −50% setup."

## 🟡 Lab 5 — ECS deployment
- [ ] Create an ECS cluster (Fargate).
- [ ] Task definition pointing at your ECR image.
- [ ] Service behind an ALB; hit the public URL.
- [ ] Do a rolling update; watch it; roll back.
- [ ] *Defends:* "provisioned ECS with Terraform."

## 🟡 Lab 6 — CI/CD with GitHub Actions (your ⭐ skill)
- [ ] Workflow: on push → build → test → build image → push ECR.
- [ ] Set up **OIDC** → assume an IAM role (no stored keys).
- [ ] Add a deploy-to-ECS step.
- [ ] Add an environment with a **manual approval** gate.
- [ ] Add a security scan (Trivy) step.
- [ ] *Defends:* "automated build/deploy, −80% release effort."

## 🟡 Lab 7 — CloudWatch monitoring (your ⭐ skill)
- [ ] Send app/EC2 logs to a CloudWatch Log Group.
- [ ] Create a metric + **alarm** (CPU >80%).
- [ ] Wire alarm → **SNS** → your email.
- [ ] Build a **dashboard** with 3–4 widgets.
- [ ] Write a Logs Insights query to find errors.
- [ ] *Defends:* "CloudWatch alerting, −50% detection; dashboards, −40%."

## 🟡 Lab 8 — IAM & security
- [ ] Write a **least-privilege** policy (one action, one resource).
- [ ] Attach a role to EC2 to read one S3 bucket (no keys).
- [ ] Store a secret in Secrets Manager; read it from code.
- [ ] Turn on S3 Block Public Access; add a bucket policy.
- [ ] *Defends:* "IAM least-privilege across 10+ resources."

## 🔵 Lab 9 — (Optional) EKS / Kubernetes
- [ ] Create a small EKS cluster (or local `kind`/`minikube` to stay free).
- [ ] Deploy a Deployment + Service + Ingress.
- [ ] Add liveness/readiness probes + HPA.
- [ ] Break a pod (bad image) → debug CrashLoopBackOff/ImagePullBackOff.
- [ ] Do a rolling update + `rollout undo`.

## 🟢 Lab 10 — AI-assisted (prove the resume line)
- [ ] Use Copilot to scaffold a Terraform module — then review & fix it.
- [ ] Use Amazon Q to debug an AWS permission error.
- [ ] Note one time AI gave wrong/insecure output and you caught it → that's a great interview story.

---

## 🎯 Minimum before interviewing
If short on time, do **Labs 3, 4, 6, 7** (Docker, Terraform, CI/CD, CloudWatch) — they cover your four biggest resume claims and the most-asked hands-on topics.

## ⚠️ Cost safety
- Tear down with `terraform destroy` / delete resources after each lab.
- Check the Billing dashboard daily during labs.
- Prefer free-tier sizes (t2/t3.micro); use `kind`/`minikube` instead of EKS where possible.

---
💡 After each lab, write 3 sentences: *what you built, one thing that broke, how you fixed it.* Those become your interview stories.
