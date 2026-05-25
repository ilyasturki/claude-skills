---
name: commit-multiple-push
description: Create multiple git commits, one per concern, from changes in the working tree, then push them
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(git push:*), Bash(git reset HEAD:*), Bash(git diff:*), Bash(if git diff --staged --quiet; then git diff; else git diff --staged; fi)
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

Group all working-tree changes (staged and unstaged) by logical concern — application, feature, or purpose. Each group becomes one commit.

Steps:
1. Review the full diff to identify distinct concerns
2. `git reset HEAD` to unstage (only if anything is staged)
3. For each group, sequentially:
   a. `git add` the files (or hunks) for that group
   b. `git commit -m "message"` — single-line, no heredocs or `$()`
4. Run `git status` to confirm the tree is clean
5. Push all commits:
   - Run `git push`.
   - If push fails because the branch has no upstream, run `git push -u origin <current-branch>`.

If a single file contains hunks for truly distinct concerns (e.g. different commit types or scopes), split them across commits; otherwise keep the whole file in its most relevant commit.
