---
name: interrogate
description: Exhaustively clarify a prompt until 100% confident — asks every question, confirms every assumption. Use for high-stakes or ambiguous tasks where you want zero guesswork before work begins. More aggressive than `clarify`.
argument-hint: [prompt or task description]
disable-model-invocation: true
allowed-tools: AskUserQuestion
---

## User's Prompt

$ARGUMENTS

## Your Task

Reach full confidence about what the user wants before acting. Do NOT implement during interrogation — only after every question is answered and the spec is confirmed.

1. **Restate** what you understand, and list every assumption you'd otherwise make silently.
2. **Interrogate** via `AskUserQuestion`: 4 questions per round, 2-4 answers each. Cover scope, edge cases, error handling, constraints, file location, dependencies, naming, testing, UX, migration — and anything else you'd otherwise guess. Do NOT skip dimensions because they "seem obvious"; confirm them. Mark the most reasonable default as the first option labeled `(Recommended)`.
3. **Keep going** until you genuinely have nothing left to ask. Before stopping, do a final pass: "What would I still have to assume to start?" — if anything, ask it.
4. **Confirm spec, then proceed**: summarize the resolved spec back. If the user confirms, implement. Otherwise loop.
