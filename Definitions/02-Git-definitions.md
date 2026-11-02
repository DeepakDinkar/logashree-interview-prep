# 📖 Git & GitHub — Definitions & Examples

> Roadmap: [`../Roadmap/02-Git-GitHub.md`](../Roadmap/02-Git-GitHub.md)

### 📚 Reference docs
- [Pro Git book (free)](https://git-scm.com/book) — the definitive reference
- [Git official docs / reference](https://git-scm.com/docs)
- [GitHub Docs](https://docs.github.com/) · [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow)
- [Atlassian Git tutorials](https://www.atlassian.com/git/tutorials) (great merge vs rebase visuals)
- [Learn Git Branching (interactive)](https://learngitbranching.js.org/) · [Oh Sh*t, Git!?!](https://ohshitgit.com/) (recovery)

---

## Core concepts

**Git** — distributed version control; every clone has full history.

**Commit** — a snapshot of tracked files + metadata, identified by a SHA hash.

**Branch** 🔥 — a movable pointer to a commit; cheap parallel line of work.

**merge vs rebase** 🔥🔥 (asked everywhere)
- **Merge** — combines branches with a **merge commit**; preserves true history (non-linear).
- **Rebase** — **replays** your commits on top of another branch for a **linear** history; rewrites commit SHAs.
- ⚠️ **Never rebase a shared/public branch** — it rewrites history others depend on.

**fetch vs pull** 🔥
- `git fetch` downloads remote changes but **doesn't** touch your working branch.
- `git pull` = `fetch` + `merge` (or `--rebase`).

**reset vs revert** 🔥🔥
- `git reset` moves HEAD, **rewrites history**. `--soft` keeps staged, `--mixed` keeps working changes, `--hard` discards all. Dangerous on shared branches.
- `git revert <sha>` creates a **new commit that undoes** a change — safe on shared branches.

**cherry-pick** — apply a single commit from one branch onto another: `git cherry-pick <sha>`.

**stash** — temporarily shelve uncommitted work: `git stash` → `git stash pop`.

**reflog** — log of where HEAD has been; recover "lost" commits after a bad reset.

**Fast-forward merge** — if target has no new commits, pointer just moves forward (no merge commit).

**Merge conflict** 🔥 — same lines changed on both branches; Git marks them:
```
<<<<<<< HEAD
my change
=======
their change
>>>>>>> feature
```
Resolve by editing, then `git add` + commit.

**Tag** — named pointer to a commit, usually a release: `git tag v1.0`.

---

## Workflows 🔥
- **Trunk-based** — everyone commits to `main` via short-lived branches; ideal for CD. ⭐ (your style)
- **GitFlow** — `develop`, `feature/*`, `release/*`, `hotfix/*`, `main`; heavier.
- **Feature-branch + PR** — branch → Pull Request → review → required checks → merge.

## GitHub platform
- **Pull Request** — propose + review changes before merge.
- **Protected branch** — require reviews/status checks before merging to `main`.
- **CODEOWNERS** — auto-request reviewers by path.
- **GitHub Secrets / Environments** — store credentials, gate deploys with approval.
- **OIDC → AWS** — keyless auth so Actions assume an IAM role (no stored keys). ⭐

---

## 🎯 Likely interview Qs
- merge vs rebase — when each? Why not rebase shared branches?
- reset vs revert — which is safe on `main`?
- fetch vs pull.
- How do you resolve a merge conflict?
- Your branching strategy and why.
- How does GitHub Actions authenticate to AWS without keys? (OIDC)
