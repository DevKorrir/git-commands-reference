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
















## 2. Configuration ⚙️

## 3. Initialize & Rename Default Branch 🌱

## 4. Basic Workflow 🔄

## 5. Remote Repositories ☁️

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
