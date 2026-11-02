# 🧠 Tricky Questions — Gotchas & "What Happens If"

> Senior-signal edge cases, common traps, and guess-the-outcome. The interviewer is testing depth, not trivia. Think out loud.

🟡 mid · 🔴 advanced · 🔥 common

---

## Git gotchas 🔥
1. 🟡🔥 You `git rebase` a branch others already pulled. What breaks? → Rewritten SHAs diverge; their pulls conflict. **Never rebase shared history.**

    Ans: Rebase rewrites commit history, changing commit SHAs. If others have based work on the original commits, their history will diverge, causing conflicts when they pull. Use `git merge` for shared branches instead.

2. 🟡 `git reset --hard` then realize you needed a commit. Recover it? → `git reflog` → `git checkout <sha>` (within gc window).

    Ans: `git reflog` keeps a log of all your HEAD movements, allowing you to find the SHA of the commit you lost. You can then check it out or create a new branch from it.

3. 🟡 Difference in result: `git revert HEAD` vs `git reset --hard HEAD~1`? → revert = new inverse commit (history kept, safe); reset = deletes the commit (history rewritten).

    Ans: `git revert` creates a new commit that undoes the changes of the specified commit, preserving history. `git reset --hard` moves the branch pointer back and discards commits, rewriting history.

4. 🟡 You committed a secret and pushed. Enough to just delete it in a new commit? → **No** — it's in history; rotate the secret + rewrite history (filter-repo/BFG).

    Ans: Deleting the secret in a new commit does not remove it from the repository's history. Anyone with access to the repo can still retrieve it. Use tools like `git filter-repo` or BFG Repo-Cleaner to remove it from history, and rotate the secret immediately.

## Linux / shell gotchas 🔥
5. 🟡🔥 `rm -rf $DIR/` where `$DIR` is unset. What happens? → expands to `rm -rf /` 💀. Why `set -u` + quoting matters.

    Ans: If `$DIR` is unset, the command expands to `rm -rf /`, which would attempt to delete the root directory, potentially destroying the system. Using `set -u` causes the shell to treat unset variables as an error, preventing this. Quoting variables (e.g., `"$DIR"`) also helps avoid unintended expansions.

6. 🟡 Script works interactively but fails in cron. Why? → cron has minimal `PATH`/env; use absolute paths + source env.

    Ans: Cron jobs run in a limited environment, often lacking the full `PATH` and other environment variables available in an interactive shell. Scripts that rely on these may fail. To fix this, use absolute paths for commands and source any necessary environment variables at the start of the script.

7. 🟡 `chmod 777` on a file — why is that bad? → world-writable; security risk. Use least-permissive (755/644).

    Ans: Setting a file to `chmod 777` makes it readable, writable, and executable by everyone, which is a significant security risk. It can allow unauthorized users to modify or execute the file. It's better to use the least permissive settings necessary for functionality, such as `755` for executables or `644` for regular files.

8. 🟡 `kill -9` a process and it leaves a lock/zombie. Why not always use -9? → no graceful cleanup; prefer SIGTERM first.

    Ans: Using `kill -9` sends a SIGKILL signal, which forcefully terminates the process without allowing it to perform any cleanup. This can leave behind resources like locks or temporary files, and may result in zombie processes. It's better to first send a SIGTERM (default `kill`) to allow the process to exit gracefully.

9. 🟡 `$?` after a pipeline `a | b` reflects which command? → the **last** (`b`) unless `set -o pipefail`.

    Ans: By default, the exit status `$?` of a pipeline reflects the exit status of the last command in the pipeline. If you want to capture the exit status of any command in the pipeline, you can use `set -o pipefail`, which will cause the pipeline to return a non-zero status if any command fails.

## Docker gotchas 🔥
10. 🟡🔥 You put `COPY . .` before `RUN npm install`. Why slow builds? → any file change busts the install layer cache. Copy manifests first.

    Ans: When you use `COPY . .` before `RUN npm install`, any change in the source files will invalidate the cache for the `npm install` layer, causing it to run again even if dependencies haven't changed. To optimize build times, copy only the necessary files (like `package.json` and `package-lock.json`) first, run `npm install`, and then copy the rest of the application files.

11. 🟡 Container exits immediately after `docker run`. Likely cause? → main process (PID 1) exited; foreground process needed; check CMD/ENTRYPOINT + `docker logs`.

    Ans: If a container exits immediately after starting, it's often because the main process (PID 1) has exited. Containers need a foreground process to keep running. Check the `CMD` or `ENTRYPOINT` in the Dockerfile and use `docker logs <container>` to see any error messages that might indicate why the process exited.

12. 🟡🔥 You set a secret via `ENV`/build-arg. Is it safe? → **No** — visible in image history/layers. Use runtime secrets.

    Ans: Setting secrets via `ENV` or build arguments in a Dockerfile is not secure because they can be exposed in the image history and layers. Instead, use runtime secrets management solutions, such as Docker secrets or environment variables passed at runtime, to keep sensitive information secure.

13. 🟡 Data disappears when container restarts. Why? → containers are ephemeral; use a **volume**.

    Ans: Containers are designed to be ephemeral, meaning that any data stored inside the container's filesystem will be lost when the container is stopped or removed. To persist data across container restarts, you should use Docker volumes or bind mounts to store data outside of the container's filesystem.

14. 🔴 `CMD` and `ENTRYPOINT` both set — what runs? → ENTRYPOINT executable with CMD as its default args.

    Ans: When both `CMD` and `ENTRYPOINT` are set in a Dockerfile, the `ENTRYPOINT` defines the executable that will run, while the `CMD` provides default arguments to that executable. If you run the container without specifying any command, it will execute the `ENTRYPOINT` with the arguments from `CMD`. If you provide arguments when running the container, they will override the `CMD` values.

## Kubernetes gotchas 🔥
15. 🟡🔥 Pod stuck in **Pending**. Top causes? → insufficient CPU/mem, no matching node (taints/selectors), unbound PVC.

    Ans: A pod can remain in the Pending state if there are not enough resources (CPU/memory) available on any node, if no nodes match the pod's node selectors or tolerations, or if a PersistentVolumeClaim (PVC) is not bound to a PersistentVolume (PV). Check `kubectl describe pod <pod>` for detailed events and reasons.

16. 🟡🔥 **ImagePullBackOff** — what's wrong? → bad image tag, private registry auth (ECR), wrong repo.

    Ans: The ImagePullBackOff error indicates that Kubernetes is unable to pull the specified container image. Common causes include using an incorrect image tag, lacking authentication for a private registry (like AWS ECR), or specifying the wrong repository. Verify the image name, tag, and ensure proper credentials are configured.

17. 🟡 You update a Secret — do running pods see the new value? → mounted-as-file updates eventually; **env-var secrets need a pod restart**.

    Ans: When a Secret is updated in Kubernetes, if it is mounted as a volume (file), the changes will eventually be reflected in the running pods. However, if the Secret is used as an environment variable, the pods will not see the new value until they are restarted, as environment variables are set at pod startup.

18. 🟡 Liveness probe too aggressive (short timeout). Effect? → healthy pods get killed → restart loop. Tune initialDelay/timeout.

    Ans: If a liveness probe is configured with a short timeout or aggressive settings, it may incorrectly determine that a healthy pod is unresponsive, leading to the pod being killed and restarted. This can create a restart loop. To avoid this, adjust the `initialDelaySeconds`, `timeoutSeconds`, and other probe parameters to allow sufficient time for the application to respond.

19. 🔴 Deleting a Deployment — do the pods survive? → No, owned ReplicaSet + pods garbage-collected. (Delete with `--cascade=orphan` to keep.)

    Ans: When you delete a Deployment in Kubernetes, the associated ReplicaSet and its pods are also deleted by default. This is because the Deployment owns the ReplicaSet, and Kubernetes performs garbage collection on owned resources. If you want to delete the Deployment but keep the pods, you can use the `--cascade=orphan` flag.

20. 🟡 `kubectl apply` vs `kubectl replace` vs `create` — difference? → apply = declarative merge; replace = full overwrite; create = fails if exists.

    Ans: `kubectl apply` is used for declarative updates, merging changes with the existing configuration. `kubectl replace` performs a full overwrite of the existing resource. `kubectl create` will create a new resource and fail if it already exists.

## Terraform gotchas 🔥
21. 🟡🔥 You change a resource's `name`. Terraform plans to **destroy + recreate**. Why? → name is often a force-new attribute. Mind downtime; use `create_before_destroy`.

    Ans: In Terraform, certain attributes are marked as "force-new," meaning that changing them requires the resource to be destroyed and recreated. The `name` attribute is commonly force-new for many resources. To minimize downtime, you can use the `create_before_destroy` lifecycle setting.

22. 🟡🔥 Two engineers run `apply` simultaneously without a lock. Result? → state corruption/race. Need DynamoDB lock.

    Ans: In Terraform, if two engineers run `apply` simultaneously without a state lock, it can lead to state corruption or race conditions. To prevent this, use a remote backend with state locking, such as DynamoDB for AWS.

23. 🟡 You delete a resource block from code. What does apply do? → **destroys** the real resource. (To stop managing without deleting: `state rm`.)

    Ans: When you remove a resource block from your Terraform configuration and run `apply`, Terraform will plan to destroy the corresponding real-world resource. If you want to stop managing the resource without deleting it, you can use `terraform state rm <resource>` to remove it from the state file.

24. 🟡 `count` vs `for_each` — you remove the middle item from a `count` list. What happens? → indices shift → everything after is recreated. `for_each` avoids this.

    Ans: When using `count`, if you remove an item from the middle of the list, the indices of the remaining items shift, causing Terraform to destroy and recreate resources that follow the removed item. Using `for_each` allows you to manage resources by key, avoiding index shifts and unnecessary recreations.

25. 🔴 Secret shows in plan/state output. Why, and fix? → state stores plaintext; mark `sensitive`, encrypt backend, restrict state access.

    Ans: In Terraform, secrets can appear in the plan or state output because the state file stores values in plaintext. To mitigate this, mark sensitive variables with `sensitive = true`, use an encrypted backend, and restrict access to the state file.

26. 🟡 Someone changed infra in the console. Next `plan` shows a diff. What is this? → **drift**. Decide: revert (apply) or import the new reality.

    Ans: Infrastructure drift occurs when the actual state of resources differs from the expected state defined in your Terraform configuration. You can either apply the configuration to revert the changes or use `terraform import` to bring the external changes into your state file.

## AWS gotchas 🔥
27. 🟡🔥 You attach a policy but the role still can't access S3. Why? → explicit Deny, SCP, bucket policy, or missing trust/assume. Deny always wins.

    Ans: In AWS, even if a policy allows access, an explicit Deny in another policy, a Service Control Policy (SCP), a bucket policy, or a missing trust/assume relationship can prevent access. Remember, Deny always overrides Allow.

28. 🟡 S3 bucket is "private" but files are public. Why? → bucket policy / ACL / Block Public Access off. Audit all three.

    Ans: Even if an S3 bucket is set to private, files can still be publicly accessible due to bucket policies, Access Control Lists (ACLs), or if the "Block Public Access" settings are turned off. It's important to audit all three configurations to ensure proper access control.

29. 🟡🔥 Security Group allows inbound 443 but site unreachable. Other suspects? → NACL, route table, subnet (private), health checks, target group, OS firewall.

    Ans: If a Security Group allows inbound traffic on port 443 but the site is still unreachable, other potential issues could include Network ACLs (NACLs) blocking traffic, incorrect route table configurations, the instance being in a private subnet without proper routing, health check failures in load balancers, misconfigured target groups, or OS-level firewalls blocking the connection.

30. 🟡 You stop an EC2 instance — does the public IP persist? → No (unless Elastic IP). Private IP persists.

    Ans: When you stop an EC2 instance, the public IP address is released unless it's an Elastic IP. The private IP address, however, remains the same.

31. 🟡 RDS Multi-AZ — does it scale reads? → No, that's **Read Replicas**. Multi-AZ = HA/failover only.

    Ans: RDS Multi-AZ deployments provide high availability and failover support, but they do not scale read operations. To scale reads, you would need to set up Read Replicas.

32. 🔴 Lambda behind VPC can't reach the internet. Why? → needs NAT Gateway (private subnet) or VPC endpoint.

    Ans: When a Lambda function is deployed inside a VPC, it loses default internet access. To allow internet access, you need to place the Lambda in a private subnet with a route to a NAT Gateway in a public subnet, or use a VPC endpoint for specific AWS services.

## CI/CD gotchas 🔥
33. 🟡🔥 Pipeline "works on my machine" but fails in CI. Common cause? → env/secret differences, missing deps, relative paths, timezone/locale.

    Ans: CI environments often differ from local development setups. Common issues include missing environment variables or secrets, dependencies not installed, relative paths that don't resolve correctly, and differences in timezone or locale settings. Ensure the CI environment mirrors the local setup as closely as possible.

34. 🟡 You store AWS keys in GitHub Secrets. Better option? → **OIDC** — no long-lived keys to leak/rotate.

    Ans: Using OpenID Connect (OIDC) for authentication allows your CI/CD pipeline to assume roles in AWS without the need for long-lived access keys. This reduces the risk of key leakage and simplifies key rotation.

35. 🟡 A deploy succeeds but app is down. Did the pipeline "pass" correctly? → missing post-deploy **health check** gate; add verification + auto-rollback.

    Ans: A successful deployment in the pipeline does not guarantee that the application is running correctly. Implementing post-deploy health checks can verify that the application is operational, and if it fails, you can trigger an automatic rollback to the previous stable version.

36. 🟡 Secrets printed in logs via `echo $SECRET`. Risk? → leaked in build logs; GitHub masks known secrets but avoid echoing.

    Ans: Printing secrets in logs can lead to accidental exposure, even if the CI/CD platform masks them. It's best to avoid echoing secrets and use them directly in commands or environment variables without logging.

---
💡 For every gotcha, the win is **stating the mental model** ("Deny wins", "containers are ephemeral", "state needs a lock"), not just the answer.
