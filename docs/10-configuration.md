# 10. Configuration & Customization ⚙️

[← Back to Home](../README.md)

---

## Essential First-Time Setup

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

---

## Viewing Configuration

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

---

## Line Endings (Cross-Platform Fix)

```bash
# Windows: auto-convert line endings
git config --global core.autocrlf true

# Mac/Linux: don't convert
git config --global core.autocrlf input

# Fix long file path issues on Windows
git config --system core.longpaths true
```

---

## Git Aliases (Create Shortcuts!)

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

# Fancy log alias (visual graph)
git config --global alias.lg "log --oneline --graph --all --decorate"
```

---

## Useful Global Config Settings

```bash
# Speed up large repositories
git config --global core.preloadindex true
git config --global core.fscache true

# Auto-setup remote tracking when pushing new branches
git config --global push.autoSetupRemote true

# Use 'main' as default branch for new repos
git config --global init.defaultBranch main

# Always use rebase instead of merge on pull (cleaner history)
git config --global pull.rebase true
```

---

## .gitignore Common Patterns

```gitignore
# Logs and temp files
*.log
*.tmp

# Environment files (NEVER commit secrets!)
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

# Track empty directories
logs/.gitkeep
```

---

## Next Steps
- ➡️ [Emergency Git Commands](./11-emergency.md)
