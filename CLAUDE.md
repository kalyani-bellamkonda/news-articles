# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A content repository for news articles, not a software project. There is no build, lint, or test tooling. Remote: `https://github.com/kalyani-bellamkonda/news-articles.git`, default branch `main`.

## Layout

Each article lives in its own top-level folder named for its date, e.g. `OCT-18-ARTICLE/`. A folder holds:

- The article itself as `<Title-In-Kebab-Case>.docx` plus an exported `.pdf` of the same name. Keep exactly one current version of each; older drafts are deleted rather than kept as `(1)`, `(2)` copies.
- `Article Preview.docx`, a short preview/teaser of the article.
- The PNG images embedded in the article, named by role: `cover-*.png`, `figure-*.png`, `table-*.png`, `checklist-<n>-*.png`.

`.gitignore` excludes `.DS_Store` and Office lock files (`~$*`), which appear while a document is open in Word.

## Custom commands

- `/start-my-day` (`.claude/commands/start-my-day.md`): fetches and fast-forward pulls from the remote; stops instead of merging if the branch has diverged or local changes conflict.
- `/push-commit-pr` (`.claude/commands/push-commit-pr.md`): commits uncommitted work to a `feature/*` branch (creating one if on `main`), merges latest `origin/main`, and opens a PR to `main` with `gh`. If the merge conflicts, it stops before pushing and asks the user to resolve the conflicts.
