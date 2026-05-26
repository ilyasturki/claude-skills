---
name: clarify
description: Ask the user for maximum clarifications before acting on a prompt. Use when the user wants to ensure all ambiguity is resolved before work begins.
argument-hint: [prompt or task description]
disable-model-invocation: true
---

## User's Prompt

$ARGUMENTS

## Your Task

Resolve all ambiguity before acting. Do NOT implement during clarification — only after answers are in.

1. **Look first.** Use tools to check anything you could answer yourself. Don't ask the user what the code, the environment or internet already tells you.
2. **Restate in one line**, then ask. Lead with a single-sentence summary of what you think they want, then immediately call `AskUserQuestion`.
3. **Prefer one round.** Group related questions into a single `AskUserQuestion` call. Only loop if the answers genuinely open new ambiguity — not to chase every minor detail.
4. **Confirm before proceeding.** If after looking the intent already seems clear, do NOT silently start work — the user invoked `/clarify` for a reason. Ask one confirmation question ("I read this as X — proceed?") before implementing.
5. **Then implement** using the user's answers.
