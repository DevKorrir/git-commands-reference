# 🔰 git-commands-reference 🔰
It is a helpful manual for navigating git world, this repo is a compilation of the most common git commands with clear explanations. This guide will help us as reminder refresher or if you are new to version control. Cheers to coding!  🚀

---

## Table of Contents

- [ Starting Your Git Journey](#️-starting-your-git-journey)
- [ The Complete Workflow](#-the-complete-workflow)
- [ Mastering Branches](#-mastering-branches)
- [ Merge Strategies & Conflict Resolution](#-merge-strategies--conflict-resolution)
- [ Remote Repository Mastery](#-remote-repository-mastery)
- [ Time Travel: Undoing & Fixing](#️-time-travel-undoing--fixing)
- [ Investigation & Information](#️-investigation--information)
- [ Stashing & Temporary Storage](#-stashing--temporary-storage)
- [ Advanced Git Techniques](#-advanced-git-techniques)
- [ Configuration & Customization](#️-configuration--customization)
- [ Emergency Git Commands](#-emergency-git-commands)
- [ Pro Tips & Best Practices](#-pro-tips--best-practices)

---

## 1. Getting Started 🚦

### The Very Beginning

Make sure Git is installed on your machine:

```bash
# Check if Git is installed
git --version
# Output: git version 2.x.x
```
*First things first - make sure Git is ready to rock!*

### Creating Your First Repository
```bash
# Initialize a new repository
git init
# This Creates .git folder - the magic happens here! 
```

### Essential First Steps
```bash
# Check what's happening (always a good idea!)
git status
# Output: On branch master (or main)
#         No commits yet
#         nothing to commit
```

---


## The Complete Workflow

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
*Modern Git uses 'main' as the default branch name!*

#### Step 3: Your First Commit
```bash
# Create your first file
echo "# My Awesome Project" > README.md

# Add file to staging area
git add README.md
# Or add everything
git add .

# Make your first commit
git commit -m "Initial commit: Added README file"
```

#### Step 4: Connect with Remote Repository
```bash
# Push and set upstream branch
git push -u origin main
# This pushes your code and sets main as the default branch
```

#### Step 5: Handling Existing Remote Repository 🤝
```bash
# If remote repository already has content, pull it first
git pull origin main

# If you get "fatal: refusing to merge unrelated histories"
git pull origin main --allow-unrelated-histories
# This merges two separate Git histories - this is very common when starting!
```

---

## 🌿 Mastering Branches

### Branch Management Basics
```bash
# See all branches
git branch -a
# * main                    (current branch marked with *)
#   remotes/origin/main

# Create new branch
git branch feature/awesome-feature

# Switch to branch (old way)
git checkout feature/awesome-feature

# Switch to branch (new way - Git 2.23+)
git switch feature/awesome-feature

# Create and switch in one command
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

# Delete local branch (safe - only if merged)
git branch -d feature/completed-feature

# Force delete local branch (careful! 💀)
git branch -D feature/unwanted-feature

# Delete remote branch
git push origin --delete feature/old-feature
```

### Branch Tracking and Upstream
```bash
# Set upstream for current branch
git branch --set-upstream-to=origin/main

# Push new branch and set upstream
git push -u origin feature/my-feature

# See tracking branches
git branch -vv
```

---

## Merge Strategies & Conflict Resolution

### 🤝 Basic Merging
```bash
# Switch to target branch (usually main)
git checkout main

# Merge feature branch
git merge feature/awesome-feature 

# Delete merged branch
git branch -d feature/awesome-feature
```

### Advanced Merge Strategies

#### Accept Their Changes (Remote/Other Branch)
```bash
# When merging, automatically accept their changes for conflicts
git merge feature/other-branch -X theirs
# eg. git merge Home/animation -X theirs

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
#### No Fast-Forward Merge (Create Merge Commit)
```bash
git merge --no-ff feature/awesome-feature
# Always creates a merge commit, preserving branch history

Main: --A--B--------------------M (Merge commit)
            \                  /
Feature:     --C--D--E--F-----

# When you do git merge --no-ff feature while on Main, Git combines F's changes into Main, but instead of just moving Main's pointer to F (which would be a "fast-forward"), it creates a new commit M.

# --no-ff: Keeps all individual feature branch commits, adds a new merge commit. (Detailed, explicit merge history)

# In essence, merging a Pull Request on most hosting platforms is the remote equivalent of performing a git merge --no-ff locally.
```

#### Squash Merge (Clean History)
```bash
git merge --squash feature/many-commits
git commit -m "Add awesome feature with many commits"

# Combines all commits from feature branch into one commit

Main: --A--B------------------S (Squash commit)
            \
Feature:     --C--D--E--F-----

# Git takes all the changes introduced by C, D, E, and F and bundles them together as if they were one single change.

# It then applies that combined change to Main as a single new commit (S), which you then explicitly create with git commit.

# The individual commits C, D, E, F are not preserved in the Main branch's history; only their combined effect appears as S.

# --squash: Combines all feature branch commits into one single commit on the target branch. (Clean, simplified history)

```

### 🔧 Handling Merge Conflicts Like a Pro (When Git gets confused!)

#### When Conflicts Happen 💥
```bash
# After a failed merge, check status
git status
# Shows files with conflicts

# See conflicted files
git diff --name-only --diff-filter=U
```

#### Manual Conflict Resolution
```bash
# Open conflicted file - you'll see:
# <<<<<<< HEAD
# Your changes
# =======
# Their changes
# >>>>>>> branch-name

# After editing, mark as resolved
git add conflicted-file.txt

# Complete the merge
git commit -m " Merge feature/branch-name"
```

#### Automated Conflict Resolution
```bash
# Accept all their changes
git checkout --theirs .
git add .
git commit

# Accept all your changes
git checkout --ours .
git add .
git commit

# Use merge tool
git mergetool
```

#### Abort Merge (Emergency Exit! 🚨)
```bash
git merge --abort
# Returns to state before merge attempt
```
---

## 🌐 Remote Repository Mastery

### Managing Multiple Remotes
```bash
# Add multiple remotes
git remote add upstream https://github.com/original/repo.git
git remote add fork https://github.com/yourusername/repo.git

# List all remotes
git remote -v

# Remove remote
git remote remove upstream
```

### Changing Remote Repository (VV Important!)

#### Method 1: Change Existing Remote URL
```bash
# Change origin to point to new repository
git remote set-url origin https://github.com/new-username/new-repo.git

# Verify the change
git remote -v
# origin  https://github.com/new-username/new-repo.git (fetch)
# origin  https://github.com/new-username/new-repo.git (push)

# Test the connection
git remote show origin
```

#### Method 2: Remove and Re-add Remote
```bash
# Remove current origin
git remote remove origin

# Add new origin
git remote add origin https://github.com/new-username/new-repo.git

# Push to new remote (may need to force first time)
git push -u origin main
```

#### Method 3: Change Remote for Different Protocols
```bash
# Switch from HTTPS to SSH
git remote set-url origin git@github.com:username/repo.git

# Switch from SSH to HTTPS  
git remote set-url origin https://github.com/username/repo.git

# Verify the change
git remote -v
```

#### Common Scenarios When You Need to Change Remote

**Scenario 1: Transferred Repository Ownership**
```bash
# Repository moved from user1 to user2
git remote set-url origin https://github.com/user2/same-repo-name.git
git push -u origin main
```

**Scenario 2: Forked Repository**
```bash
# You forked someone's repo and want to point to your fork
git remote set-url origin https://github.com/yourusername/forked-repo.git

# Keep original as upstream
git remote add upstream https://github.com/original-owner/original-repo.git
```

**Scenario 3: Company Repository Migration**
```bash
# Company moved from GitHub to GitLab
git remote set-url origin https://gitlab.com/company/project.git

# Or moved to different organization
git remote set-url origin https://github.com/new-org/project.git
```

**Scenario 4: Local Repository to New Remote**
```bash
# You have local repo and want to connect to new remote
git remote add origin https://github.com/username/new-repo.git
git branch -M main
git push -u origin main
```

### Fetching and Pulling Strategies
```bash
# Fetch all branches from all remotes
git fetch --all

# Fetch specific remote
git fetch origin

# Fetch and prune deleted remote branches
git fetch --prune
# If a branch was deleted on the remote, this command cleans up your local list
# of remote branches to match. It's like throwing away old, unused address books!

# Pull with rebase (cleaner history)
git pull --rebase origin main
# no need for "merge commit"

# Pull specific branch
git pull origin feature/specific-branch
# This command downloads changes specifically from 'feature/specific-branch' on the remote
# this merges into your *current* local branch. Make sure you're on the right branch!
```

### Advanced Push Operations
```bash
# Push all branches
git push --all origin

# Push tags
git push --tags

# Force push (be very careful! ⚠️)
git push --force origin main
# this is like : : "I know what I'm doing, overwrite everything!"

# Safer force push
git push --force-with-lease origin main
# Force push, but only if no one else has touched it!. If someone else pushed changes to the remote main since you last pulled, this command will fail, protecting their work.

# Push new branch
git push -u origin feature/new-branch

# Push to different branch name
git push origin local-branch:remote-branch
# Eg: git push origin develop:staging would push your local develop branch to a remote branch named staging.
```

---

## Time Travel: Undoing & Fixing
### Working Directory Changes
```bash
# Discard changes in specific file
git checkout -- filename.txt
# The -- is important here; it tells Git that what follows are file paths, not branch names.
# or (newer syntax)
git restore filename.txt

# Discard all changes in working directory
git checkout -- .
# or                 The . means "all files in the current directory and its subdirectories." 
git restore .

# If a file was staged (you git added it but didn't git commit it), these commands will also revert it back to its state in the last commit, removing it from the staging area.
# They DO NOT affect untracked files.


# Remove untracked files
git clean -f
# Rmoves all untracked files from your current folder and it does not remove untracked folders or directories. If you have an empty folder or a folder with untracked files inside it, git clean -f will not remove the folder itself, only untracked files

# Remove untracked files and directories
git clean -fd
# -f (force)
# -d (directories)
# By default it will still respect yout .gitignore file.

# Preview what will be removed
git clean -n
# This command is a "dry run". It shows you what files and directories would be removed if you run git clean -f or git clean -fd. It doesn't actually delete anything.

# Untrack Specific file
git rm --cached <file>
# git rm --cached app/google-services.json
# Untrack a specific file that Git is currently tracking, keeping the file on your local disk. It's about changing Git's knowledge of the file, not necessarily about "cleaning up" loose items.
```

### Staging Area Operations
```bash
# Unstage specific file
git reset HEAD filename.txt
# or (newer syntax)
git restore --staged filename.txt

# Unstage all files
git reset HEAD
# or
git restore --staged .
```

### Commit History Manipulation

#### Soft Reset (Keep Changes)
```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Undo multiple commits
git reset --soft HEAD~3
```

#### Mixed Reset (Default)
```bash
# Undo last commit, keep changes in working directory
git reset HEAD~1

# Reset to specific commit
git reset abc1234
```

#### Hard Reset (Nuclear Option! 💀)
```bash
# DANGER: Permanently lose all changes
git reset --hard HEAD~1

# Reset to specific commit (lose everything after)
git reset --hard abc1234

# Reset to remote state
git reset --hard origin/main
```

#### Safe Undoing with Revert
```bash
# Create new commit that undoes changes
git revert HEAD

# Revert specific commit
git revert abc1234

# Revert merge commit
git revert -m 1 merge-commit-hash
```

---

## 🕵️ Investigation & Information












































































## 💎 Pro Tips & Best Practices

### Commit Message Magic
```bash
# Great commit message format:
# Type: Brief description (50 chars max)
# 
# More detailed explanation if needed (wrap at 72 chars)
# 
# - Use bullet points for multiple changes
# - Reference issues: Fixes #123

# Examples:
git commit -m "feat: Add user authentication system

- Implement JWT token handling
- Add login/logout endpoints  
- Create user registration flow
Fixes #42"

# Commit types with emojis:
# ✨ feat: New feature
# 🐛 fix: Bug fix
# 📚 docs: Documentation
# 🎨 style: Formatting
# ♻️ refactor: Code refactoring
# ⚡ perf: Performance improvement
# ✅ test: Adding tests
# 🔧 chore: Maintenance tasks
```

### Workflow Strategies

#### Git Flow
```bash
# Main branches
main        # Production-ready code
develop     # Integration branch

# Supporting branches
feature/    # New features
release/    # Release preparation
hotfix/     # Emergency fixes
```

#### GitHub Flow (Simpler)
```bash
# Simple workflow:
1. Create branch from main
2. Make changes and commit
3. Open pull request
4. Merge to main
5. Delete branch
```

### 🛡️ Safety First
```bash
# Always check before destructive operations
git status
git log --oneline -5

# Use --dry-run when available
git clean --dry-run

# Backup important branches
git branch backup-main main

# Use force-with-lease instead of force
git push --force-with-lease origin main
```

### 🚀 Performance Tips
```bash
# Speed up large repositories
git config --global core.preloadindex true
git config --global core.fscache true

# Partial clone for huge repos
git clone --filter=blob:none <url>

# Shallow clone for CI/CD
git clone --depth 1 <url>
```

### .gitignore Mastery
```bash
# Common patterns
*.log
*.tmp
.env
.DS_Store
node_modules/
dist/
build/

# Ignore everything except specific files
*
!.gitignore
!src/
!src/**

# Track empty directories
cache/.gitkeep
```

### 🔍 Git Hooks (Automation)
```bash
# Location: .git/hooks/

# Pre-commit hook (runs before each commit)
#!/bin/sh
npm test
if [ $? -ne 0 ]; then
    echo "Tests failed! Commit aborted."
    exit 1
fi

# Make hook executable
chmod +x .git/hooks/pre-commit
```

---

## 🎉 Congratulations!

You've mastered the complete Git universe! 🌟 From basic `git init` to complex merge strategies, you now have the power to handle any Git situation with confidence.

### 📖 Quick Reference Card
```bash
# Daily essentials
git status              # Check what's happening
git add .              # Stage changes  
git commit -m "msg"    # Save changes
git push               # Share changes
git pull               # Get updates

# Branch workflow
git checkout -b feature/name    # Create & switch branch
git push -u origin feature/name # Push new branch
git checkout main              # Switch to main
git merge feature/name         # Merge feature
git branch -d feature/name     # Clean up

# Emergency commands
git stash              # Save work temporarily
git reset --hard HEAD  # Nuclear reset
git reflog             # Find lost commits
```

### 🌟 Remember the Golden Rules:
1. **Commit early, commit often** 📝
2. **Write descriptive commit messages** 💬
3. **Always pull before push** ⬇️⬆️
4. **Use branches for features** 🌿
5. **Test before you commit** ✅
6. **Backup important work** 💾

---

**Happy Git-ing! May your merges be conflict-free and your commits be meaningful! 🚀✨**

> *"With great Git power comes great Git responsibility!"* - Uncle Git 🕷️

---

## 📚 Learn More
- [Official Git Documentation](https://git-scm.com/doc)
- [Pro Git Book (Free)](https://git-scm.com/book)
- [Interactive Git Learning](https://learngitbranching.js.org/)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)


# ⭐ This file is a living document. Happy coding! 🎉

*Made with ❤️ for developers who want to Git things done right!*
