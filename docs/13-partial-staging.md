# 13. Partial Staging with `git add -p` 🎯

[← Back to Home](../README.md)

> 💡 **Why does this matter?** This is one of the most-used tools by professional developers but is rarely taught to beginners. It lets you commit only *part* of your changes in a file — so each commit stays clean, focused, and meaningful.

---

## The Problem It Solves

Imagine you fixed a bug AND added a new feature — both in the same file. You want two separate commits (one per change) instead of bundling them together. `git add -p` to the rescue!

---

## Basic Usage

```bash
# Start interactive/patch staging for a specific file
git add -p filename.txt

# Or for all changed files at once
git add -p
```

Git will show you each "hunk" (chunk of changes) one at a time and ask what to do with it.

---

## What Each Option Means

When Git shows a hunk, you'll see a prompt:

```
Stage this hunk [y,n,q,a,d,s,e,?]?
```

| Key | What It Does |
|---|---|
| `y` | **Yes** — stage this hunk |
| `n` | **No** — skip this hunk (don't stage) |
| `q` | **Quit** — stop and keep whatever you've staged so far |
| `a` | **All** — stage this hunk AND all remaining hunks in this file |
| `d` | **Don't** — skip this hunk AND all remaining hunks in this file |
| `s` | **Split** — split this hunk into smaller pieces (very useful!) |
| `e` | **Edit** — manually edit what gets staged (most precise control) |
| `?` | **Help** — show all options |

---

## Step-by-Step Example

You have this file with two changes:

```diff
# You added a greeting function...
+def greet(name):
+    return f"Hello, {name}!"

# ...AND fixed a typo in a different function
-def calcualte_total(items):
+def calculate_total(items):
     return sum(items)
```

With `git add -p` you stage just the typo fix:

```bash
git add -p math.py

# Git shows first hunk (the greeting function)
Stage this hunk? [y,n,q,a,d,s,e,?] n    ← Skip it

# Git shows second hunk (the typo fix)
Stage this hunk? [y,n,q,a,d,s,e,?] y    ← Stage it!

git commit -m "fix: correct typo in calculate_total"

# Now stage and commit the feature separately
git add -p math.py
# Stage this hunk? y
git commit -m "feat: add greet function"
```

Result: **2 clean, meaningful commits** instead of 1 mixed one. ✅

---

## Splitting Hunks (`s`)

Sometimes Git shows a large hunk that contains multiple separate changes. Use `s` to split it:

```bash
Stage this hunk? [y,n,q,a,d,s,e,?] s
# Git tries to split into smaller pieces
# Then prompts you for each smaller piece
```

> 💡 **Tip:** If `s` says "cannot split" (because the changes are adjacent), use `e` to manually edit the diff.

---

## Manual Editing (`e`)

When a hunk can't be split automatically:

```bash
Stage this hunk? [y,n,q,a,d,s,e,?] e
# Opens your editor with the diff
# - Leave lines with + to include them
# - Change + to space to exclude addition
# - Change - to space to exclude deletion (keep the line)
# Save and close the editor
```

---

## Quick Workflow Reference

```bash
# See what would be staged before committing
git diff --staged

# Stage specific lines of a file
git add -p filename.txt

# Commit only staged changes
git commit -m "type: focused description"

# Verify the split worked — check remaining diff
git diff filename.txt
```

---

## When to Use `git add -p`

| Situation | Use it? |
|---|---|
| Mixed changes (bug fix + feature) in same file | ✅ Yes |
| Debugging code mixed with real changes | ✅ Yes |
| You want atomic, reviewable commits | ✅ Yes |
| Simple, single-purpose change to a file | ❌ `git add file` is fine |

---

## Next Steps
- ➡️ [SSH Key Setup](./14-ssh-setup.md)
- ➡️ [GitHub Workflow (Forks & PRs)](./15-github-workflow.md)
