---
description: Commit uncommitted changes to a feature branch, sync with main, and open a PR
argument-hint: [optional branch name or short description of the change]
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git branch:*), Bash(git switch:*), Bash(git checkout:*), Bash(git fetch:*), Bash(git add:*), Bash(git commit:*), Bash(git merge:*), Bash(git push:*), Bash(git log:*), Bash(git ls-files:*), Bash(gh pr:*)
---

Commit what is uncommitted in this repo to a feature branch, bring it up to date with `main`, and open a pull request into `main`. Extra input from me, if any: $ARGUMENTS

1. **Check what is uncommitted.** Run `git status` and `git diff --stat` (plus `git diff --cached --stat`). Show me a short list of the changed and new files. If there is nothing to commit and the current branch has no commits ahead of `origin/main`, say so and stop.
   - Don't stage files that look like secrets (`.env`, keys, credentials) or junk the `.gitignore` should cover; point them out instead.

2. **Get onto a feature branch.**
   - If the current branch is not `main`, use it as the feature branch.
   - If on `main`, create a new branch with `git switch -c <name>`. Use the name from my input if I gave one; otherwise make a short kebab-case name from the changes, prefixed with `feature/` (for example `feature/add-oct-25-article`). Uncommitted changes carry over to the new branch.

3. **Commit.** Stage the relevant files and commit with a clear message that describes the change.

4. **Get the latest from main.** Run `git fetch origin`, then `git merge origin/main` into the feature branch.

5. **Check for conflicts.**
   - If the merge reports conflicts, **stop**. Do not push, and do not open a PR. Alert me clearly with a list of the conflicting files (`git diff --name-only --diff-filter=U`) and tell me to resolve them, then run this command again. Leave the merge in progress so I can resolve it; don't abort it or pick sides myself.
   - If the merge is clean, continue.

6. **Push.** Run `git push -u origin <branch>`.

7. **Raise the PR.**
   - If an open PR already exists for this branch (`gh pr view`), don't create another; tell me the new commits were added to it and give me its link.
   - Otherwise run `gh pr create --base main --head <branch>` with a title and a short body summarizing the changes. End the body with:
     🤖 Generated with [Claude Code](https://claude.com/claude-code)

8. **Report back:** the branch name, the commit(s) included, and the PR link.
