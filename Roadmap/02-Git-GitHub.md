# 2. GIT & GITHUB — Roadmap

> Source of truth for code AND infra (Terraform, YAML). GitHub Actions is your CI/CD, so GitHub fluency is core.

```
GIT & GITHUB
│
├── 1. BASICS
│   ├── init, clone, status, add, commit
│   ├── log, diff, show
│   └── .gitignore
│
├── 2. BRANCHING
│   ├── branch, checkout -b, switch
│   ├── merge (merge commit) vs rebase (linear)
│   ├── fast-forward vs no-ff
│   └── delete / prune branches
│
├── 3. REMOTE
│   ├── remote add origin, push, pull, fetch
│   ├── tracking branches
│   └── push vs pull vs fetch
│
├── 4. HISTORY SURGERY
│   ├── reset (soft / mixed / hard)
│   ├── revert (safe undo on shared)
│   ├── cherry-pick (one commit)
│   ├── stash (shelve work)
│   ├── amend
│   └── reflog (recover lost commits)
│
├── 5. CONFLICTS
│   ├── why they happen
│   ├── resolve markers <<<<<<< ======= >>>>>>>
│   └── mergetool
│
├── 6. WORKFLOWS
│   ├── Trunk-based (short branches, deploy fast)  ⭐
│   ├── GitFlow (release/hotfix/develop)
│   └── Feature-branch + Pull Request
│
├── 7. TAGS & RELEASES
│   ├── git tag v1.0, annotated tags
│   └── GitHub Releases
│
└── 8. GITHUB PLATFORM
    ├── Pull Requests + review + approvals
    ├── Protected branches + required checks
    ├── CODEOWNERS
    ├── GitHub Actions (CI/CD) — see section 8
    ├── Secrets & environments
    └── OIDC → AWS (keyless auth)
```

## 🔑 Must-know commands
| Task | Command |
|------|---------|
| New branch | `git checkout -b feature/x` |
| Save for later | `git stash` → `git stash pop` |
| Undo last commit (keep changes) | `git reset --soft HEAD~1` |
| Safe undo on shared branch | `git revert <sha>` |
| Bring one commit over | `git cherry-pick <sha>` |
| Replay onto main (linear) | `git rebase main` |
| See what will be pushed | `git log origin/main..HEAD` |
| Recover deleted commit | `git reflog` then `git checkout <sha>` |

## 🎯 Interview focus (🔥 asked constantly)
- **merge vs rebase** — merge preserves history (merge commit); rebase rewrites for linear history. **Never rebase shared branches.**
- **reset vs revert** — reset rewrites history (dangerous on shared); revert creates a new inverse commit (safe).
- **fetch vs pull** — fetch downloads, doesn't merge; pull = fetch + merge.
- **How you resolve a merge conflict** — walk through markers.
- **Branching strategy you use** — trunk-based for fast CD, PR + required checks.

→ Definitions: [`../Definitions/02-Git-definitions.md`](../Definitions/02-Git-definitions.md)
