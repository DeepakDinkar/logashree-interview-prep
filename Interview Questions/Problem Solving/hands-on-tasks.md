# 💻 Problem Solving — Hands-On Tasks

> "Write this / fix this" tasks asked in technical rounds. Try WITHOUT looking, then check. Solutions sketched below each set.

🟢 basic · 🟡 mid · 🔴 advanced · 🔥 common

---

## A. Shell scripting 🔥
1. 🟢🔥 `[TCS][INFY]` Write a script that prints "UP"/"DOWN" for a list of URLs (health check).

    Ans: `for u in "$@"; do curl -sf "$u" >/dev/null && echo "UP $u" || echo "DOWN $u"; done`

2. 🟡🔥 `[CTS]` Count the number of `ERROR` lines in a log and group by error type.

    Ans: `grep ERROR app.log | awk '{print $5}' | sort | uniq -c | sort -rn`

3. 🟡 `[WMT]` Delete log files older than 7 days in `/var/log/app`.

    Ans: `find /var/log/app -name '*.log' -mtime +7 -delete`

4. 🟡🔥 `[WMT]` Alert if disk usage of `/` exceeds 80%.

    Ans: `u=$(df / | awk 'NR==2{gsub("%","",$5);print $5}'); [ "$u" -gt 80 ] && echo "disk $u%"`

5. 🟡 `[HEXA]` Find the top 5 IPs hitting an access log.

    Ans: `awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -5`

6. 🟡 `[CAPG]` Back up a directory with a date-stamped tarball.

    Ans: `tar -czf backup-$(date +%F).tar.gz /app/data`

<details><summary>Solution sketches</summary>

```bash
# 1 health check
for u in "$@"; do curl -sf "$u" >/dev/null && echo "UP $u" || echo "DOWN $u"; done
# 2 group errors
grep ERROR app.log | awk '{print $5}' | sort | uniq -c | sort -rn
# 3 cleanup
find /var/log/app -name '*.log' -mtime +7 -delete
# 4 disk alert
u=$(df / | awk 'NR==2{gsub("%","",$5);print $5}'); [ "$u" -gt 80 ] && echo "disk $u%"
# 5 top IPs
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -5
# 6 backup
tar -czf backup-$(date +%F).tar.gz /app/data
```
</details>

---

## B. Terraform 🔥
7. 🟢🔥 `[INFY][CTS]` Write a resource for an S3 bucket with versioning + SSE enabled.
8. 🟡🔥 `[WMT]` Configure a remote S3 backend with DynamoDB locking.
9. 🟡🔥 `[LTIM]` Create 3 EC2 instances using `for_each` over a map of names.
10. 🟡 `[ACN]` Write a reusable VPC module skeleton (inputs: cidr, azs; output: vpc_id).
11. 🟡 `[PP]` Import an existing S3 bucket into Terraform state.
12. 🔴 `[AMZN]` Given a resource recreated every apply, how do you stop it? (`ignore_changes`/`lifecycle`)

<details><summary>Solution sketches</summary>

```hcl
# 7
resource "aws_s3_bucket" "b" { bucket = "my-bucket" }
resource "aws_s3_bucket_versioning" "v" { bucket = aws_s3_bucket.b.id
  versioning_configuration { status = "Enabled" } }
resource "aws_s3_bucket_server_side_encryption_configuration" "e" {
  bucket = aws_s3_bucket.b.id
  rule { apply_server_side_encryption_by_default { sse_algorithm = "AES256" } } }

# 8 backend
terraform { backend "s3" {
  bucket="tfstate" key="prod.tfstate" region="us-east-1"
  dynamodb_table="tf-lock" encrypt=true } }

# 9 for_each
variable "names" { default = { a="t3.micro", b="t3.micro" } }
resource "aws_instance" "web" {
  for_each = var.names
  instance_type = each.value
  ami = data.aws_ami.al2.id
  tags = { Name = each.key } }

# 11 import
terraform import aws_s3_bucket.b my-existing-bucket
```
</details>

---

## C. Dockerfile 🔥
13. 🟡🔥 `[WMT][CMCST]` Write a multi-stage Dockerfile for a Node app (build → nginx).
14. 🟡 `[CTS]` Make an image run as non-root and add a healthcheck.
15. 🟡🔥 `[PP]` Given a 1.2 GB image, list 4 ways to shrink it.
16. 🟡 `[HEXA]` Push a built image to ECR (commands).

<details><summary>Solution sketches</summary>

```dockerfile
# 13
FROM node:20 AS build
WORKDIR /app
COPY package*.json ./ && RUN npm ci
COPY . . && RUN npm run build
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
# 14 add:
RUN adduser -D app && USER app
HEALTHCHECK CMD curl -f http://localhost/ || exit 1
```
15: multi-stage, alpine/distroless base, `.dockerignore`, merge RUN layers, remove caches.
16: `aws ecr get-login-password | docker login ...`; `docker tag`; `docker push`.
</details>

---

## D. Kubernetes YAML 🔥
17. 🟡🔥 `[WMT]` Write a Deployment (3 replicas) + Service (ClusterIP) for an app on port 8080.
18. 🟡🔥 `[PP]` Add liveness + readiness probes.
19. 🟡 `[CTS]` Mount a ConfigMap value as an env var.
20. 🔴 `[AMZN]` Add an HPA scaling 2→10 at 70% CPU.

<details><summary>Solution sketches</summary>

```yaml
# 17 + 18
apiVersion: apps/v1
kind: Deployment
metadata: { name: app }
spec:
  replicas: 3
  selector: { matchLabels: { app: app } }
  template:
    metadata: { labels: { app: app } }
    spec:
      containers:
      - name: app
        image: app:1.0
        ports: [{ containerPort: 8080 }]
        readinessProbe: { httpGet: { path: /health, port: 8080 }, initialDelaySeconds: 5 }
        livenessProbe:  { httpGet: { path: /health, port: 8080 }, initialDelaySeconds: 15 }
---
apiVersion: v1
kind: Service
metadata: { name: app }
spec: { selector: { app: app }, ports: [{ port: 80, targetPort: 8080 }] }
```
```yaml
# 20 HPA
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
spec:
  scaleTargetRef: { kind: Deployment, name: app, apiVersion: apps/v1 }
  minReplicas: 2
  maxReplicas: 10
  metrics: [{ type: Resource, resource: { name: cpu, target: { type: Utilization, averageUtilization: 70 } } }]
```
</details>

---

## E. GitHub Actions 🔥
21. 🟡🔥 `[WMT][ACN]` Write a workflow: on push to main → build Docker → push ECR (OIDC) → deploy ECS.
22. 🟡 `[LTIM]` Add a manual approval before prod deploy.
23. 🟡 `[CMCST]` Run tests on PRs only, deploy on merge only.

<details><summary>Solution sketches</summary>

See [`../../Roadmap/08-CICD-GitHub-Actions.md`](../../Roadmap/08-CICD-GitHub-Actions.md) reference workflow. Key bits:
`permissions: { id-token: write }`, `aws-actions/configure-aws-credentials` with `role-to-assume`, `environment: production` for approval gate, `on: { pull_request }` vs `on: { push: { branches: [main] } }`.
</details>

---

## F. SQL (PostgreSQL — resume) 🔥
24. 🟡🔥 `[TCS][INFY]` Nth highest salary.
25. 🟡🔥 `[CTS]` Find + delete duplicate rows keeping one.
26. 🟡 `[WMT]` Top 3 earners per department (window function).

<details><summary>Solution sketches</summary>

```sql
-- 24
SELECT DISTINCT salary FROM emp ORDER BY salary DESC OFFSET 1 LIMIT 1; -- 2nd highest
-- 26
SELECT * FROM (SELECT *, DENSE_RANK() OVER (PARTITION BY dept ORDER BY salary DESC) r FROM emp) t WHERE r <= 3;
-- 25 delete dups
DELETE FROM t a USING t b WHERE a.ctid < b.ctid AND a.col = b.col;
```
</details>

---
💡 In interviews, **talk while you type**: state assumptions, edge cases, then code.
