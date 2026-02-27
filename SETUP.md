# Setup Guide: Connecting from Termux (Android) & Managing Collaborators

This guide covers how to connect your Android phone (via Termux) to your GitHub repositories, and how to add collaborators as admins with appropriate permissions.

---

## 1. Setting Up Termux on Android

Install Termux from [F-Droid](https://f-droid.org/en/packages/com.termux/) (recommended over the Play Store version).

Once installed, update packages:

```bash
pkg update && pkg upgrade
pkg install git openssh
```

---

## 2. Generating an SSH Key in Termux

Run the following in Termux to generate an SSH key pair:

```bash
ssh-keygen -t ed25519 -C "your_github_email@example.com"
```

- Press **Enter** to accept the default file location (`~/.ssh/id_ed25519`).
- Set a passphrase when prompted (recommended), or press **Enter** to skip.

Display your public key so you can add it to GitHub:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copy the entire output.

---

## 3. Adding Your SSH Key to GitHub

1. Go to [https://github.com/settings/keys](https://github.com/settings/keys)
2. Click **New SSH key**
3. Give it a title like `Termux - My Phone`
4. Paste your public key into the **Key** field
5. Click **Add SSH key**

Test the connection from Termux:

```bash
ssh -T git@github.com
```

You should see: `Hi <your-username>! You've successfully authenticated...`

---

## 4. Cloning Your Repositories from Termux

Replace `YOUR_USERNAME` and `REPO_NAME` with your actual GitHub username and repository name:

```bash
# Clone a repo using SSH
git clone git@github.com:YOUR_USERNAME/REPO_NAME.git
```

Repeat this command for each repository you want to clone. Once cloned, you can work in each repo normally with `git pull`, `git push`, etc.

---

## 5. Configuring Git Identity in Termux

Set your name and email so commits are attributed correctly:

```bash
git config --global user.name "Your Name"
git config --global user.email "your_github_email@example.com"
```

---

## 6. Adding Collaborators as Admins

GitHub manages repository access through collaborator permissions — there are no per-user passwords on repos. Access is controlled via SSH keys or Personal Access Tokens (PATs).

### To add a collaborator with Admin access (via GitHub web):

1. Go to your repository on GitHub
2. Click **Settings** → **Collaborators and teams** (or **Access**)
3. Click **Add people**
4. Enter the collaborator's GitHub username
5. Select the **Admin** role
6. Click **Add `<username>` to this repository**

The collaborator will receive an email invitation to accept.

Repeat for each repository and for each person you want to add.

### Permission levels:

| Role | What they can do |
|------|-----------------|
| Read | View and clone the repository |
| Triage | Read + manage issues/PRs |
| Write | Triage + push to branches |
| Maintain | Write + manage repo settings (no destructive actions) |
| **Admin** | Full access including settings, collaborators, deletion |

---

## 7. Using a Personal Access Token (PAT) Instead of SSH

If you prefer HTTPS over SSH in Termux:

1. Go to [https://github.com/settings/tokens](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Select scopes: `repo` (full control of private repos)
4. Copy the token — you won't see it again

In Termux, clone with HTTPS and use your token as the password:

```bash
git clone https://github.com/YOUR_USERNAME/REPO_NAME.git
# When prompted:
# Username: your GitHub username
# Password: paste your PAT here
```

To avoid re-entering credentials each time:

```bash
git config --global credential.helper store
```

---

## 8. Keeping Termux Connected to GitHub Codespaces

Your Codespace runs in the cloud — Termux on your phone connects to GitHub (not directly to the Codespace). To work with Codespaces from your phone, you can use the [GitHub mobile app](https://github.com/mobile) or a browser-based terminal.

For direct shell access to a running Codespace, use the GitHub CLI:

```bash
# In Termux, install GitHub CLI
pkg install gh

# Authenticate
gh auth login

# List your codespaces
gh codespace list

# SSH into a codespace
gh codespace ssh --codespace YOUR_CODESPACE_NAME
```

---

## Quick Reference

| Task | Command |
|------|---------|
| Generate SSH key | `ssh-keygen -t ed25519 -C "email@example.com"` |
| Show public key | `cat ~/.ssh/id_ed25519.pub` |
| Test GitHub SSH | `ssh -T git@github.com` |
| Clone a repo | `git clone git@github.com:USER/REPO.git` |
| Pull latest changes | `git pull` |
| Push changes | `git push` |
| Install GitHub CLI | `pkg install gh` |
| Login with GitHub CLI | `gh auth login` |
| List codespaces | `gh codespace list` |
| SSH into codespace | `gh codespace ssh` |
