# github-forker

A Claude Code skill that extracts GitHub repository URLs from text or images, forks them, and stars the originals — all in one step.

## Features

- Extract GitHub URLs from plain text (with or without `https://`, with sub-paths)
- Extract GitHub URLs from screenshots or images (via vision)
- Resolve truncated URLs (e.g. `github.com/owner/re...`) using GitHub search + context inference
- Fork all found repositories via GitHub API
- Star the original repository after each successful fork
- Batch support: handles multiple repos in a single message

## Installation

Copy the skill directory to `~/.claude/skills/`:

```bash
cp -r github-forker ~/.claude/skills/github-forker
```

## Setup

### 1. Install Git

**macOS**
```bash
brew install git
```

**Ubuntu / Debian**
```bash
sudo apt update && sudo apt install git -y
```

**Windows**

Download and install from https://git-scm.com/download/win

### 2. Configure SSH Key (passwordless access)

Generate an SSH key and add it to GitHub so you never need to enter a password:

```bash
# Generate key (use your GitHub email)
ssh-keygen -t ed25519 -C "your@email.com"
# Press Enter to accept default path (~/.ssh/id_ed25519), set passphrase if desired

# Add key to ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard
# macOS
cat ~/.ssh/id_ed25519.pub | pbcopy
# Linux
cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard
```

Then go to **GitHub → Settings → SSH and GPG keys → New SSH key**, paste and save.

Verify it works:
```bash
ssh -T git@github.com
# Hi username! You've successfully authenticated...
```

### 3. Set GitHub Token

The skill uses the GitHub REST API to fork and star repos, which requires a Personal Access Token (classic PAT with `repo` or `public_repo` scope).

```bash
# Set for current session
export GITHUB_TOKEN="ghp_..."

# Persist across sessions (add to shell config)
echo 'export GITHUB_TOKEN="ghp_..."' >> ~/.zshrc   # zsh
echo 'export GITHUB_TOKEN="ghp_..."' >> ~/.bashrc  # bash
```

Generate a token at: **GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)**

## Usage

Just mention a GitHub repo and ask to fork it:

```
帮我 fork 这个：https://github.com/owner/repo
fork this: github.com/owner/repo
copy this repo to my account: https://github.com/owner/repo/tree/main/subdir
```

Works with truncated URLs from screenshots too:

```
fork git [image with github.com/owner/re...]
```

The skill will infer the full repo from context, fork it, and star the original automatically.
