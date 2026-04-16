---
name: commit-manual
description: Create a git commit
allowed-tools: Bash(if git diff --staged --quiet; then git diff; else git diff --staged; fi), Bash(git status:*)
disable-model-invocation: true
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

Based on the above changes, and output rules, create a single git commit on a single line.
Use `git commit -m "message"` directly. Do NOT use heredocs or $() command substitution.
