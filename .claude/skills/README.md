# Skills

Project skills for this repo. Claude Code loads them automatically when you open a session in the repo. Each skill is a folder with a `SKILL.md` file.

| Skill | What it does | How it runs |
|---|---|---|
| `/start-my-day` | Pulls the latest changes from the remote | Type it, or ask Claude to sync |
| `/push-commit-pr` | Commits your work, pushes it, and opens a PR to `main` | Only when you type it |

## Prerequisites

- `git`, with access to the remote (`origin`).
- The GitHub CLI (`gh`), signed in, for `/push-commit-pr`. Check with `gh auth status`; if you're not signed in, run `! gh auth login` in Claude Code.

## `/start-my-day`

Run it at the start of a work session to bring your local branch up to date.

```
/start-my-day
```

You can also just ask, for example "pull the latest" or "sync with the remote", and Claude will run it.

What it does:

1. Shows the current branch and any uncommitted changes.
2. Fetches from the remote.
3. Fast-forward pulls (`git pull --ff-only`).
4. Lists the commits that came in, or says you were already up to date.

It never merges or rebases on its own. It stops and explains if:

- your uncommitted changes would conflict with the incoming ones (it lists the files), or
- your branch has diverged from the remote.

## `/push-commit-pr`

Run it when an article or change is ready for review.

```
/push-commit-pr
/push-commit-pr feature/add-15-nov-article
/push-commit-pr add the 15 Nov article
```

The argument is optional. Pass a branch name, or a short description that Claude turns into a `feature/...` branch name. With no argument, Claude picks a name from the changes.

What it does:

1. Lists the changed and new files. It skips anything that looks like a secret or junk and tells you about it.
2. If you're on `main`, it creates a `feature/*` branch. Otherwise it uses your current branch.
3. Commits the changes.
4. Merges the latest `origin/main` into the branch.
5. Pushes the branch and opens a PR to `main`. If the branch already has an open PR, it adds the commits to that PR instead.
6. Reports the branch, the commits, and the PR link.

**If the merge conflicts**, it stops before pushing and lists the conflicting files. Resolve them, then run `/push-commit-pr` again. It leaves the merge in progress for you and doesn't pick sides.

Because this skill pushes and opens PRs, it has `disable-model-invocation: true` in its frontmatter. Claude never runs it unless you type the command.

## Typical day

1. `/start-my-day` to get the latest.
2. Add or edit articles (see the layout in the root `CLAUDE.md`).
3. `/push-commit-pr` to open a PR.
4. Merge the PR on GitHub, switch back with `git switch main`, then run `/start-my-day` to pull the merge.

## Adding or changing a skill

- Create `.claude/skills/<skill-name>/SKILL.md`. The folder name becomes the `/` command.
- Start the file with YAML frontmatter:

  ```yaml
  ---
  name: skill-name
  description: What it does and when Claude should use it.
  allowed-tools: Bash(git status:*)        # optional: tools it can use without asking
  argument-hint: [optional argument]       # optional: shown in the / menu
  disable-model-invocation: true           # optional: only run when typed
  ---
  ```

- Write the steps in Markdown below the frontmatter. `$ARGUMENTS` is replaced with whatever you type after the command.
- Restart Claude Code if a new or edited skill doesn't show up in the `/` menu.
