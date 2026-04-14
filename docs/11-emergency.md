# 11. Emergency Git Commands 🚨

[← Back to Home](../README.md)

---

## Git Reflog — Your Safety Net

> 💡 **Reflog is a superpower.** Git records every movement of HEAD (even through resets and branch deletions) for ~90 days. You can recover almost anything!

```bash
# See a log of every action Git has taken
git reflog
# HEAD@{0}: reset: moving to HEAD~1
# HEAD@{1}: commit: Add login page
# HEAD@{2}: commit: Fix navbar bug
# HEAD@{3}: checkout: moving from feature to main

# Recover a commit you accidentally reset away
git reflog
# Find the SHA of the commit you want (e.g. abc1234)
git reset --hard abc1234
# OR create a new branch at that commit:
git checkout -b recovery-branch abc1234
```

---

## Recovering Lost Commits

```bash
# Find the lost commit SHA in reflog
git reflog | grep "the thing you remember"

# Restore it to a new branch
git checkout -b rescued-branch abc1234

# Or apply it with cherry-pick
git cherry-pick abc1234
```

---

## Detached HEAD State

```bash
# "Detached HEAD" means you're not on any branch
# This happens when you checkout a specific commit:
git checkout abc1234
# WARNING: You are in 'detached HEAD' state

# To save any work you do here, create a branch:
git checkout -b my-new-branch

# Or just go back to a named branch
git checkout main
```

---

## Recovering a Deleted Branch

```bash
# Find the last commit SHA that was on the deleted branch
git reflog

# Recreate the branch at that commit
git checkout -b recovered-branch abc1234
```

---

## Fix Wrong Commit Message

```bash
# Fix the most recent commit message (before pushing!)
git commit --amend -m "Corrected commit message"

# Add a forgotten file to your last commit
git add forgotten-file.txt
git commit --amend --no-edit   # Keeps existing message
```

> ⚠️ **WARNING:** `git commit --amend` rewrites history. Only use it on commits that haven't been pushed yet!

---

## Nuclear Recovery

```bash
# Something went terribly wrong — reset to exactly match remote
git fetch origin
git reset --hard origin/main
git clean -fd

# Find ALL unreachable objects (dangling commits, blobs)
git fsck --lost-found
```

---

## Next Steps
- ➡️ [Pro Tips & Best Practices](./12-pro-tips.md)
