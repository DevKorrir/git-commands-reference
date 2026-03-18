# 🔰 Git Commands Reference 🔰

> A helpful manual for navigating the Git world — a compilation of the most common Git commands with clear explanations. Whether you're a total beginner or need a quick refresher, this guide has you covered. Cheers to coding! 🚀

---

## 🗺️ Table of Contents

1. [Getting Started](#1-getting-started)
2. [The Complete Workflow](#2-the-complete-workflow)
3. [Mastering Branches](#3-mastering-branches)
4. [Merge Strategies & Conflict Resolution](#4-merge-strategies--conflict-resolution)
5. [Remote Repository Mastery](#5-remote-repository-mastery)
6. [Time Travel: Undoing & Fixing](#6-time-travel-undoing--fixing)
7. [Investigation & Information](#7-investigation--information)
8. [Stashing & Temporary Storage](#8-stashing--temporary-storage)
9. [Advanced Git Techniques](#9-advanced-git-techniques)
10. [Configuration & Customization](#10-configuration--customization)
11. [Emergency Git Commands](#11-emergency-git-commands)
12. [Pro Tips & Best Practices](#12-pro-tips--best-practices)

---

## 1. Getting Started 🚦

### The Very Beginning

Make sure Git is installed on your machine:

```bash
# Check if Git is installed
git --version
# Output: git version 2.x.x
```

> 💡 **Beginner Tip:** If you get "command not found", download Git from [git-scm.com](https://git-scm.com/)

### Creating Your First Repository

```bash
# Initialize a new repository
git init
# This creates a hidden .git folder — the magic happens here!
```

### Essential First Steps

```bash
# Check what's happening (always a good idea!)
git status
# Output: On branch master (or main)
#         No commits yet
#         nothing to commit
```

### How Git Tracks Your Work (Visual Overview)

```
┌─────────────────────────────────────────────────────────┐
│                    GIT WORKFLOW                         │
│                                                         │
│  Working Dir   Staging Area    Local Repo    Remote     │
│  (your files)  (git add)       (git commit)  (GitHub)  │
│                                                         │
│  [Edit files] ──git add──► [Staged] ──git commit──►    │
│                                          [Committed]    │
│                                               │          │
│  [Updated] ◄──git pull──                git push──►    │
│                            [Remote Repo (origin)]       │
└─────────────────────────────────────────────────────────┘
```

---

## 2. The Complete Workflow 🔄

### Real-World Scenario: Starting a New Project

#### Step 1: Initialize and Connect

```bash
# Start your local repository
git init

# Add your remote repository (where your code will live online)
git remote add origin https://github.com/username/your-repo.git

# Check your remote is set up correctly
git remote -v
# origin  https://github.com/username/your-repo.git (fetch)
# origin  https://github.com/username/your-repo.git (push)
```

#### Step 2: The Great Branch Migration (Master → Main)

```bash
# If you're on 'master' and want to switch to 'main'
git branch -M main
# This renames your current branch to 'main'

# Or create main branch if it doesn't exist
git checkout -b main
```

> 💡 **Beginner Tip:** Modern Git uses `main` as the default branch name. If you see `master`, you can rename it!

#### Step 3: Your First Commit

```bash
# Create your first file
echo "# My Awesome Project" > README.md

# Add file to staging area
git add README.md
# Or add everything at once
git add .

# Make your first commit
git commit -m "Initial commit: Added README file"
```

#### Step 4: Connect with Remote Repository

```bash
# Push and set upstream branch
git push -u origin main
# The -u flag sets main as the default tracking branch (only needed once!)
```

#### Step 5: Handling an Existing Remote Repository 🤝

```bash
# If remote repository already has content, pull it first
git pull origin main

# If you get "fatal: refusing to merge unrelated histories"
git pull origin main --allow-unrelated-histories
# This merges two separate Git histories — very common when starting!
```

---

## 3. Mastering Branches 🌿

> 💡 **Why branches?** Think of branches as parallel universes for your code. You can experiment on a feature branch without breaking the main codebase.

### Branch Management Basics

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

### Advanced Branch Operations

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

### Branch Tracking and Upstream

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

## 4. Merge Strategies & Conflict Resolution 🔀

### 🤝 Basic Merging

```bash
# Switch to target branch (usually main)
git checkout main

# Merge feature branch into current branch
git merge feature/awesome-feature

# Delete merged branch (clean up!)
git branch -d feature/awesome-feature
```

### Advanced Merge Strategies

#### Accept Their Changes (Remote/Other Branch)

```bash
# When merging, automatically accept their changes for conflicts
git merge feature/other-branch -X theirs

# Or during pull
git pull origin main -X theirs
```

#### Keep Your Changes (Local)

```bash
# When merging, prefer your local changes
git merge feature/other-branch -X ours

# During pull
git pull origin main -X ours
```

#### No Fast-Forward Merge (Preserve Branch History)

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

#### Squash Merge (Clean History)

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

### 🔧 Handling Merge Conflicts Like a Pro

#### When Conflicts Happen 💥

```bash
# After a failed merge, see which files have conflicts
git status

# List only conflicted files
git diff --name-only --diff-filter=U
```

#### Manual Conflict Resolution

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

#### Automated Conflict Resolution

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

#### Abort Merge (Emergency Exit! 🚨)

```bash
git merge --abort
# Cancels the merge and returns to the state before you started
```

---

## 5. Remote Repository Mastery 🌐

### Managing Multiple Remotes

```bash
# Add multiple remotes
git remote add upstream https://github.com/original/repo.git
git remote add fork https://github.com/yourusername/repo.git

# List all remotes
git remote -v

# Remove a remote
git remote remove upstream
```

### Changing Remote Repository URL

#### Method 1: Change Existing Remote URL

```bash
# Change origin to point to new repository
git remote set-url origin https://github.com/new-username/new-repo.git

# Verify the change
git remote -v

# Test the connection
git remote show origin
```

#### Method 2: Remove and Re-add Remote

```bash
git remote remove origin
git remote add origin https://github.com/new-username/new-repo.git
git push -u origin main
```

#### Method 3: Switch Between HTTPS and SSH

```bash
# Switch from HTTPS to SSH
git remote set-url origin git@github.com:username/repo.git

# Switch from SSH to HTTPS
git remote set-url origin https://github.com/username/repo.git
```

### Common Scenarios

| Scenario | Command |
|---|---|
| Transferred repo ownership | `git remote set-url origin https://github.com/user2/repo.git` |
| Forked a repo | `git remote set-url origin https://github.com/yourusername/fork.git` |
| Company moved to GitLab | `git remote set-url origin https://gitlab.com/company/project.git` |
| New local repo to new remote | `git remote add origin <url>` → `git push -u origin main` |

### Fetching and Pulling Strategies

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

> 💡 **Tip:** `git fetch` is always safe — it downloads info but never changes your working files. `git pull` = `git fetch` + merge (or rebase), depending on your configuration/flags.

### Advanced Push Operations

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

## 6. Time Travel: Undoing & Fixing ⏰️

### Working Directory Changes

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

### Staging Area Operations

```bash
# Unstage a specific file (undo git add)
git reset HEAD filename.txt
# or (newer syntax)
git restore --staged filename.txt

# Unstage ALL files
git reset HEAD
git restore --staged .
```

### Commit History Manipulation

```
RESET MODES AT A GLANCE:
─────────────────────────────────────────────────────────
 --soft    Undo commit     ✅ Keep in staging   ✅ Keep files
 --mixed   Undo commit     ❌ Remove from stage ✅ Keep files  (DEFAULT)
 --hard    Undo commit     ❌ Remove from stage ❌ LOSE files
─────────────────────────────────────────────────────────
```

#### Soft Reset (Keep Changes Staged)

```bash
# Undo last commit, keep changes staged and ready to re-commit
git reset --soft HEAD~1

# Undo multiple commits
git reset --soft HEAD~3
```

#### Mixed Reset (Default — Keep Files But Unstage)

```bash
# Undo last commit, keep changes in working directory (unstaged)
git reset HEAD~1

# Reset to specific commit
git reset abc1234
```

#### Hard Reset (Nuclear Option! 💀)

```bash
# DANGER: Permanently loses ALL uncommitted changes
git reset --hard HEAD~1

# Reset to specific commit (lose everything after it)
git reset --hard abc1234

# Reset to match remote state exactly
git reset --hard origin/main
```

> ⚠️ **DANGER:** `git reset --hard` is irreversible for uncommitted changes. Only use it if you're 100% sure!

#### Safe Undoing with Revert (Public Repo Friendly ✅)

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

## 7. Investigation & Information 🕵️

### Viewing Commit History

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

### Inspecting Changes

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

### Inspecting Specific Commits

```bash
# Show what a specific commit changed
git show abc1234

# Show a specific file at a specific commit
git show abc1234:path/to/file.txt

# Show the latest commit on current branch
git show HEAD
```

### Finding Who Changed What (Blame 🔍)

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

### Contributor Statistics

```bash
# Show commit count per author
git shortlog -sn

# Full shortlog with commit messages
git shortlog

# Count total commits in repo
git rev-list --count HEAD
```

---

## 8. Stashing & Temporary Storage 📦

> 💡 **What is stashing?** Like putting your unfinished work in a drawer so you can quickly switch tasks — then come back and pick up right where you left off.

### Basic Stash Operations

```bash
# Stash your current changes (staged + unstaged)
git stash
# Your working directory is now clean!

# Stash with a descriptive message
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

### Working with Multiple Stashes

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

### Advanced Stash Usage

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

### Stash Workflow Example

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

## 9. Advanced Git Techniques 🚀

### Git Rebase (Rewrite History)

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
# pick  → keep commit
# squash → merge into previous commit
# reword → change commit message
# drop   → delete commit entirely

# Abort rebase if something goes wrong
git rebase --abort

# Continue rebase after resolving conflicts
git rebase --continue
```

> ⚠️ **WARNING:** Never rebase commits that have already been pushed to a shared branch — it rewrites history and causes problems for teammates.

### Cherry-Pick (Take One Commit From Another Branch)

```bash
# Apply a specific commit from another branch to current branch
git cherry-pick abc1234
# Makes a copy of that commit on your current branch

# Cherry-pick multiple commits
git cherry-pick abc1234 def5678

# Cherry-pick a range of commits
git cherry-pick abc1234^..def5678

# Cherry-pick without auto-committing (stage changes only)
git cherry-pick --no-commit abc1234
```

> 💡 **Use case:** You merged a bug fix to your feature branch, but want to also apply JUST that fix to main without merging the whole feature.

### Git Bisect (Find the Bug's Origin)

```bash
# Start a binary search through your commit history
git bisect start

# Mark the current state as bad (bug exists here)
git bisect bad

# Mark a known-good commit (when bug didn't exist)
git bisect good abc1234

# Git will checkout commits in between — test each one:
# If bug exists:  git bisect bad
# If bug is gone: git bisect good
# Git narrows it down automatically!

# When finished, reset back to normal
git bisect reset
```

> 💡 **Use case:** "My app broke sometime in the last 200 commits — which one introduced the bug?" Bisect finds it in ~8 steps instead of 200!

### Git Tags (Mark Important Points)

```bash
# Create a lightweight tag
git tag v1.0.0

# Create an annotated tag (with message — recommended for releases)
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

## 10. Configuration & Customization ⚙️

### Essential First-Time Setup

```bash
# Set your name (appears in commit history)
git config --global user.name "Your Name"

# Set your email (should match your GitHub email)
git config --global user.email "you@example.com"

# Set default branch name to 'main' for new repos
git config --global init.defaultBranch main

# Set preferred editor for commit messages
git config --global core.editor "code --wait"   # VS Code
git config --global core.editor "nano"          # Nano
git config --global core.editor "vim"           # Vim
```

### Viewing Configuration

```bash
# See all your global config settings
git config --global --list

# See local repo config (overrides global)
git config --local --list

# Check a specific setting
git config user.name

# See where a setting comes from
git config --show-origin user.name
```

### Line Endings (Cross-Platform Fix)

```bash
# Windows: auto-convert line endings
git config --global core.autocrlf true

# Mac/Linux: don't convert
git config --global core.autocrlf input

# Fix long file path issues on Windows
git config --system core.longpaths true
```

### Git Aliases (Create Shortcuts!)

```bash
# Create shortcuts for common commands
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm "commit -m"
git config --global alias.last "log -1 HEAD"

# Now you can type:
git st        # = git status
git co main   # = git checkout main
git last      # = show last commit

# Fancy log alias
git config --global alias.lg "log --oneline --graph --all --decorate"
```

### Useful Global Config Settings

```bash
# Speed up large repositories
git config --global core.preloadindex true
git config --global core.fscache true

# Auto-setup remote tracking when pushing new branches
git config --global push.autoSetupRemote true

# Use 'main' as default branch for new repos
git config --global init.defaultBranch main

# Always use rebase instead of merge on pull
git config --global pull.rebase true
```

---

## 11. Emergency Git Commands 🚨

### Git Reflog — Your Safety Net

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

### Recovering Lost Commits

```bash
# Find the lost commit SHA in reflog
git reflog | grep "the thing you remember"

# Restore it to a new branch
git checkout -b rescued-branch abc1234

# Or apply it with cherry-pick
git cherry-pick abc1234
```

### Detached HEAD State

```bash
# "Detached HEAD" means you're not on any branch
# This happens when you checkout a specific commit:
git checkout abc1234
# WARNING: You are in 'detached HEAD' state

# To save any work you do here, create a branch:
git checkout -b my-new-branch

# Or just go back to a branch
git checkout main
```

### Recovering a Deleted Branch

```bash
# Find the last commit SHA that was on the deleted branch
git reflog

# Recreate the branch at that commit
git checkout -b recovered-branch abc1234
```

### Fix Wrong Commit Message

```bash
# Fix the most recent commit message (before pushing!)
git commit --amend -m "Corrected commit message"

# Add a forgotten file to your last commit
git add forgotten-file.txt
git commit --amend --no-edit   # Keeps existing message
```

> ⚠️ **WARNING:** `git commit --amend` rewrites history. Only use it on commits that haven't been pushed yet!

### Nuclear Recovery

```bash
# Something went terribly wrong — reset to exactly match remote
git fetch origin
git reset --hard origin/main
git clean -fd

# Find ALL unreachable objects (dangling commits, blobs)
git fsck --lost-found
```

---

## 12. Pro Tips & Best Practices 💎

### Commit Message Magic

```bash
# Great commit message format:
# type: Brief description (50 chars max)
#
# More detailed explanation if needed (wrap at 72 chars)
#
# - Use bullet points for multiple changes
# - Reference issues: Fixes #123

# Example:
git commit -m "feat: Add user authentication system

- Implement JWT token handling
- Add login/logout endpoints
- Create user registration flow
Fixes #42"
```

### Conventional Commit Types

| Type | Emoji | When to Use |
|---|---|---|
| `feat` | ✨ | New feature |
| `fix` | 🐛 | Bug fix |
| `docs` | 📚 | Documentation only |
| `style` | 🎨 | Formatting, no code change |
| `refactor` | ♻️ | Code restructuring |
| `perf` | ⚡ | Performance improvement |
| `test` | ✅ | Adding/fixing tests |
| `chore` | 🔧 | Maintenance, build tasks |

### Workflow Strategies

#### Git Flow (Complex Projects)

```
main        # Production-ready code only
develop     # Integration branch — ongoing work
feature/*   # New features (branch from develop)
release/*   # Release preparation
hotfix/*    # Emergency production fixes
```

#### GitHub Flow (Simpler — Most Teams Use This)

```
1. Branch from main
2. Make changes and commit
3. Open a pull request
4. Get code review
5. Merge to main
6. Delete branch
```

### 🛡️ Safety First

```bash
# Always check before doing anything destructive
git status
git log --oneline -5

# Do a dry run before cleaning
git clean --dry-run

# Backup important branches before risky operations
git branch backup-main main

# Always prefer --force-with-lease over --force
git push --force-with-lease origin main
```

### .gitignore Common Patterns

```gitignore
# Logs and temp files
*.log
*.tmp

# Environment files (never commit secrets!)
.env
.env.local
.env.production

# OS files
.DS_Store
Thumbs.db

# Dependencies
node_modules/
vendor/

# Build output
dist/
build/
*.class
*.o

# IDEs
.idea/
.vscode/
*.swp

# Ignore everything except specific files
*
!.gitignore
!src/
!src/**

# Keep empty directories tracked
logs/.gitkeep
```

### 🔍 Git Hooks (Automation)

```bash
# Hooks live in .git/hooks/

# Example: pre-commit hook (runs before every commit)
#!/bin/sh
npm test
if [ $? -ne 0 ]; then
    echo "❌ Tests failed! Commit aborted."
    exit 1
fi
echo "✅ Tests passed. Committing..."

# Make hook executable
chmod +x .git/hooks/pre-commit
```

---

## 🎉 Congratulations!

You've explored the complete Git universe! 🌟 From `git init` to emergency recovery, you now have the tools to handle any Git situation confidently.

### 📖 Quick Reference Card

| Task | Command |
|---|---|
| Check status | `git status` |
| Stage all changes | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push` |
| Pull updates | `git pull` |
| Create & switch branch | `git checkout -b feature/name` |
| Merge a branch | `git merge feature/name` |
| Delete branch | `git branch -d feature/name` |
| Stash work | `git stash` |
| Restore stash | `git stash pop` |
| Undo last commit (keep files) | `git reset --soft HEAD~1` |
| Undo last commit (lose files) | `git reset --hard HEAD~1` |
| Safe undo (public repos) | `git revert HEAD` |
| Find lost commits | `git reflog` |
| See who changed a line | `git blame filename` |
| Visual commit graph | `git log --oneline --graph --all` |

### 🌟 The Golden Rules

1. **Commit early, commit often** 📝
2. **Write descriptive commit messages** 💬
3. **Always pull before push** ⬇️⬆️
4. **Use branches for every feature** 🌿
5. **Test before you commit** ✅
6. **Never force push to shared branches** 🛡️
7. **Use `--force-with-lease` instead of `--force`** ⚠️
8. **When in doubt, `git reflog` can save you** 🚨

---

**Happy Git-ing! May your merges be conflict-free and your commits be meaningful! 🚀✨**

> *"With great Git power comes great Git responsibility!"* — Uncle Git 🕷️

---

## 📚 Learn More

- [Official Git Documentation](https://git-scm.com/doc)
- [Pro Git Book (Free)](https://git-scm.com/book)
- [Interactive Git Learning](https://learngitbranching.js.org/)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Conventional Commits Spec](https://www.conventionalcommits.org/)

---

⭐ **This file is a living document. Happy coding!** 🎉

*Made with ❤️ for developers who want to Git things done right!*
