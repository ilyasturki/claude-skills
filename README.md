# Claude Code Skills

Custom skills for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Most skills are also compatible with other coding agents like [Codex](https://github.com/openai/codex) and [OpenCode](https://github.com/opencode-ai/opencode).

## Skills

| Skill | Description | Claude Code | Other Agents |
|---|---|---|---|
| `/clarify` | Look first via tools, then ask grouped clarifying questions in one round and confirm intent before implementing. | Yes | Yes |
| `/interrogate` | Exhaustive clarification — confirms every assumption, asks every question. For high-stakes or ambiguous tasks. | Yes | Yes |
| `/discuss` | Collaborative discussion — critiques, proposes approaches with trade-offs, lets you pick before implementing. | Yes | Partial |
| `/spec` | Greenfield product spec for an empty repo — clarifies scope, then challenges the idea (checks prior art, verifies the pain is real, surfaces scope risks), then writes a concise `spec.md`. | Yes | Yes |
| `/commit` | Auto-stage and commit with a conventional commit message. | Yes | Yes |
| `/commit-push` | Auto-stage and commit with a conventional commit message, then push. | Yes | Yes |
| `/commit-multiple` | Split working tree changes into multiple commits, one per logical concern. | Yes | Yes |
| `/commit-multiple-push` | Split working tree changes into multiple commits, one per logical concern, then push. | Yes | Yes |
| `/security-full` | Comprehensive security review of the entire repository. | Yes | Yes |
| `/ncu` | Bump deps via `npm-check-updates`: auto-apply and verify safe upgrades, then enter plan mode for major-bump packages with their migration steps grounded in actual usage. | Yes | Partial |
| `/readme` | Write or refresh a README that earns the reader's attention — classifies the project, auto-generates a visual (vhs gif, screenshot, or sample output), keeps prose short and honest. | Yes | Partial |
| `/verify` | Test a recent change end-to-end with the right harness (bash, browser, or computer use), then run `/simplify` to clean up the changed code before wrapping up. | Yes | Partial |

> **Note:** Skills that use Claude Code-specific features like `allowed-tools`, `disable-model-invocation`, or `AskUserQuestion` may need adaptation for other agents. The core prompt logic works anywhere.

## Installation

### Claude Code

Copy the skill folders into your Claude Code skills directory:

```bash
git clone https://github.com/ilyasturki/claude-skills.git
cp -r claude-skills/*/ ~/.claude/skills/
```

Or clone directly:

```bash
git clone https://github.com/ilyasturki/claude-skills.git ~/.claude/skills
```

### Other Agents

Copy the `SKILL.md` content into your agent's system prompt or custom instructions. The prompt content between the `---` frontmatter blocks is agent-agnostic.

## Usage

In Claude Code, type `/<skill-name>` to invoke a skill:

```
/clarify Build a REST API for user management
/discuss Should we use SQLite or PostgreSQL for this project?
/commit
/security-full
```
