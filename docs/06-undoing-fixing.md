# 6. Time Travel: Undoing & Fixing ⏰️

[← Back to Home](../README.md)

---

## Working Directory Changes

```bash
# Discard changes in a specific file
git checkout -- filename.txt
# or (newer syntax)
git restore filename.txt

# Discard ALL changes in working directory
git checkout -- .
git restore .
```

> 💡 **Note:** These commands do NOT affect untracked files (files Git doesn't know about yet).

```bash
# Remove untracked files (preview first!)
git clean -n          # Dry run — shows what WOULD be deleted
git clean -f          # Remove untracked files
git clean -fd         # Remove untracked files AND directories

# Untrack a specific file (keeps it on disk, removes from Git)
git rm --cached <file>
# e.g. git rm --cached app/google-services.json
```

> ⚠️ **WARNING:** `git clean -f` is permanent! Always run `git clean -n` first to preview.

---

## Staging Area Operations

```bash
# Unstage a specific file (undo git add)
git reset HEAD filename.txt
# or (newer syntax)
git restore --staged filename.txt

# Unstage ALL files
git reset HEAD
git restore --staged .
```

---

## Commit History Manipulation

```
RESET MODES AT A GLANCE:
─────────────────────────────────────────────────────────
 --soft    Undo commit     ✅ Keep in staging   ✅ Keep files
 --mixed   Undo commit     ❌ Remove from stage ✅ Keep files  (DEFAULT)
 --hard    Undo commit     ❌ Remove from stage ❌ LOSE files
─────────────────────────────────────────────────────────
```

### Soft Reset (Keep Changes Staged)

```bash
# Undo last commit, keep changes staged and ready to re-commit
git reset --soft HEAD~1

# Undo multiple commits
git reset --soft HEAD~3
```

### Mixed Reset (Default — Keep Files But Unstage)

```bash
# Undo last commit, keep changes in working directory (unstaged)
git reset HEAD~1

# Reset to specific commit
git reset abc1234
```

### Hard Reset (Nuclear Option! 💀)

```bash
# DANGER: Permanently loses ALL uncommitted changes
git reset --hard HEAD~1

# Reset to specific commit (lose everything after it)
git reset --hard abc1234

# Reset to match remote state exactly
git reset --hard origin/main
```

> ⚠️ **DANGER:** `git reset --hard` is irreversible for uncommitted changes. Only use it if you're 100% sure!

### Safe Undoing with Revert (Public Repo Friendly ✅)

```bash
# Create a new commit that reverses the last commit
git revert HEAD

# Revert a specific commit
git revert abc1234

# Revert a merge commit
git revert -m 1 merge-commit-hash
```

> 💡 **`revert` vs `reset`:** Use `git revert` on shared/public branches — it adds a new "undo" commit without rewriting history. Use `git reset` only on your own local commits that haven't been pushed.

---

## Next Steps
- ➡️ [Investigation & Information](./07-investigation.md)
- ➡️ [Emergency Git Commands](./11-emergency.md)
