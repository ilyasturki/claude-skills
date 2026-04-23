---
name: verify
description: After a code change, test it end-to-end (bash, browser, or computer use — whichever fits) and then run `/simplify` to review and clean up the changed code. Use to confirm a change works and is tidy before wrapping up.
argument-hint: [optional: what to focus on]
---

## User's Prompt

$ARGUMENTS

## Your Task

Verify a recent code change works end-to-end, then simplify it.

1. **Identify the change**: use `git diff` (or the conversation context) to determine what was modified.
2. **Pick the right test harness** based on what changed — do NOT rely solely on unit tests or type checks, those verify code correctness, not feature correctness:
   - **Bash** for CLI tools, scripts, libraries, backends, APIs — actually run the command, hit the endpoint, execute the script.
   - **Browser** (via `mcp__claude-in-chrome__*` tools) for web UI changes — navigate, click, fill forms, watch console, verify the UI responds correctly.
3. **Test the golden path AND edge cases**: trigger the main flow, then try obvious edge cases. Monitor for regressions in adjacent features.
4. **Report findings honestly**: state what you tested, what passed, what failed. If something can't be tested in this environment (no browser, no test data, no running service), say so explicitly rather than claiming success.
5. **Run `/simplify`**: once verification passes, invoke the `simplify` skill via the `Skill` tool to review the changed code for reuse, quality, and efficiency issues, and fix anything it finds.

## Rules

- If verification fails, fix the regression before running `/simplify`. Don't simplify broken code.
- If you can't test something, say so — never fabricate a test result.
- Keep test scope proportional to the change: a one-line typo fix doesn't need a full browser session.
