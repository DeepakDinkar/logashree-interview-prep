# 5. TERRAFORM ⭐ — Roadmap

> Your IaC tool. Resume: *"provisioned AWS with Terraform, reduced manual effort 70%; built reusable modules, reduced env setup 50%."* Expect deep Terraform questions.

```
TERRAFORM
│
├── 1. CORE CONCEPTS
│   ├── IaC — declarative, idempotent
│   ├── HCL syntax
│   ├── Providers (aws, random, null)
│   └── terraform init / plan / apply / destroy
│
├── 2. RESOURCES & DATA
│   ├── resource "aws_instance" "web" { ... }
│   ├── data "aws_ami" "al2" { ... }  (read existing)
│   ├── attributes / references
│   └── depends_on
│
├── 3. VARIABLES & OUTPUTS
│   ├── variable (type, default, validation)
│   ├── terraform.tfvars / -var / TF_VAR_
│   ├── output values
│   └── locals (computed)
│
├── 4. EXPRESSIONS
│   ├── count vs for_each
│   ├── for expressions, dynamic blocks
│   ├── conditionals (cond ? a : b)
│   └── functions (join, lookup, cidrsubnet, merge)
│
├── 5. MODULES ⭐
│   ├── root vs child modules
│   ├── module "vpc" { source = "./modules/vpc" }
│   ├── input vars / outputs
│   ├── versioning + registry
│   └── reusable network/ecs/rds modules
│
├── 6. STATE ⭐
│   ├── terraform.tfstate — source of truth
│   ├── Remote backend (S3 + DynamoDB lock) ⭐
│   ├── state locking (concurrent safety)
│   ├── terraform state list / mv / rm
│   ├── terraform import (adopt existing infra)
│   └── NEVER edit state by hand / commit to git
│
├── 7. WORKSPACES & ENVS
│   ├── workspaces (dev/stage/prod)
│   ├── directory-per-env pattern
│   └── tfvars per env
│
├── 8. LIFECYCLE
│   ├── create_before_destroy
│   ├── prevent_destroy
│   ├── ignore_changes
│   └── taint / replace
│
└── 9. WORKFLOW & QUALITY
    ├── fmt, validate, plan review
    ├── tflint, checkov (security scan)
    ├── CI/CD: plan on PR, apply on merge ⭐
    └── drift detection
```

## 🔑 Core commands
| Command | Purpose |
|---------|---------|
| `terraform init` | download providers + configure backend |
| `terraform plan` | preview changes (dry run) |
| `terraform apply` | execute changes |
| `terraform destroy` | tear down |
| `terraform fmt` | format code |
| `terraform validate` | syntax/config check |
| `terraform state list` | list managed resources |
| `terraform import aws_s3_bucket.b my-bucket` | adopt existing |

## 🏗️ Remote backend (the #1 real-world setup)
```hcl
terraform {
  backend "s3" {
    bucket         = "my-tfstate"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "tf-locks"   # state locking
    encrypt        = true
  }
}
```

## 🎯 Interview focus (🔥)
- **What is state? Why remote backend?** Shared state + locking so teams don't corrupt it.
- **count vs for_each** — for_each uses a map/set (stable keys, no index shifting).
- **How to adopt existing infra** — `terraform import`.
- **Module design** — inputs/outputs, DRY, versioned.
- **How do you handle secrets** — never in tfvars committed; use Secrets Manager / env / Vault.
- **Drift** — someone changed infra manually → `plan` shows diff.
- **plan on PR, apply on merge** — your CI/CD gate.

→ Definitions: [`../Definitions/05-Terraform-definitions.md`](../Definitions/05-Terraform-definitions.md)
