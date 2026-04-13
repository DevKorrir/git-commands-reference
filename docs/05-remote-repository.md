# 5. Remote Repository Mastery 🌐

[← Back to Home](../README.md)

---

## Managing Multiple Remotes

```bash
# Add multiple remotes
git remote add upstream https://github.com/original/repo.git
git remote add fork https://github.com/yourusername/repo.git

# List all remotes
git remote -v

# Remove a remote
git remote remove upstream
```

---

## Changing Remote Repository URL

### Method 1: Change Existing Remote URL

```bash
# Change origin to point to new repository
git remote set-url origin https://github.com/new-username/new-repo.git

# Verify the change
git remote -v

# Test the connection
git remote show origin
```

### Method 2: Remove and Re-add Remote

```bash
git remote remove origin
git remote add origin https://github.com/new-username/new-repo.git
git push -u origin main
```

### Method 3: Switch Between HTTPS and SSH

```bash
# Switch from HTTPS to SSH
git remote set-url origin git@github.com:username/repo.git

# Switch from SSH to HTTPS
git remote set-url origin https://github.com/username/repo.git
```

---

## Common Scenarios

| Scenario | Command |
|---|---|
| Transferred repo ownership | `git remote set-url origin https://github.com/user2/repo.git` |
| Forked a repo | `git remote set-url origin https://github.com/yourusername/fork.git` |
| Company moved to GitLab | `git remote set-url origin https://gitlab.com/company/project.git` |
| New local repo to new remote | `git remote add origin <url>` → `git push -u origin main` |

---

## Fetching and Pulling Strategies

```bash
# Fetch all branches from all remotes (doesn't change your files)
git fetch --all

# Fetch specific remote
git fetch origin

# Fetch and prune deleted remote branches
git fetch --prune
# Keeps your local remote-tracking list in sync

# Pull with rebase (cleaner, linear history)
git pull --rebase origin main

# Pull a specific branch
git pull origin feature/specific-branch
```

> 💡 **Tip:** `git fetch` is always safe — it downloads info but never changes your working files. `git pull` = `git fetch` + `git merge`.

---

## Advanced Push Operations

```bash
# Push all local branches
git push --all origin

# Push tags
git push --tags
```

> ⚠️ **WARNING:** Force push can destroy others' work on shared branches!

```bash
# Force push (overwrites remote history — dangerous!)
git push --force origin main

# Safer force push — fails if someone else pushed since your last pull
git push --force-with-lease origin main

# Push new branch and set upstream
git push -u origin feature/new-branch

# Push to a differently-named remote branch
git push origin local-branch:remote-branch
# e.g. git push origin develop:staging
```

---

## Next Steps
- ➡️ [Time Travel: Undoing & Fixing](./06-undoing-fixing.md)
- ➡️ [GitHub Workflow (Forks & PRs)](./15-github-workflow.md)
