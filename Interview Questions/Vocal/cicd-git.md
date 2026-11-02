# 🗣️ Vocal — CI/CD & Git (Explain Out Loud)

> Definitions: [`../../Definitions/08-CICD-definitions.md`](../../Definitions/08-CICD-definitions.md) · [`../../Definitions/02-Git-definitions.md`](../../Definitions/02-Git-definitions.md)

## Git 🔥
1. 🟢🔥 `[GEN]` merge vs rebase — when each? Why not rebase a shared branch?

    Ans: Merge is used to combine changes from different branches, preserving the history of both branches. Rebase is used to apply changes from one branch onto another, creating a linear history. Rebase should not be used on shared branches because it rewrites history, which can cause conflicts and confusion for other collaborators.

2. 🟡🔥 `[TCS][CTS]` reset vs revert — which is safe on `main`?

    Ans: `git reset` is used to move the current branch pointer to a specific commit, effectively discarding commits after that point. This can be dangerous on shared branches like `main` because it rewrites history. `git revert`, on the other hand, creates a new commit that undoes the changes of a previous commit, making it safe to use on shared branches.

3. 🟢🔥 `[INFY]` fetch vs pull.

    Ans: `git fetch` downloads commits, files, and refs from a remote repository into your local repository, but it does not merge them into your current branch. `git pull` is a combination of `git fetch` followed by `git merge`, which updates your current branch with the latest changes from the remote repository.

4. 🟡🔥 `[WMT]` How do you resolve a merge conflict?

    Ans: To resolve a merge conflict, you need to manually edit the conflicting files to choose which changes to keep. After resolving the conflicts, you stage the changes using `git add`, and then commit the resolution with `git commit`. You can also use tools like `git mergetool` to assist in resolving conflicts.

5. 🟡 `[CAPG]` reset --soft vs --mixed vs --hard.

    Ans: `git reset --soft` moves the branch pointer to a specific commit but leaves the staging area and working directory unchanged. `git reset --mixed` (default) moves the branch pointer and updates the staging area to match the commit, but leaves the working directory unchanged. `git reset --hard` moves the branch pointer, updates the staging area, and resets the working directory to match the commit, effectively discarding all changes.

6. 🟡 `[HEXA]` What is cherry-pick? When used?

    Ans: `git cherry-pick` is a command that allows you to apply the changes introduced by an existing commit from one branch onto another branch. It is used when you want to selectively apply specific commits without merging entire branches, often for bug fixes or features that need to be applied to multiple branches.

7. 🟡 `[ACN]` Your branching strategy — GitFlow vs trunk-based, why?

    Ans: GitFlow is a branching model that uses feature branches, release branches, and hotfix branches to manage development. It is suitable for projects with longer release cycles and multiple developers. Trunk-based development, on the other hand, encourages developers to work on a single main branch (trunk) and integrate changes frequently. It is suitable for projects with continuous integration and delivery, promoting faster feedback and collaboration.

8. 🟡 `[LTIM]` How do you recover a commit after a bad reset? (reflog)

    Ans: You can recover a commit after a bad reset by using `git reflog`, which shows a log of all the changes made to the branches, including commits that are no longer reachable. You can find the commit hash of the lost commit in the reflog and then use `git checkout <commit-hash>` or `git reset --hard <commit-hash>` to restore it.

## CI/CD 🔥🔥
9. 🟢🔥 `[GEN]` Explain your CI/CD pipeline — stages and gates. (−80% release effort story)

    Ans: A typical CI/CD pipeline consists of several stages, including build, test, scan, push to a container registry (like ECR), deploy to an environment (like ECS), perform health checks, and handle rollbacks if necessary. Gates can be implemented at various stages, such as requiring approvals before deploying to production or running quality/security checks during the CI stage. This automation reduces manual effort and speeds up the release process significantly.

10. 🟡🔥 `[WMT][PP]` Continuous Delivery vs Continuous Deployment.

    Ans: Continuous Delivery is a software development practice where code changes are automatically built, tested, and prepared for release to production, but the actual deployment requires manual approval. Continuous Deployment takes this a step further by automatically deploying every change that passes the automated tests to production without manual intervention.

11. 🟡🔥 `[AMZN]` How does GitHub Actions authenticate to AWS? OIDC vs access keys.

    Ans: GitHub Actions can authenticate to AWS using OpenID Connect (OIDC) or access keys. OIDC allows for secure, short-lived credentials that are automatically rotated and do not require storing long-term secrets. Access keys, on the other hand, are static credentials that need to be managed and rotated manually, which can pose security risks if not handled properly.

12. 🟡🔥 `[WMT][CMCST]` Blue-green vs canary vs rolling deployment.

    Ans: Blue-green deployment involves running two identical production environments (blue and green) and switching traffic between them. Canary deployment gradually rolls out changes to a small subset of users before a full release. Rolling deployment updates instances in batches, replacing old versions with new ones over time. Each strategy has its own advantages and trade-offs in terms of risk, complexity, and user experience.

13. 🟡🔥 `[CTS][DLT]` How do you roll back a bad deployment? Automated rollback on health check?

    Ans: To roll back a bad deployment, you can use automated rollback mechanisms that monitor the health of the application after deployment. If the health checks fail, the system can automatically revert to the previous stable version. This can be achieved using deployment strategies like blue-green or canary deployments, where the previous version is still available and can be switched back to if needed.

14. 🟡 `[PP]` How do you gate a production deploy? (environment + approval)

    Ans: Production deployments can be gated by requiring approvals from designated stakeholders before the deployment proceeds. This can be implemented using environment protection rules in CI/CD tools, where only authorized users can approve the deployment to production. Additionally, automated checks and tests can be run to ensure that the code meets quality and security standards before it is deployed.

15. 🟡🔥 `[GEN]` Where do you store secrets in a pipeline?

    Ans: Secrets in a pipeline can be stored in secure secret management systems provided by CI/CD platforms, such as GitHub Secrets, GitLab CI/CD variables, or AWS Secrets Manager. These systems encrypt the secrets and provide controlled access to them during the pipeline execution, ensuring that sensitive information is not exposed in the codebase or logs.

16. 🟡 `[LTIM][ACN]` What quality/security gates run in CI? (tests, SonarQube, Trivy, Checkov)

    Ans: Quality and security gates in CI can include running unit tests, integration tests, and end-to-end tests to ensure code functionality. Additionally, static code analysis tools like SonarQube can be used to check for code quality issues, while security scanning tools like Trivy and Checkov can identify vulnerabilities in dependencies and infrastructure as code (IaC) configurations. These gates help maintain high standards for code quality and security before deployment.

17. 🟡 `[CAPG]` What is an artifact? "Build once, deploy many" — why?

    Ans: An artifact is a packaged output of the build process, such as a compiled binary, Docker image, or JAR file. The principle of "build once, deploy many" means that the same artifact can be deployed to multiple environments (e.g., staging, production) without rebuilding it each time. This ensures consistency across environments, reduces build time, and minimizes the risk of introducing errors during the build process.

18. 🟡 `[TECHM]` GitHub Actions: workflow / job / step / `needs:` / matrix.

    Ans: In GitHub Actions, a workflow is a configurable automated process that runs one or more jobs. A job is a set of steps that execute on the same runner, and each step is an individual task, such as running a script or command. The `needs:` keyword allows you to define dependencies between jobs, ensuring that one job runs only after another has completed successfully. A matrix allows you to run the same job with different configurations (e.g., different operating systems or versions) in parallel, enabling efficient testing across multiple environments.

19. 🟡 `[CMCST]` What is GitOps? ArgoCD/Flux basics.

    Ans: GitOps is a set of practices that uses Git as the single source of truth for declarative infrastructure and application configurations. Changes to the desired state are made in Git, and automated processes (like ArgoCD or Flux) continuously reconcile the actual state of the system with the desired state defined in Git. ArgoCD is a continuous delivery tool that monitors Git repositories and automatically deploys changes to Kubernetes clusters, while Flux is a set of continuous and progressive delivery solutions for Kubernetes that also relies on Git as the source of truth.

20. 🟢 `[HEXA]` Trigger types: push / pull_request / workflow_dispatch / schedule.

    Ans: In GitHub Actions, trigger types define how workflows are initiated. The `push` trigger runs a workflow when code is pushed to a specified branch. The `pull_request` trigger runs a workflow when a pull request is opened, synchronized, or closed. The `workflow_dispatch` trigger allows manual triggering of workflows through the GitHub UI or API. The `schedule` trigger runs workflows at specified intervals using cron syntax, enabling automated tasks to run on a regular basis.

---
### ⭐ Your resume line
- "Automated build/deploy with GitHub Actions, −80% release effort" → narrate: build→test→scan→push ECR→deploy ECS→health check→auto-rollback, prod gated by approval, OIDC keyless auth.
