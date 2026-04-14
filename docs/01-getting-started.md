# 1. Getting Started 🚦

[← Back to Home](../README.md)

---

## The Very Beginning

Make sure Git is installed on your machine:

```bash
# Check if Git is installed
git --version
# Output: git version 2.x.x
```

> 💡 **Beginner Tip:** If you get "command not found", download Git from [git-scm.com](https://git-scm.com/)

---

## Creating Your First Repository

```bash
# Initialize a new repository in the current folder
git init
# This creates a hidden .git folder — all of Git's magic lives here!
```

---

## Essential First Steps

```bash
# Check what's happening (run this often — it always helps!)
git status
# Output: On branch master (or main)
#         No commits yet
#         nothing to commit
```

---

## How Git Tracks Your Work (Visual Overview)

```
┌─────────────────────────────────────────────────────────┐
│                    GIT WORKFLOW                         │
│                                                         │
│  Working Dir   Staging Area    Local Repo    Remote     │
│  (your files)  (git add)       (git commit)  (GitHub)   │
│                                                         │
│  [Edit files] ──git add──► [Staged] ──git commit──►     │
│                                          [Committed]    │
│                                               │         │
│  [Updated] ◄──git pull──            git push──►         │
│                            [Remote Repo (origin)]       │
└─────────────────────────────────────────────────────────┘
```

> 💡 **Key mental model:** Git has 3 "places" your changes live locally — the working directory (your files), the staging area (what you've `git add`ed), and the local repo (what you've committed). Then there's the **remote** (GitHub/GitLab) as a 4th location.

---

## The Three States of a File in Git

| State | What it means |
|---|---|
| **Untracked** | Git doesn't know this file exists yet |
| **Modified** | Git knows the file, but you've changed it since last commit |
| **Staged** | You've run `git add` — changes are ready to commit |
| **Committed** | Changes are safely stored in Git's history |

---

## Next Steps

- ➡️ [The Complete Workflow](./02-complete-workflow.md) — push your first code
- ➡️ [SSH Key Setup](./14-ssh-setup.md) — connect to GitHub securely (do this first!)
