# 2. The Complete Workflow 🔄

[← Back to Home](../README.md)

---

## Real-World Scenario: Starting a New Project

### Step 1: Initialize and Connect

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

### Step 2: The Great Branch Migration (Master → Main)

```bash
# If you're on 'master' and want to switch to 'main'
git branch -M main
# This renames your current branch to 'main'

# Or create main branch if it doesn't exist
git checkout -b main
```

> 💡 **Beginner Tip:** Modern Git uses `main` as the default branch name. If you see `master`, you can rename it!

### Step 3: Your First Commit

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

### Step 4: Connect with Remote Repository

```bash
# Push and set upstream branch
git push -u origin main
# The -u flag sets main as the default tracking branch (only needed once!)
```

### Step 5: Handling an Existing Remote Repository 🤝

```bash
# If remote repository already has content, pull it first
git pull origin main

# If you get "fatal: refusing to merge unrelated histories"
git pull origin main --allow-unrelated-histories
# This merges two separate Git histories — very common when starting!
```

---

## What's Next?
- ➡️ [Mastering Branches](./03-branching.md)
- ➡️ [Partial Staging (git add -p)](./13-partial-staging.md) — advanced staging techniques
