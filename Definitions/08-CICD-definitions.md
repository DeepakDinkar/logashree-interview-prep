# 📖 CI/CD & GitHub Actions — Definitions & Examples ⭐

> Roadmap: [`../Roadmap/08-CICD-GitHub-Actions.md`](../Roadmap/08-CICD-GitHub-Actions.md)

### 📚 Reference docs
- [GitHub Actions docs](https://docs.github.com/en/actions) · [Workflow syntax](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)
- [GitHub Marketplace (actions)](https://github.com/marketplace?type=actions) · [configure-aws-credentials (OIDC)](https://github.com/aws-actions/configure-aws-credentials)
- [OIDC with AWS](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-amazon-web-services)
- [amazon-ecs-deploy-task-definition](https://github.com/aws-actions/amazon-ecs-deploy-task-definition) · [CodeQL](https://codeql.github.com/) · [Dependabot](https://docs.github.com/en/code-security/dependabot)
- [CI/CD concepts (GitLab)](https://about.gitlab.com/topics/ci-cd/) · [Argo CD (GitOps)](https://argo-cd.readthedocs.io/) · [SonarQube](https://docs.sonarsource.com/)

---

## Core concepts
**CI (Continuous Integration)** 🔥 — every push is auto-built + tested; catch breakage early.
**Continuous Delivery vs Deployment** 🔥 — Delivery = always release-ready, deploy to prod is a **manual** approval. Deployment = fully **automatic** to prod.
**Pipeline stages** — checkout → build → test → scan → package (image) → deploy → verify → rollback.
**Artifact** — build output (jar, image) stored once, promoted dev→stage→prod (build once, deploy many).

## GitHub Actions anatomy 🔥
- **Workflow** — YAML in `.github/workflows/`.
- **Event (`on:`)** — `push`, `pull_request`, `workflow_dispatch` (manual), `schedule` (cron).
- **Job** — runs on a runner (`runs-on: ubuntu-latest`); jobs run in parallel unless `needs:`.
- **Step** — `uses:` (a prebuilt action) or `run:` (shell).
- **Matrix** — run across versions/OSes in parallel.
- **Runner** — the VM/container executing jobs (GitHub-hosted or self-hosted).

## Secrets & environments 🔥
- **Secrets** — encrypted values (`${{ secrets.X }}`); never printed.
- **Environment** — `dev/stage/prod` with protection rules + **required reviewers** = manual approval gate.
- Prefer **OIDC** over stored AWS keys.

## OIDC → AWS 🔥🔥 (modern keyless auth)
GitHub issues a short-lived OIDC token; `aws-actions/configure-aws-credentials` exchanges it (via STS AssumeRole) for temp AWS creds. **No long-lived access keys to store or rotate.** IAM role's trust policy restricts which repo/branch may assume it.

## Deployment strategies 🔥🔥
| Strategy | How | Trade-off |
|----------|-----|-----------|
| **Rolling** | replace instances gradually | default; brief mixed versions |
| **Blue-Green** | run new (green) alongside old (blue), switch traffic | instant rollback; 2x resources |
| **Canary** | send small % to new version, ramp up | safest; needs traffic metrics |
| **Recreate** | stop old, start new | downtime |

**Rollback** 🔥 — redeploy previous image/task def, `kubectl rollout undo`, or revert Terraform. Automate on failed health check.

## Quality gates
- Branch protection + **required status checks** before merge.
- Tests + coverage, SonarQube quality gate.
- Security: CodeQL (SAST), Dependabot (deps), Trivy/ECR (image), Checkov (IaC).
- **Reusable workflows** to DRY pipelines.

---

## 🏗️ Your pipeline (narrate this)
`push → checkout → build + unit test → SonarQube gate → build Docker image → Trivy scan → push to ECR (tagged with SHA) → deploy to ECS (update task def) → health check → auto-rollback if unhealthy`. Prod requires environment approval.

---

## 🎯 Likely interview Qs
- Walk through your CI/CD pipeline — stages and gates.
- Continuous Delivery vs Deployment.
- How does GitHub Actions auth to AWS? (OIDC vs keys)
- Blue-green vs canary vs rolling. How do you roll back?
- How do you gate a production deploy? (environment + approval)
- Where do secrets live? How do you scan in CI?
- `needs:` and matrix builds — what are they?
