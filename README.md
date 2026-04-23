# Claude Code Skills

Custom skills for [Claude Code](https://docs.anthropic.com/en/docs/claude-code). Most skills are also compatible with other coding agents like [Codex](https://github.com/openai/codex) and [OpenCode](https://github.com/opencode-ai/opencode).

## Skills

| Skill | Description | Claude Code | Other Agents |
|---|---|---|---|
| `/clarify` | Ask up to 4 clarifying questions per round before acting. Resolves ambiguity without jumping into implementation. | Yes | Yes |
| `/interrogate` | Exhaustive clarification — confirms every assumption, asks every question. For high-stakes or ambiguous tasks. | Yes | Yes |
| `/discuss` | Collaborative discussion — critiques, proposes approaches with trade-offs, lets you pick before implementing. | Yes | Partial |
| `/verify` | After a code change, test it end-to-end (bash, browser, or computer use) and then run `/simplify` to clean up. | Yes | Partial |
| `/commit` | Auto-stage and commit with a conventional commit message. | Yes | Yes |
| `/commit-manual` | Commit already-staged changes with a conventional commit message. | Yes | Yes |
| `/commit-multiple` | Split working tree changes into multiple commits, one per logical concern. | Yes | Yes |
| `/security` | Security review on changed or specified files. | Yes | Yes |
| `/security-full` | Comprehensive security review of the entire repository. | Yes | Yes |
| `/issue-summary` | Generate a focused prompt explaining the current issue for LLM assistance. | Yes | Yes |

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
/security src/auth/
```
