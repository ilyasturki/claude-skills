---
name: security
description: Run a security review on changed or specified files, checking for vulnerabilities.
argument-hint: [file, directory, or blank for changed files]
---

Perform a thorough security review of the relevant code. Identify real vulnerabilities, not hypothetical or stylistic concerns.

$ARGUMENTS

## Output Format

For each finding:

```
### [SEVERITY] Title

- **File:** path/to/file:line
- **Category:** e.g. injection, auth, data exposure, etc.
- **Issue:** what's wrong and why it's exploitable or dangerous
- **Fix:** concrete remediation (code snippet if short, otherwise description)
```

Severity levels: **CRITICAL**, **HIGH**, **MEDIUM**, **LOW**, **INFO**

## Rules

- Only report real, actionable security issues.
- Do not report style issues, missing docs, or non-security code quality problems.
- If a finding depends on context you can't determine, note the assumption.
- At the end, provide a one-line summary: total findings by severity.
- If no issues are found, say so clearly.
