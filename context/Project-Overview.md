# Project Overview

## What this repo is

A content repository for news articles, not a software project. There is no build, lint, or test tooling.

- Remote: `https://github.com/kalyani-bellamkonda/news-articles.git`
- Default branch: `main`. Changes go in through `feature/*` branches and pull requests.

## Layout

Articles are grouped by **series**. Each series is a top-level folder, and each article in it is a subfolder named for its publish date as `DD-MON-ARTICLE/`.

```
<SERIES>/
  <DD-MON>-ARTICLE/
```

Current series:

| Series folder | Articles |
|---|---|
| `AGENT-IN-CHARGE/` | `18-OCT-ARTICLE/`: *When AI Agents Start Talking to Each Other* |
| `JUST-ADD-MCP/` | `21-OCT-ARTICLE/`: Part 1, *Just Add MCP: The Decision in Front of Leaders*<br>`01-NOV-ARTICLE/`: Part 2, *Would Your API Survive an Agent at 3am*<br>`08-NOV-ARTICLE/`: Part 3, *Nine Groups, One Paved Road* |

Supporting folders:

- `context/`: project documentation, including this file.
- `.claude/skills/`: Claude Code skills for the git workflow (see [Workflow](#workflow)).

## What an article folder holds

The two series use different file conventions.

### `AGENT-IN-CHARGE/` style

- The article as `<Title-In-Kebab-Case>.docx`, plus an exported `.pdf` with the same name, in the article folder.
- `Article Preview.docx`: a short preview or teaser of the article.
- The PNG images embedded in the article, named by role: `cover-*.png`, `figure-*.png`, `table-*.png`, `checklist-<n>-*.png`.

### `JUST-ADD-MCP/` style

- The article as `Part<N>_LinkedIn_Article.docx`.
- `Part<N>_Article_Images.zip`: all of the article's images. Parts 2 and 3 also keep the unzipped `Part<N>_Article_Images/` folder, numbered in reading order (`00_in_this_part.png`, `01_series.png`, ...).
- `Part<N>_Cover_1920x1080.png`: the cover image.
- The exported PDFs for every part are kept together in `JUST-ADD-MCP/PDF-ARTICLES/`, named `Part<N>_<Title_In_Snake_Case>.pdf`.

## Conventions

- **One current version of each file.** Delete older drafts rather than keeping `(1)`, `(2)` copies. The same goes for duplicate folders.
- **Folder names** use `DD-MON-ARTICLE` with a two-digit day and an uppercase month, e.g. `08-NOV-ARTICLE`.
- **Ignored files:** `.gitignore` excludes `.DS_Store` (macOS Finder metadata) and Office lock files (`~$*`), which appear while a document is open in Word.

## Workflow

Two Claude Code skills handle git:

- `/start-my-day`: pull the latest from the remote.
- `/push-commit-pr`: commit to a `feature/*` branch, merge `origin/main`, push, and open a PR.

Usage, prerequisites, and a typical day are in [`.claude/skills/README.md`](../.claude/skills/README.md).
