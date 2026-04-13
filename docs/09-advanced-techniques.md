# 9. Advanced Git Techniques 🚀

[← Back to Home](../README.md)

---

## Git Rebase (Rewrite History)

> 💡 **Rebase vs Merge:** Rebase creates a cleaner, linear history. Merge preserves the true branch structure. Neither is wrong — it depends on your team's preference.

```bash
# Rebase current branch onto main
git rebase main
# "Replays" your commits on top of main's latest commit
```

```
Before rebase:
  main:    ──A──B──C
                \
  feature:       ──D──E

After: git rebase main (while on feature)
  main:    ──A──B──C
                    \
  feature:           ──D'──E'  ← New commits (replayed on top of C)
```

```bash
# Interactive rebase — edit, squash, reorder last 3 commits
git rebase -i HEAD~3
# Opens editor where you can:
# pick  → keep commit as-is
# squash → merge into previous commit
# reword → change commit message
# drop   → delete commit entirely

# Abort rebase if something goes wrong
git rebase --abort

# Continue rebase after resolving conflicts
git rebase --continue
```

> ⚠️ **WARNING:** Never rebase commits that have already been pushed to a shared branch — it rewrites history and causes problems for teammates.

---

## Cherry-Pick (Take One Commit From Another Branch)

```bash
# Apply a specific commit from another branch to current branch
git cherry-pick abc1234

# Cherry-pick multiple commits
git cherry-pick abc1234 def5678

# Cherry-pick a range of commits
git cherry-pick abc1234^..def5678

# Cherry-pick without auto-committing (stage changes only)
git cherry-pick --no-commit abc1234
```

> 💡 **Use case:** You fixed a bug on a feature branch and want to apply JUST that fix to `main` without merging the whole feature.

---

## Git Bisect (Find the Bug's Origin)

```bash
# Start a binary search through commit history
git bisect start

# Mark current state as bad (bug exists here)
git bisect bad

# Mark a known-good commit (when bug didn't exist)
git bisect good abc1234

# Git checks out commits between them — test each one:
# If bug exists:  git bisect bad
# If bug is gone: git bisect good
# Git narrows it down automatically — usually 7-8 steps!

# When done, reset back to normal
git bisect reset
```

> 💡 **Use case:** "My app broke somewhere in the last 200 commits — which one introduced the bug?" Bisect finds it in ~8 steps!

---

## Git Tags (Mark Important Points / Releases)

```bash
# Create a lightweight tag
git tag v1.0.0

# Create an annotated tag with message (recommended for releases)
git tag -a v1.0.0 -m "Version 1.0.0 — First stable release"

# Tag a specific commit
git tag -a v0.9.0 abc1234 -m "Beta release"

# List all tags
git tag

# Show tag details
git show v1.0.0

# Push a specific tag to remote
git push origin v1.0.0

# Push ALL tags to remote
git push --tags

# Delete a local tag
git tag -d v1.0.0

# Delete a remote tag
git push origin --delete v1.0.0
```

---

## Next Steps
- ➡️ [Configuration & Customization](./10-configuration.md)
- ➡️ [Partial Staging (git add -p)](./13-partial-staging.md)
