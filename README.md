# 🔰 Git Commands Reference 🔰

> A complete, organized manual for navigating the Git world — from absolute beginner to advanced techniques. Each topic has its own focused guide. Pick what you need!

**Cheers to coding! 🚀**

---

## 📂 How This Repo is Organized

```
git-commands-reference/
├── README.md           ← You are here (start here!)
└── docs/
    ├── 01-getting-started.md
    ├── 02-complete-workflow.md
    ├── 03-branching.md
    ├── 04-merging-conflicts.md
    ├── 05-remote-repository.md
    ├── 06-undoing-fixing.md
    ├── 07-investigation.md
    ├── 08-stashing.md
    ├── 09-advanced-techniques.md
    ├── 10-configuration.md
    ├── 11-emergency.md
    ├── 12-pro-tips.md
    ├── 13-partial-staging.md   ← 🆕
    ├── 14-ssh-setup.md         ← 🆕
    └── 15-github-workflow.md   ← 🆕
```

---

## 🗺️ All Topics

### 🟢 Beginner — Start Here

| # | Topic | What You'll Learn |
|---|---|---|
| 1 | [Getting Started](./docs/01-getting-started.md) | Install Git, `git init`, how Git tracks files |
| 2 | [The Complete Workflow](./docs/02-complete-workflow.md) | Init → add → commit → push, first-time setup |
| 14 | [SSH Key Setup](./docs/14-ssh-setup.md) 🆕 | Connect to GitHub securely without passwords |

### 🔵 Intermediate — Build Your Skills

| # | Topic | What You'll Learn |
|---|---|---|
| 3 | [Mastering Branches](./docs/03-branching.md) | Create, switch, rename, delete branches |
| 4 | [Merge Strategies & Conflict Resolution](./docs/04-merging-conflicts.md) | `--no-ff`, `--squash`, resolving conflicts |
| 5 | [Remote Repository Mastery](./docs/05-remote-repository.md) | `fetch`, `pull`, `push`, managing remotes |
| 6 | [Time Travel: Undoing & Fixing](./docs/06-undoing-fixing.md) | `reset`, `revert`, `restore`, clean up mistakes |
| 7 | [Investigation & Information](./docs/07-investigation.md) | `git log`, `git diff`, `git blame`, `git show` |
| 8 | [Stashing & Temporary Storage](./docs/08-stashing.md) | Save/restore work-in-progress instantly |
| 13 | [Partial Staging (`git add -p`)](./docs/13-partial-staging.md) 🆕 | Stage only selected lines — like a pro! |

### 🔴 Advanced — Level Up

| # | Topic | What You'll Learn |
|---|---|---|
| 9 | [Advanced Git Techniques](./docs/09-advanced-techniques.md) | Rebase, cherry-pick, bisect, tags |
| 10 | [Configuration & Customization](./docs/10-configuration.md) | Aliases, global settings, `.gitignore` |
| 11 | [Emergency Git Commands](./docs/11-emergency.md) | `reflog`, recover lost commits, detached HEAD |
| 15 | [GitHub Forking Workflow](./docs/15-github-workflow.md) 🆕 | Fork, open PRs, sync with upstream |

### 📋 Reference

| # | Topic | What You'll Learn |
|---|---|---|
| 12 | [Pro Tips & Best Practices](./docs/12-pro-tips.md) | Commit conventions, workflows, safety rules |

---

## ⚡ Quick Reference Card

| Task | Command |
|---|---|
| Check status | `git status` |
| Stage all changes | `git add .` |
| Stage selectively | `git add -p` |
| Commit | `git commit -m "type: message"` |
| Push | `git push` |
| Pull updates | `git pull` |
| Create & switch branch | `git checkout -b feature/name` |
| Merge a branch | `git merge feature/name` |
| Delete branch | `git branch -d feature/name` |
| Stash work | `git stash` |
| Restore stash | `git stash pop` |
| Undo last commit (keep files) | `git reset --soft HEAD~1` |
| Safe undo (public repos) | `git revert HEAD` |
| Find lost commits | `git reflog` |
| Stage specific lines | `git add -p filename` |
| Visual commit graph | `git log --oneline --graph --all` |
| Who changed this line? | `git blame filename` |

---

## 🌟 The Golden Rules

1. **Commit early, commit often** 📝
2. **Write descriptive commit messages** 💬
3. **Always pull before push** ⬇️⬆️
4. **Use branches for every feature** 🌿
5. **Test before you commit** ✅
6. **Never force push to shared branches** 🛡️
7. **Use `--force-with-lease` instead of `--force`** ⚠️
8. **When in doubt, `git reflog` can save you** 🚨

---

## 📚 Learn More

- [Official Git Documentation](https://git-scm.com/doc)
- [Pro Git Book (Free)](https://git-scm.com/book)
- [Interactive Git Learning](https://learngitbranching.js.org/)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Conventional Commits Spec](https://www.conventionalcommits.org/)

---

**Happy Git-ing! May your merges be conflict-free and your commits be meaningful! 🚀✨**

> *"With great Git power comes great Git responsibility!"* — Uncle Git 🕷️

---

⭐ **This is a living document. Contributions welcome!**

*Made with ❤️ for developers who want to Git things done right!*
