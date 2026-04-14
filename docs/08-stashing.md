# 8. Stashing & Temporary Storage 📦

[← Back to Home](../README.md)

> 💡 **What is stashing?** Like putting your unfinished work in a drawer so you can quickly switch tasks — then come back and pick up right where you left off.

---

## Basic Stash Operations

```bash
# Stash your current changes (staged + unstaged)
git stash
# Your working directory is now clean!

# Stash with a descriptive message (modern syntax)
git stash push -m "WIP: half-done login feature"

# List all your stashes
git stash list
# stash@{0}: WIP: half-done login feature
# stash@{1}: On main: experimental changes

# Apply the most recent stash (keeps it in the stash list)
git stash apply

# Apply AND remove from stash list
git stash pop
```

---

## Working with Multiple Stashes

```bash
# Apply a specific stash by index
git stash apply stash@{2}

# Show what's in a stash before applying
git stash show stash@{0}
git stash show -p stash@{0}   # Full diff

# Drop (delete) a specific stash
git stash drop stash@{1}

# Clear ALL stashes (careful!)
git stash clear
```

> ⚠️ **WARNING:** `git stash clear` permanently deletes all stashes.

---

## Advanced Stash Usage

```bash
# Stash only unstaged changes (keep staged changes)
git stash --keep-index

# Also stash untracked files
git stash -u
# or
git stash --include-untracked

# Create a branch from a stash (useful when stash conflicts with current code)
git stash branch feature/from-stash stash@{0}
```

---

## Stash Workflow Example

```
1. You're working on feature X...
   git stash push -m "WIP: feature X"

2. Switch to fix an urgent bug on main:
   git checkout main
   # fix bug, commit

3. Come back to your feature:
   git checkout feature/x
   git stash pop   ← Your work is back!
```

---

## Next Steps
- ➡️ [Advanced Git Techniques](./09-advanced-techniques.md)
