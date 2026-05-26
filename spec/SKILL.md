---
name: spec
argument-hint: [idea description]
description: Greenfield product spec for an empty repo. Clarifies scope, then challenges the idea — checking whether it already exists and whether the pain is real — before writing a concise spec.md.
---

## User's Prompt

$ARGUMENTS

## Context

- Tree: !`ls -A 2>/dev/null | head -20`
- Existing spec: !`test -f spec.md && wc -l spec.md || echo "no spec.md"`

## Your Task

Help the user decide *whether* and *what* to build, then write a concise `spec.md`. No code, no implementation. Order matters: **clarify → challenge → write**. Do not push back before you understand.

1. **Restate** the idea in one sentence: *what*, *for whom*, *why it matters*.

2. **Clarify** in one round via `AskUserQuestion` — up to 4 grouped questions covering whatever's genuinely undecided: target user, the specific pain being solved, non-goals, success criteria, must-have vs nice-to-have, constraints (time, budget, stack). Skip dimensions already clear from the prompt. Your job here is to *understand*, not to challenge — questions only, no pushback yet.

3. **Challenge** — now that scope is clear, stress-test the idea. Be honest, not polite. Use `WebSearch` and `WebFetch` where it helps:
   - **Does it already exist?** Find 2–5 competing or adjacent products. One line each: what they do, where they fall short. If a competitor already nails it, name what genuinely differentiates the user's version — or admit there isn't a differentiator.
   - **Is the pain real?** Look for evidence — Reddit threads, HN comments, GitHub issues, blog posts complaining about the gap. If you can't find any, that's itself a finding: the pain is thin.
   - **Scope risks**: is this two products glued together? Is the MVP actually doable solo?
   - **Hidden conflicts** in goals or constraints.
   - Time-box the searches to ~3–5 queries — sanity check, not a market report.

4. **Write** `./spec.md`. Cap at ~100 lines.

## What every spec must answer

Each spec gets a different shape — do NOT force one layout on all. Pick section names and order that fit the app (a B2B SaaS spec frames differently than a CLI utility or a consumer app). But the doc must address, somewhere:

- **What it is** — one sentence, concrete, no marketing.
- **Who specifically** — not "developers", but "developers running TUIs they want to demo on GitHub".
- **The pain, with evidence** — link a thread, quote a complaint from the investigation. No hand-wavy claims.
- **Prior art** — 2–5 entries with one-line takeaways and where they fall short. If nothing exists, ask why.
- **Scope of v1** — the smallest thing that's still useful.
- **What it explicitly is NOT** — non-goals matter as much as scope.

## Rules

- Product spec, not engineering. No code, no stack choices, no file layout.
- The order is **clarify → challenge → write**. Don't challenge before you understand. The prior-art check inside Challenge is not optional.
- A spec without evidence the pain is real is just a wish. The pain section — whatever you call it — must cite something concrete.
- If prior art already solves this, name the differentiator. If there isn't one, the spec should say so plainly — even if it means "reconsider".
- Concrete over abstract: *"Tracks tasks in a TUI with vim keybindings"* beats *"A productivity tool"*.
- Cap at ~100 lines. If it needs more, the scope is wrong — narrow it.
- Don't commit. Leave changes in the working tree.
