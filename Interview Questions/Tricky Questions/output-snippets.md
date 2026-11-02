# 🧠 Tricky Questions — Output / "Will It Work?" Snippets (Set 2)

> Guess-the-output and spot-the-bug snippets. Read, predict, then check. These catch people who memorized commands but don't understand them.

---

## Shell / Linux
### 1. 🔥
```bash
x=5
if [ $x = 5 ]; then echo "equal"; fi
```
<details><summary>?</summary>Prints `equal`. `=` is string compare; works here but use `-eq` for numbers.</details>

### 2. 🔥
```bash
echo "files: $(ls | wc -l)"
cd /nonexistent && echo "in dir"
echo "done"
```
<details><summary>?</summary>`cd` fails → `&&` short-circuits so "in dir" is skipped, "done" still prints. Without `set -e`, script continues.</details>

### 3.
```bash
arr=(a b c)
echo ${arr[1]}
echo ${#arr[@]}
```
<details><summary>?</summary>`b` (0-indexed), then `3` (length).</details>

### 4. 🔥 Bug?
```bash
for file in $(ls *.txt); do
  rm $file
done
```
<details><summary>?</summary>Breaks on filenames with spaces; parsing `ls` is unsafe. Use `for f in *.txt; do rm "$f"; done`.</details>

### 5.
```bash
a=10
( a=20 )
echo $a
```
<details><summary>?</summary>`10`. `()` runs in a subshell; parent var unchanged.</details>

---

## Docker
### 6. 🔥
```dockerfile
FROM alpine
ENV GREETING=hello
RUN echo $GREETING
CMD echo $GREETING
```
<details><summary>?</summary>Build prints `hello`. At runtime CMD also prints `hello` — ENV persists into the container.</details>

### 7. 🔥 Why huge image?
```dockerfile
FROM ubuntu
RUN apt-get update && apt-get install -y python3
COPY . .
RUN pip install -r requirements.txt
```
<details><summary>?</summary>Full ubuntu base + build tools; no cleanup; `COPY . .` before pip busts cache. Use slim/alpine, multi-stage, copy requirements first.</details>

### 8.
```bash
docker run -d nginx
docker ps -a   # container exited?
```
<details><summary>?</summary>nginx stays running (foreground master process). A container exits only when PID 1 exits.</details>

### 9. 🔥
```dockerfile
ENTRYPOINT ["echo", "hello"]
CMD ["world"]
```
Run: `docker run img` then `docker run img goodbye`.
<details><summary>?</summary>First → `hello world`; second → `hello goodbye` (CMD overridden, ENTRYPOINT fixed).</details>

---

## Kubernetes
### 10. 🔥
A Deployment has `replicas: 3`. You `kubectl delete pod <one>`. Result?
<details><summary>?</summary>ReplicaSet recreates it → back to 3. Self-healing.</details>

### 11. 🔥
`replicas: 3` but only 2 pods ever Ready. Likely?
<details><summary>?</summary>Readiness probe failing on one, or insufficient resources for the 3rd (Pending).</details>

### 12.
Two containers in one pod — can they reach each other on `localhost`?
<details><summary>?</summary>Yes, pod containers share the network namespace.</details>

### 13. 🔥
You update a ConfigMap. Pods using it as **env vars** — updated?
<details><summary>?</summary>No — env vars are set at start; need a pod restart. Volume-mounted values update eventually.</details>

### 14.
`kubectl scale deploy app --replicas=0` — then HPA min is 2. What happens?
<details><summary>?</summary>HPA scales it back up to minReplicas (2).</details>

---

## Terraform
### 15. 🔥
```hcl
resource "aws_instance" "web" { count = 3 ... }
```
You remove the middle element from a list the count derives from. Effect?
<details><summary>?</summary>Indices shift → resources after it get destroyed/recreated. `for_each` with a map avoids this.</details>

### 16. 🔥
You delete a `resource` block and run `apply`. What happens to the real resource?
<details><summary>?</summary>It's **destroyed**. To stop managing without deleting: `terraform state rm`.</details>

### 17.
```hcl
variable "env" {}
resource "aws_s3_bucket" "b" { bucket = "data-${var.env}" }
```
Change `env` from `dev` to `prod`. Plan?
<details><summary>?</summary>Bucket name changes → destroy + recreate (name is force-new).</details>

### 18. 🔥
Two engineers run `apply` at the same time, no DynamoDB lock. Result?
<details><summary>?</summary>State race → possible corruption/conflicting changes. Remote backend + lock prevents it.</details>

---

## Git
### 19. 🔥
You force-push after rebasing a branch two others branched from. Impact?
<details><summary>?</summary>Their history diverges; their next pull conflicts. Don't rebase shared branches.</details>

### 20.
```bash
git reset --hard HEAD~2
```
Did you lose those 2 commits forever?
<details><summary>?</summary>No — `git reflog` can recover them until garbage collection.</details>

### 21. 🔥
You committed `.env` with secrets and pushed. Is `git rm .env` + commit enough?
<details><summary>?</summary>No — still in history. Rotate the secret + rewrite history (BFG/filter-repo).</details>

---

## AWS
### 22. 🔥
IAM role has `s3:*` allow, but a bucket policy has an explicit `Deny`. Can it access?
<details><summary>?</summary>No — explicit **Deny always wins**.</details>

### 23. 🔥
SG allows inbound 443, but the website is unreachable. Suspects?
<details><summary>?</summary>NACL, route table, private subnet, target-group/health-check, instance stopped, OS firewall, wrong listener.</details>

### 24.
You stop an EC2 instance without an Elastic IP, then start it. Public IP?
<details><summary>?</summary>Changes (new public IP). Private IP stays.</details>

### 25. 🔥
RDS is Multi-AZ. Does that improve read throughput?
<details><summary>?</summary>No — Multi-AZ is failover/HA only. Use Read Replicas to scale reads.</details>

### 26.
A Lambda in a private subnet can't call an external API. Why?
<details><summary>?</summary>No route to internet; needs a NAT Gateway or VPC endpoint.</details>

---

## CI/CD
### 27. 🔥
Pipeline passes but the app is down after deploy. Did it "work"?
<details><summary>?</summary>Deploy step succeeded but no health-check gate. Add post-deploy verification + auto-rollback.</details>

### 28.
`echo "token=$MY_SECRET"` in a GitHub Actions step. Safe?
<details><summary>?</summary>Risky — GitHub masks registered secrets but never print them; could leak via indirect transforms.</details>

### 29. 🔥
You store AWS access keys in repo secrets. Interviewer frowns. Better?
<details><summary>?</summary>OIDC — short-lived creds via AssumeRole, nothing to leak or rotate.</details>

---
💡 The point isn't the trick — it's **naming the underlying rule** ("Deny wins", "ephemeral containers", "state needs a lock", "env vars set at start").
