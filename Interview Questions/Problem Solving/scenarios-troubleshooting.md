# 💻 Problem Solving — Scenarios & Troubleshooting

> "What would you do if…" + debugging rounds. Senior-signal: a clear diagnosis method, not guessing. Answer with **how you'd investigate → likely causes → fix → prevent**.

🟢 basic · 🟡 mid · 🔴 advanced · 🔥 common

---

## Production incidents 🔥
1. 🟡🔥 `[WMT][PP]` A deployment went out and the site is returning 5xx. Walk me through what you do **right now**.
2. 🟡🔥 `[CTS]` A pod is in **CrashLoopBackOff**. How do you debug it?
3. 🟡🔥 `[AMZN]` An EC2 instance is unreachable via SSH. What do you check?
4. 🟡 `[CMCST]` CPU on the app servers is pinned at 100%. How do you investigate?
5. 🟡🔥 `[WMT]` Disk is full on a server at 2 AM. What do you do?
6. 🔴 `[PP]` Latency spiked for 10% of requests (p99). How do you find the cause?
7. 🟡 `[DLT]` Users report intermittent 502s from the ALB. Where do you look?
8. 🔴 `[AMZN]` A Terraform `apply` failed halfway. State is now partial. What now?

<details><summary>Approach cheatsheet</summary>

- **1 (5xx after deploy):** check CloudWatch logs/metrics → confirm it's the new version → **roll back** (previous task def / `rollout undo`) → then root-cause in staging. Mitigate first.
- **2 (CrashLoopBackOff):** `kubectl describe pod` (events) + `kubectl logs --previous` → common: bad config/env, missing secret, failing migration, OOMKilled, wrong command.
- **3 (no SSH):** Security Group (port 22), NACL, instance status checks, key pair, is it running?, public IP/route table, SSH agent.
- **4 (100% CPU):** `top`/`ps`, check a runaway process, recent deploy, check CloudWatch, consider scaling (ASG/HPA) as mitigation.
- **5 (disk full):** `df -h` → `du -sh /*` → truncate/rotate big logs → add logrotate → alarm earlier at 80%.
- **6 (p99 latency):** traces (X-Ray) → find slow dependency (DB, downstream), check DB slow query log, connection pool, GC; add caching.
- **7 (502 from ALB):** target health checks failing, app timeouts shorter than ALB idle timeout, unhealthy targets being cycled, backend 5xx.
- **8 (partial TF apply):** `terraform plan` to see diff, `terraform state list`, re-apply (idempotent), `import` any orphaned resource, never hand-edit state.
</details>

---

## Design-ish operational scenarios 🔥
9. 🟡🔥 `[WMT]` How would you achieve zero-downtime deployments?
10. 🟡 `[PP]` How do you roll back a bad release automatically?
11. 🟡🔥 `[CTS]` How do you manage secrets across dev/stage/prod?
12. 🟡 `[ACN]` How do you do blue-green on ECS?
13. 🔴 `[AMZN]` How do you handle a region outage? (DR strategy)
14. 🟡 `[LTIM]` How do you prevent config drift in infra?
15. 🟡 `[CMCST]` A teammate created resources manually in the console. How do you reconcile with Terraform?
16. 🟡🔥 `[WMT]` How do you reduce cloud cost without hurting reliability?
17. 🔴 `[PP]` How do you secure a CI/CD pipeline end-to-end?
18. 🟡 `[DLT]` How do you give developers safe, limited AWS access?

<details><summary>Approach cheatsheet</summary>

- **9 zero-downtime:** rolling/blue-green/canary + readiness probes + connection draining on ALB + DB backward-compatible migrations.
- **11 secrets:** Secrets Manager / SSM per env, injected at deploy via OIDC; never in Git; rotate.
- **13 region outage:** multi-region (active-passive), Route 53 failover, cross-region replication (S3, RDS), IaC to rebuild fast; define RTO/RPO.
- **14 drift:** everything via Terraform, deny console writes (SCP), scheduled `plan` drift detection, PR review.
- **15 reconcile:** `terraform import`, then codify; or delete + recreate via TF.
- **16 cost:** right-size, autoscale, spot for non-critical, reserved/savings for steady, S3 lifecycle, delete idle (EIP/EBS/snapshots), Budgets alerts.
- **17 secure pipeline:** OIDC (no keys), least-priv deploy role, secret scanning, SAST/SCA/container/IaC scans, signed artifacts, protected branches, approval gates, audit via CloudTrail.
</details>

---
💡 Always lead with **"first I'd mitigate (roll back), then root-cause."** Shows production maturity.
