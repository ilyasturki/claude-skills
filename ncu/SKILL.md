---
name: ncu
description: Bump dependencies via npm-check-updates. Auto-apply and verify safe upgrades; for major-bump packages enter plan mode with per-package migration steps grounded in actual usage.
disable-model-invocation: true
---

## User's Prompt

$ARGUMENTS

## Context

Working tree: !`git status --short`

Upgrades available:
!`npx -y npm-check-updates --jsonUpgraded 2>&1 | tail -100`

## Your Task

Two passes: apply + verify safe bumps, then plan + apply breaking bumps one at a time.

1. **Baseline.** Clean tree (stash if dirty). Run the verify scripts that exist in `package.json#scripts` (`build`/`typecheck`/`lint`/`test`/`format:check`). Pre-existing failures don't count later — only *new* ones do.
2. **Split** the upgrades above into:
   - **Safe** — patch/minor with major unchanged. 0.x rule: `0.y.z → 0.y.z+1` safe; `0.y.* → 0.y+1.0` breaking.
   - **Breaking** — everything else, plus peer-coupled packages where any one is breaking (e.g. `react`/`react-dom`, `@types/*` with their runtime).
   - **Skip** — pinned via `resolutions`/`overrides` or adjacent comments. Surface in the final report.
3. **Apply safe.** `npx npm-check-updates -u --target minor` (add `--filter` if the user passed one; `--deep` for workspaces). Install with the project's package manager (match ncu's `Using bun`/`pnpm`/etc.). Re-run verify; *new* failures → bisect, demote offender to breaking.
4. **Plan breaking.** If none, finish with a short report. Otherwise `EnterPlanMode`. Per package: migration notes from `mcp__plugin_context7_context7__query-docs` (fallback `WebFetch` on the release page), grep to scope to actual usage, note exact edits + cross-package ordering.
5. **Apply breaking.** Exit plan, one package at a time: bump → install → edit → verify. Don't move on until green.

## Rules

- Spell out `npm-check-updates` — `npx ncu` is a different deprecated package.
- Typecheck passing ≠ app runs; exercise tests or the dev server.
- A "safe" bump that fails verification is breaking — reclassify, don't paper over.
- Don't commit. Leave changes in the working tree.
