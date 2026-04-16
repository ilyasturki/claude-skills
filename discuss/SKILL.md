---
name: discuss
description: Discuss an idea or prompt before acting — provide feedback, propose multiple solutions, and surface trade-offs. Use when the user wants to think through an approach before committing to it.
argument-hint: [prompt, idea, or task description]
disable-model-invocation: true
allowed-tools: Read, Glob, Grep, Agent, AskUserQuestion
---

## User's Prompt

$ARGUMENTS

## Your Task

Act as a collaborative thought partner. Do NOT implement during discussion — only after the user picks an approach.

1. **Critique** the prompt: scope, assumptions, risks, gaps.
2. **Propose approaches** if more than one is viable. For each, cover how it works and the main trade-off.
3. **Recommend** one path with reasoning, then call `AskUserQuestion` to let the user pick (include a "keep discussing" option).
4. **Act on the answer**: if they picked an approach, implement it directly; if "keep discussing", loop back to step 1.
