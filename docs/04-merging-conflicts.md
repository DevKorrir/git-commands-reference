# 4. Merge Strategies & Conflict Resolution 🔀

[← Back to Home](../README.md)

---

## 🤝 Basic Merging

```bash
# Switch to target branch (usually main)
git checkout main

# Merge feature branch into current branch
git merge feature/awesome-feature

# Delete merged branch (clean up!)
git branch -d feature/awesome-feature
```

---

## Advanced Merge Strategies

### Accept Their Changes (Remote/Other Branch)

```bash
# When merging, automatically accept their changes for conflicts
git merge feature/other-branch -X theirs

# Or during pull
git pull origin main -X theirs
```

### Keep Your Changes (Local)

```bash
# When merging, prefer your local changes
git merge feature/other-branch -X ours

# During pull
git pull origin main -X ours
```

### No Fast-Forward Merge (Preserve Branch History)

```bash
git merge --no-ff feature/awesome-feature
# Always creates a merge commit, preserving branch history
```

```
Before:  main: ──A──B
                     \
         feature:     ──C──D──E──F

After (--no-ff):
         main: ──A──B────────────────M  ← Merge commit
                     \              /
         feature:     ──C──D──E──F
```

> 💡 **Note:** `--no-ff` keeps all individual feature branch commits and adds a new merge commit. Merging a Pull Request on GitHub is essentially a remote `git merge --no-ff`.

### Squash Merge (Clean History)

```bash
git merge --squash feature/many-commits
git commit -m "Add awesome feature"
# Combines all commits from feature branch into ONE commit
```

```
Before:  main: ──A──B
                     \
         feature:     ──C──D──E──F

After (--squash):
         main: ──A──B──S  ← Single squash commit (C+D+E+F combined)
```

> 💡 **When to use:** `--squash` is great when your feature branch has messy "WIP" commits you don't want in history.

---

## 🔧 Handling Merge Conflicts Like a Pro

### When Conflicts Happen 💥

```bash
# After a failed merge, see which files have conflicts
git status

# List only conflicted files
git diff --name-only --diff-filter=U
```

### Manual Conflict Resolution

```bash
# Open conflicted file — you'll see conflict markers:
# <<<<<<< HEAD
# Your changes here
# =======
# Their changes here
# >>>>>>> branch-name

# 1. Edit the file to keep what you want
# 2. Remove ALL conflict markers (<<<, ===, >>>)
# 3. Stage the resolved file
git add conflicted-file.txt

# 4. Complete the merge
git commit -m "Merge: resolved conflict in conflicted-file.txt"
```

### Automated Conflict Resolution

```bash
# Accept ALL their changes (entire repo)
git checkout --theirs .
git add .
git commit

# Accept ALL your changes (entire repo)
git checkout --ours .
git add .
git commit

# Open a visual merge tool
git mergetool
```

### Abort Merge (Emergency Exit! 🚨)

```bash
git merge --abort
# Cancels the merge and returns to the state before you started
```

---

## Next Steps
- ➡️ [Remote Repository Mastery](./05-remote-repository.md)
