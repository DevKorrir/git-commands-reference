# 7. Investigation & Information 🕵️

[← Back to Home](../README.md)

---

## Viewing Commit History

```bash
# Full commit log
git log

# Compact one-line-per-commit view (most useful!)
git log --oneline

# Last 5 commits, one line each
git log --oneline -5

# Visual branch graph
git log --oneline --graph --all
# Shows a visual tree of all branches and merges

# Log with stats (which files changed, how many lines)
git log --stat

# Search commits by author
git log --author="John"

# Search commits by message keyword
git log --grep="fix bug"

# Show commits in a date range
git log --after="2024-01-01" --before="2024-06-01"

# Show what changed in each commit
git log -p
```

---

## Inspecting Changes

```bash
# Show unstaged changes (what you changed but haven't git added)
git diff

# Show staged changes (what you've git added but not committed)
git diff --staged
# also works: git diff --cached

# Show changes between two commits
git diff abc1234 def5678

# Show changes between two branches
git diff main..feature/my-feature

# Show only filenames that changed (not the full diff)
git diff --name-only
```

---

## Inspecting Specific Commits

```bash
# Show what a specific commit changed
git show abc1234

# Show a specific file at a specific commit
git show abc1234:path/to/file.txt

# Show the latest commit on current branch
git show HEAD
```

---

## Finding Who Changed What (Blame 🔍)

```bash
# Show who last modified each line of a file
git blame filename.txt
# Output: abc1234 (John Doe 2024-05-01) line content here

# Blame with email addresses
git blame -e filename.txt

# Blame a specific range of lines (lines 10–30)
git blame -L 10,30 filename.txt
```

> 💡 **Use case:** When you find a bug and want to know who wrote that line and why (check the commit message!).

---

## Contributor Statistics

```bash
# Show commit count per author
git shortlog -sn

# Full shortlog with commit messages
git shortlog

# Count total commits in repo
git rev-list --count HEAD
```

---

## Next Steps
- ➡️ [Stashing & Temporary Storage](./08-stashing.md)
