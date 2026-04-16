---
name: commit-multiple
description: Create multiple git commits, one per concern, from changes in the working tree
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(git reset HEAD:*), Bash(git diff:*), Bash(if git diff --staged --quiet; then git diff; else git diff --staged; fi)
---

## Context

- Current git status: !`git status`
- Changes to commit: !`if git diff --staged --quiet; then git diff; else git diff --staged; fi`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10 2>/dev/null || echo "No commits yet"`

## User Context

$ARGUMENTS

## Commit Name Rules

Single-line Conventional Commit:
- Format: <type>(<scope>): <description>
- Types: feat, fix, refactor, perf, docs, style, test, build, ci, chore, revert
- Description must mention the SPECIFIC thing changed (component name, function, feature, etc.)
- Include "!" after type for breaking changes
- ≤72 chars, lowercase, imperative mood, no period

## Your task

Analyze ALL changes in the working tree (both staged and unstaged) and group them by logical concern — e.g. by application, feature, or purpose. Each group becomes its own commit.

Steps:
1. Review the full diff and file list to identify distinct concerns
2. `git reset HEAD` to unstage everything (only if anything is staged)
3. For each group, execute sequentially:
   a. `git add` the specific files for that group
   b. `git commit -m "message"` — use a single-line message, NO heredocs or $() command substitution
4. After all commits, run `git status` to confirm the tree is clean

If a single file contains changes for multiple concerns, put it in the most relevant commit rather than trying to split hunks.
