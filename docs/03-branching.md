# 3. Mastering Branches 🌿

[← Back to Home](../README.md)

> 💡 **Why branches?** Think of branches as parallel universes for your code. You can experiment on a feature branch without breaking the main codebase.

---

## Branch Management Basics

```bash
# See all branches (local + remote)
git branch -a
# * main                    (current branch marked with *)
#   remotes/origin/main

# Create a new branch
git branch feature/awesome-feature

# Switch to branch (classic way)
git checkout feature/awesome-feature

# Switch to branch (modern way — Git 2.23+)
git switch feature/awesome-feature

# Create AND switch in one command (most common)
git checkout -b feature/new-feature
# or
git switch -c feature/new-feature
```

---

## Advanced Branch Operations

```bash
# Rename current branch
git branch -m new-branch-name

# Rename any branch
git branch -m old-name new-name

# Copy a branch
git checkout -b new-branch existing-branch

# Delete local branch (safe — only deletes if merged)
git branch -d feature/completed-feature

# Force delete local branch
git branch -D feature/unwanted-feature
```

> ⚠️ **WARNING:** `git branch -D` is destructive — any unmerged work on that branch will be lost!

```bash
# Delete remote branch
git push origin --delete feature/old-feature
```

---

## Branch Tracking and Upstream

```bash
# Set upstream for current branch
git branch --set-upstream-to=origin/main

# Push new branch and set upstream
git push -u origin feature/my-feature

# See tracking relationships for all local branches
git branch -vv
# main   a1b2c3d [origin/main] My last commit message
```

---

## Next Steps
- ➡️ [Merge Strategies & Conflict Resolution](./04-merging-conflicts.md)
