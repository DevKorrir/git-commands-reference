# 12. Pro Tips & Best Practices 💎

[← Back to Home](../README.md)

---

## Commit Message Magic

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

---

## Conventional Commit Types

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

---

## Workflow Strategies

### Git Flow (Complex Projects)

```
main        # Production-ready code only
develop     # Integration branch — ongoing work
feature/*   # New features (branch from develop)
release/*   # Release preparation
hotfix/*    # Emergency production fixes
```

### GitHub Flow (Simpler — Most Teams Use This)

```
1. Branch from main
2. Make changes and commit
3. Open a pull request
4. Get code review
5. Merge to main
6. Delete branch
```

---

## 🛡️ Safety First

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

---

## 🔍 Git Hooks (Automation)

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

## The Golden Rules 🌟

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
