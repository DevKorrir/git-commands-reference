# 14. SSH Key Setup 🔐

[← Back to Home](../README.md)

> 💡 **Why SSH?** SSH keys let you push/pull from GitHub without typing your username and password every time. Once set up, it just works — securely and automatically.

---

## How SSH Authentication Works

```
Your Computer                      GitHub
┌─────────────────┐                ┌──────────────────┐
│  Private Key 🔑 │ ─── proves ──► │  Public Key 🔓   │
│  (~/.ssh/id_ed) │    identity    │  (in your        │
│  NEVER share!   │                │   GitHub account) │
└─────────────────┘                └──────────────────┘
```

Your **private key** stays on your machine forever. Your **public key** is uploaded to GitHub. They match together like a lock and key.

---

## Step 1: Check for Existing SSH Keys

```bash
ls -al ~/.ssh
# Look for files named:
# id_ed25519 + id_ed25519.pub  (modern, recommended)
# id_rsa + id_rsa.pub          (older, still works)
```

If you see those files, skip to Step 3. If not, generate a new key:

---

## Step 2: Generate a New SSH Key

```bash
# Generate a modern Ed25519 key (recommended)
ssh-keygen -t ed25519 -C "your_email@example.com"

# If your system doesn't support Ed25519 (unlikely), use RSA:
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

When prompted:
```
Enter file in which to save the key: [Press Enter for default]
Enter passphrase: [optional but recommended for security]
Enter same passphrase again:
```

> 💡 **Tip:** A passphrase adds extra security. You'll only need to enter it once per session if you use `ssh-agent`.

---

## Step 3: Add Your Key to the SSH Agent

The SSH agent manages your keys so you don't re-enter your passphrase constantly.

```bash
# Start the SSH agent
eval "$(ssh-agent -s)"
# Output: Agent pid 12345

# Add your key to the agent
ssh-add ~/.ssh/id_ed25519
# For RSA: ssh-add ~/.ssh/id_rsa
```

---

## Step 4: Copy Your Public Key

```bash
# Print your public key to the terminal
cat ~/.ssh/id_ed25519.pub
# Output: ssh-ed25519 AAAAC3Nza... your_email@example.com

# On Linux with xclip installed — copy to clipboard directly:
xclip -selection clipboard < ~/.ssh/id_ed25519.pub

# On macOS:
pbcopy < ~/.ssh/id_ed25519.pub
```

---

## Step 5: Add the Key to GitHub

1. Go to **GitHub.com** → Click your profile photo → **Settings**
2. Click **SSH and GPG keys** in the left sidebar
3. Click **New SSH key**
4. Give it a title (e.g. "My Laptop")
5. Paste your public key into the **Key** field
6. Click **Add SSH key**

---

## Step 6: Test the Connection

```bash
ssh -T git@github.com
# Expected output:
# Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

> ✅ If you see "successfully authenticated" — you're all set!

---

## Step 7: Use SSH URLs Instead of HTTPS

```bash
# SSH URL format (use this when cloning)
git clone git@github.com:username/repo.git

# Already have a repo using HTTPS? Switch it to SSH:
git remote set-url origin git@github.com:username/repo.git

# Verify:
git remote -v
# origin  git@github.com:username/repo.git (fetch)
# origin  git@github.com:username/repo.git (push)
```

---

## Managing Multiple SSH Keys (e.g. Work + Personal)

If you have multiple GitHub accounts, create a `~/.ssh/config` file:

```
# Personal GitHub account
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519

# Work GitHub account
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work
```

Then use the alias when cloning for work:
```bash
git clone git@github-work:workorg/repo.git
```

---

## Troubleshooting

| Problem | Fix |
|---|---|
| `Permission denied (publickey)` | Key not added to GitHub or wrong URL format |
| `ssh-add: command not found` | Install openssh-client |
| `Agent has no identities` | Run `ssh-add ~/.ssh/id_ed25519` |
| Connection timeout | Check firewall or use port 443: `ssh -T -p 443 git@ssh.github.com` |

---

## Next Steps
- ➡️ [GitHub Workflow (Forks & PRs)](./15-github-workflow.md)
