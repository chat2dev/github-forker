# github-forker

A Claude Code skill that extracts GitHub repository URLs from text or images, forks them, and stars the originals — all in one step.

## Features

- Extract GitHub URLs from plain text (with or without `https://`, with sub-paths)
- Extract GitHub URLs from screenshots or images (via vision)
- Fork all found repositories via GitHub API
- Star the original repository after each successful fork
- Batch support: handles multiple repos in a single message

## Installation

Copy the skill directory to `~/.claude/skills/`:

```bash
cp -r github-forker ~/.claude/skills/github-forker
```

## Setup

Set your GitHub token (classic PAT with `repo` or `public_repo` scope):

```bash
export GITHUB_TOKEN="ghp_..."
# Add to ~/.zshrc to persist
```

## Usage

Just mention a GitHub repo and ask to fork it:

```
帮我 fork 这个：https://github.com/owner/repo
fork this: github.com/owner/repo
copy this repo to my account: https://github.com/owner/repo/tree/main/subdir
```

The skill will fork the repo and star the original automatically.
