# 8. CI/CD with GITHUB ACTIONS ⭐ — Roadmap

> Resume: *"Automated build/deploy with GitHub Actions, reduced release effort 80%+."* This is a headline skill — know workflows, OIDC to AWS, and deploy-to-ECS/EKS cold.

```
CI/CD — GITHUB ACTIONS
│
├── 1. CONCEPTS
│   ├── CI — build + test on every push/PR
│   ├── CD — auto deploy to envs (delivery vs deployment)
│   ├── pipeline stages — build → test → scan → package → deploy
│   └── artifacts + promotion (dev→stage→prod)
│
├── 2. WORKFLOW ANATOMY
│   ├── .github/workflows/*.yml
│   ├── on: (push, pull_request, workflow_dispatch, schedule)
│   ├── jobs → runs-on → steps
│   ├── uses: (actions) vs run: (shell)
│   ├── needs: (job dependency)
│   └── matrix builds
│
├── 3. SECRETS & CONFIG
│   ├── repo / environment / org secrets
│   ├── environments + required reviewers (approval gate) ⭐
│   ├── variables vs secrets
│   └── NEVER echo secrets
│
├── 4. AWS AUTH ⭐
│   ├── OIDC → aws-actions/configure-aws-credentials (keyless) ⭐
│   ├── IAM role trust policy for the repo
│   └── avoid long-lived access keys
│
├── 5. BUILD & TEST
│   ├── checkout, setup-node/java/python
│   ├── cache dependencies
│   ├── unit tests + coverage
│   └── quality gate (SonarQube)
│
├── 6. SECURITY SCANS
│   ├── SAST (CodeQL)
│   ├── dependency scan (Dependabot)
│   ├── container scan (Trivy / ECR scan)
│   └── IaC scan (Checkov / tflint)
│
├── 7. PACKAGE & PUSH
│   ├── docker build
│   ├── login + push to ECR
│   └── tag with git SHA
│
├── 8. DEPLOY ⭐
│   ├── ECS — update task def + service
│   ├── EKS — kubectl/helm apply
│   ├── Terraform — plan on PR, apply on merge
│   └── S3 + CloudFront invalidation (static)
│
├── 9. STRATEGIES
│   ├── Rolling (default)
│   ├── Blue-Green (swap)
│   ├── Canary (gradual %)
│   └── Rollback on failed health check ⭐
│
└── 10. QUALITY
    ├── branch protection + required checks
    ├── reusable workflows
    └── status badges
```

## 🏗️ Reference workflow (ECS deploy via OIDC)
```yaml
name: deploy
on:
  push: { branches: [main] }
permissions:
  id-token: write      # for OIDC
  contents: read
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: aws-actions/configure-aws-credentials@v4
        with:
          role-to-assume: arn:aws:iam::123:role/gha-deploy
          aws-region: us-east-1
      - uses: aws-actions/amazon-ecr-login@v2
      - run: |
          docker build -t $ECR_REPO:$GITHUB_SHA .
          docker push $ECR_REPO:$GITHUB_SHA
      - uses: aws-actions/amazon-ecs-deploy-task-definition@v2
        with:
          task-definition: task-def.json
          service: app-svc
          cluster: prod
```

## 🎯 Interview focus (🔥)
- **Walk through your pipeline** — stages + gates (build→test→scan→push ECR→deploy ECS→health check→rollback).
- **OIDC vs access keys** — keyless, short-lived, no secret rotation.
- **How do you roll back** — redeploy previous task def / `rollout undo` / Terraform revert.
- **How do you gate prod** — environment protection + manual approval.
- **Blue-green vs canary** — swap vs gradual %.
- **Where do secrets live** — GitHub Secrets / Secrets Manager, never in code.

→ Definitions: [`../Definitions/08-CICD-definitions.md`](../Definitions/08-CICD-definitions.md)
