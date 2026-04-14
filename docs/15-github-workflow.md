# 15. GitHub Forking Workflow 🍴

[← Back to Home](../README.md)

> 💡 **What is a fork?** A fork is your own personal copy of someone else's repository on GitHub. It's how you contribute to open source — you work on your fork, then propose your changes to the original via a **Pull Request**.

---

## How the Fork Workflow Works

```
Original Repo (upstream)          Your Fork (origin)
github.com/owner/project    →    github.com/you/project
        │                               │
        │                         git clone ↓
        │                         Your Local Computer
        │                               │
        └── sync updates ◄── git pull upstream main
                                        │
                                  make changes
                                  git push origin
                                        │
                              Open Pull Request ──► Original Repo
```

---

## Step 1: Fork the Repository

1. Go to the original repo on GitHub (e.g. `github.com/owner/project`)
2. Click the **Fork** button (top right)
3. Choose your account — GitHub creates `github.com/you/project`

---

## Step 2: Clone Your Fork Locally

```bash
# Clone YOUR fork (not the original!)
git clone git@github.com:YOUR_USERNAME/project.git
cd project
```

---

## Step 3: Add the Original as "Upstream"

```bash
# Add the original repo as a remote called "upstream"
git remote add upstream git@github.com:ORIGINAL_OWNER/project.git

# Verify both remotes exist
git remote -v
# origin    git@github.com:YOUR_USERNAME/project.git (fetch)
# origin    git@github.com:YOUR_USERNAME/project.git (push)
# upstream  git@github.com:ORIGINAL_OWNER/project.git (fetch)
# upstream  git@github.com:ORIGINAL_OWNER/project.git (push)
```

> 💡 **Naming convention:** `origin` = your fork, `upstream` = the original project.

---

## Step 4: Create a Feature Branch

> ⚠️ **Never work directly on `main` in your fork!** Always create a new branch for your contribution.

```bash
# Make sure your main is up to date first (Step 6 explains how)
# Then create a feature branch
git checkout -b fix/typo-in-readme
# or
git checkout -b feat/add-dark-mode
```

---

## Step 5: Make Changes and Commit

```bash
# Make your changes...

# Stage and commit
git add .
git commit -m "fix: correct typo in README introduction"

# Push your branch to YOUR fork
git push -u origin fix/typo-in-readme
```

---

## Step 6: Keep Your Fork in Sync with Upstream

> This is the step most beginners forget! If the original repo gets new commits while you're working, your fork goes out of date.

```bash
# Fetch the latest changes from the original repo
git fetch upstream

# Switch to your main branch
git checkout main

# Merge upstream's main into your local main
git merge upstream/main
# or (cleaner history):
git rebase upstream/main

# Push updated main to your fork
git push origin main
```

Do this regularly to avoid messy merge conflicts in your PR!

---

## Step 7: Open a Pull Request

1. Go to your fork on GitHub: `github.com/YOUR_USERNAME/project`
2. GitHub will show a banner: **"Compare & pull request"** — click it
3. Fill in:
   - **Title**: Clear and descriptive (e.g. "Fix typo in README")
   - **Description**: What you changed and why
4. Click **Create Pull Request**

---

## Step 8: Respond to Review Feedback

If the maintainer requests changes:

```bash
# Make the requested changes locally
git add .
git commit -m "fix: address review feedback"

# Push to the same branch — PR updates automatically!
git push origin fix/typo-in-readme
```

---

## Step 9: After Your PR is Merged

```bash
# Sync your fork's main with upstream
git checkout main
git fetch upstream
git merge upstream/main
git push origin main

# Delete your feature branch (it's merged, no longer needed)
git branch -d fix/typo-in-readme
git push origin --delete fix/typo-in-readme
```

---

## Fork vs Clone — Quick Comparison

| | Fork | Clone |
|---|---|---|
| Creates copy on GitHub | ✅ Yes | ❌ No |
| Creates copy locally | ❌ (clone separately) | ✅ Yes |
| Can push directly | Only to your fork | Depends on permissions |
| Used for | Contributing to others' repos | Working on your own repos |

---

## Common Fork Workflow Commands — Quick Reference

```bash
# One-time setup
git remote add upstream git@github.com:owner/repo.git

# Before starting any new work
git fetch upstream
git checkout main
git merge upstream/main
git checkout -b my-new-feature

# After making changes
git add -p                           # Stage selectively
git commit -m "type: description"
git push -u origin my-new-feature

# After PR is merged
git checkout main
git merge upstream/main
git push origin main
git branch -d my-new-feature
```

---

## Next Steps
- ⬅️ [Back to Home](../README.md)
- 📚 [Official GitHub Docs: Forking a repo](https://docs.github.com/en/get-started/quickstart/fork-a-repo)
