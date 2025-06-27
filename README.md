# 🔰 git-commands-reference 🔰
It is a helpful manual for navigating git world, this repo is a compilation of the most common git commands with clear explanations. This guide will help us as reminder refresher or if you are new to version control. Cheers to coding!  🚀

---

## Table of Contents

1. [Getting Started](#getting-started)  
2. [Configuration](#configuration)  
3. [Initialise a Repository](#initialise-a-repository)  
4. [Basic Workflow](#basic-workflow)  
5. [Branches](#branches)  
6. [Merging & Rebasing](#merging--rebasing)  
7. [Remote Repositories](#remote-repositories)  
8. [Tips & Troubleshooting](#tips--troubleshooting)  

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

### 🔗 Managing Multiple Remotes
```bash
# Add multiple remotes
git remote add upstream https://github.com/original/repo.git
git remote add fork https://github.com/yourusername/repo.git

# List all remotes
git remote -v

# Remove remote
git remote remove upstream
```

## 6. Branching 🌳

## 7. Merging & Advanced Options 🤝

## 8. Tips & Troubleshooting 🛠️

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
