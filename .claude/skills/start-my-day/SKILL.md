---
name: start-my-day
description: Bring this repository up to date with the remote by fetching and fast-forward pulling, then summarize the new commits. Use when the user wants to start their day, sync with or pull from the remote, or get the latest changes. Stops instead of merging if the branch has diverged or local changes would conflict.
allowed-tools: Bash(git status:*), Bash(git fetch:*), Bash(git pull:*), Bash(git log:*), Bash(git branch:*), Bash(git rev-list:*)
---

# Start my day

Bring this repository up to date with the remote.

1. Run `git status` and `git branch -vv` to see the current branch and whether there are uncommitted changes.
2. Run `git fetch --all --prune`.
3. If the working tree has uncommitted changes that would conflict with the incoming changes, stop and tell the user which files are affected instead of pulling.
4. Otherwise run `git pull --ff-only`. If a fast-forward isn't possible because the local branch has diverged, stop and explain the situation; don't merge or rebase without asking.
5. Summarize what came in: run `git log --oneline` over the range that was pulled, and list the new commits (or say it was already up to date).
