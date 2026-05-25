---
name: clarify
description: Ask the user for maximum clarifications before acting on a prompt. Use when the user wants to ensure all ambiguity is resolved before work begins.
argument-hint: [prompt or task description]
disable-model-invocation: true
allowed-tools: AskUserQuestion
---

## User's Prompt

$ARGUMENTS

## Your Task

Resolve all ambiguity before acting. Do NOT implement during clarification — only after answers are in.

1. **Restate** what you understand the user is asking for, so they can confirm or correct.
2. **Ask** via `AskUserQuestion`: Cover whatever's genuinely ambiguous, wrong and elements that you still need to clarify — skip what's already clear. Don't ask questions that you already know the answer to by using a tool or looking it up.
3. **Loop or proceed**: if answers reveal further ambiguity, run another round; once everything is clear, implement using the user's answers.

If the intent is already clear, proceed without clarification and directly implement.
