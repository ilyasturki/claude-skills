---
name: commit-push
description: Create a git commit and push it
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*), Bash(git push:*), Bash(git diff:*)
disable-model-invocation: true
---

## Context

- Current git status: !`git status`
- Staged diff: !`git diff --staged`
- Unstaged diff: !`git diff`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10 2>/dev/null || echo "No commits yet"`

## User Context

$ARGUMENTS

## Scope rules — what to commit

Pick exactly one of these scopes based on the current conversation:

1. **Conversation has context** (you have made or discussed edits earlier in this conversation):
   commit ONLY the files that were touched/discussed in this conversation.
   Do NOT include unrelated working-tree changes — leave them untouched (staged or unstaged).
   Mechanics: `git add <paths>` (needed so untracked conversation files become known), then
   `git commit -m "..." -- <paths>`. The trailing pathspec is required — it makes the commit
   ignore any unrelated entries already in the index. Never use `git add -A` / `git add .`.
   Whole-file scope is fine: if a conversation file also has unrelated local hunks, they ride along.

2. **First message, something is staged**: commit ONLY what is already staged. Do not add anything.

3. **First message, nothing staged**: commit everything in the working tree (`git add -A`).
   If the working tree is also clean (nothing to commit at all), stop and tell the user — do not make an empty commit and do not push.

If unsure whether a change belongs to the conversation, leave it out.

## Commit Name Rules

Single-line Conventional Commit:
- Format: <type>(<scope>): <description>
- Types: feat, fix, refactor, perf, docs, style, test, build, ci, chore, revert
- Description must mention the SPECIFIC thing changed (component name, function, feature, etc.)
- Include "!" after type for breaking changes
- ≤72 chars, lowercase, imperative mood, no period

## Your task

1. Determine which scope rule applies (see above).
2. Stage and commit per that rule's mechanics. Single-line commit message. Do NOT use heredocs or `$()` command substitution.
3. Push the commit:
   - Run `git push`.
   - If push fails because the branch has no upstream, run `git push -u origin <current-branch>`.
