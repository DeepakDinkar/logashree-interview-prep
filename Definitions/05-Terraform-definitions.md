# 📖 Terraform — Definitions & Examples ⭐

> Roadmap: [`../Roadmap/05-Terraform.md`](../Roadmap/05-Terraform.md) · Your core IaC skill.

### 📚 Reference docs
- [Terraform documentation](https://developer.hashicorp.com/terraform/docs) · [Language reference](https://developer.hashicorp.com/terraform/language)
- [AWS Provider registry](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) (every resource)
- [Terraform Registry (modules)](https://registry.terraform.io/) · [terraform-aws-modules](https://github.com/terraform-aws-modules)
- [HashiCorp Learn — Terraform tutorials](https://developer.hashicorp.com/terraform/tutorials)
- [S3 backend](https://developer.hashicorp.com/terraform/language/settings/backends/s3) · [Checkov](https://www.checkov.io/) · [tflint](https://github.com/terraform-linters/tflint) · [Style guide](https://developer.hashicorp.com/terraform/language/style)

---

## Core concepts
**Infrastructure as Code (IaC)** 🔥 — define infra in code; **declarative** (describe desired state) and **idempotent** (same result each run).

**Terraform vs CloudFormation/Ansible** — Terraform: multi-cloud, declarative, state-based provisioning. Ansible: config management (procedural). CloudFormation: AWS-only.

**Provider** — plugin for a platform: `provider "aws" { region = "us-east-1" }`.

**Resource** 🔥 — an infra object you manage:
```hcl
resource "aws_instance" "web" {
  ami           = data.aws_ami.al2.id
  instance_type = "t3.micro"
}
```
**Data source** — read existing infra you don't manage: `data "aws_ami" "al2" {...}`.

**Variable / Output / Locals** — inputs / exported values / computed internal values.

**count vs for_each** 🔥 — `count = 3` (indexed list) vs `for_each = toset([...])` (map/set with stable keys — no shifting when you remove one).

---

## State 🔥🔥 (most-asked Terraform topic)
**State file (`terraform.tfstate`)** — Terraform's record mapping config → real resources. Source of truth for what it manages.
- ⚠️ Never edit by hand or commit to Git (has secrets).
**Remote backend** 🔥 — store state centrally (S3) so teams share it; with **DynamoDB lock** to prevent concurrent corruption.
```hcl
terraform {
  backend "s3" {
    bucket = "tfstate"; key = "prod.tfstate"
    region = "us-east-1"; dynamodb_table = "tf-lock"
  }
}
```
**State locking** — stops two people running `apply` at once.
**terraform import** 🔥 — bring existing (manually-created) infra under management.
**Drift** — real infra changed outside Terraform; `plan` shows the diff.

---

## Modules 🔥
**Module** — reusable bundle of resources with inputs/outputs. DRY: one `vpc` module reused across envs.
```hcl
module "vpc" {
  source = "./modules/vpc"
  cidr   = "10.0.0.0/16"
}
```
Root module calls child modules. Version them (registry/git tags).

---

## Lifecycle & workflow
**Commands** — `init` (providers+backend), `plan` (preview), `apply` (execute), `destroy` (tear down), `fmt`, `validate`.
**Lifecycle block** — `create_before_destroy`, `prevent_destroy`, `ignore_changes`.
**taint / -replace** — force recreate a resource.
**Workspaces** — multiple state instances for envs (dev/stage/prod); many teams prefer directory-per-env instead.

**CI/CD pattern** 🔥 — `terraform plan` on PR (review), `apply` on merge to main.

**Secrets** 🔥 — never in committed `.tfvars`; use environment vars (`TF_VAR_`), AWS Secrets Manager, or Vault; mark outputs `sensitive = true`.

---

## 🎯 Likely interview Qs
- What is state? Why a remote backend + locking?
- count vs for_each — when each?
- How do you import existing infra?
- How do you structure reusable modules?
- How do you handle secrets in Terraform?
- What is drift and how do you detect it?
- Your CI/CD flow for Terraform (plan on PR, apply on merge).
