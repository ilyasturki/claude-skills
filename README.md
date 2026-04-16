# Claude Code Skills

Custom skills for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Skills

| Skill | Description |
|---|---|
| `/clarify` | Ask up to 4 clarifying questions per round before acting. Resolves ambiguity without jumping into implementation. |
| `/interrogate` | Exhaustive clarification — confirms every assumption, asks every question. For high-stakes or ambiguous tasks. |
| `/discuss` | Collaborative discussion — critiques, proposes approaches with trade-offs, lets you pick before implementing. |
| `/commit` | Auto-stage and commit with a conventional commit message. |
| `/commit-manual` | Commit already-staged changes with a conventional commit message. |
| `/commit-multiple` | Split working tree changes into multiple commits, one per logical concern. |
| `/security` | Security review on changed or specified files. |
| `/security-full` | Comprehensive security review of the entire repository. |
| `/issue-summary` | Generate a focused prompt explaining the current issue for LLM assistance. |

## Installation

Copy the skill folders into your Claude Code skills directory:

```bash
# Clone the repo
git clone https://github.com/ilyasturki/claude-skills.git

# Copy all skills to your Claude Code config
cp -r claude-skills/*/ ~/.claude/skills/
```

Or clone directly into your skills directory:

```bash
git clone https://github.com/ilyasturki/claude-skills.git ~/.claude/skills
```

## Usage

In Claude Code, type `/<skill-name>` to invoke a skill. For example:

```
/clarify Build a REST API for user management
/discuss Should we use SQLite or PostgreSQL for this project?
/commit
/security src/auth/
```
