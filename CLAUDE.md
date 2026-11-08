# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

The repo's purpose, layout, file conventions, and workflow are documented in `context/Project-Overview.md`, imported below. Update that file, not this one, when they change.

@context/Project-Overview.md

## Working in this repo

- Use `git mv` to rename or move tracked files and folders, so git records them as renames.
- Skill definitions are in `.claude/skills/<name>/SKILL.md`, and their usage guide is `.claude/skills/README.md`. `/push-commit-pr` has `disable-model-invocation: true`, so run it only when the user types it.
