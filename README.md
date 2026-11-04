# agent-guardrail-skill: One-File Safety Skill for AI Coding Agents

[![skills-install](https://img.shields.io/badge/install%20with-skills--install-blue)](https://github.com/clements23/skills-install)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)

A single `SKILL.md` that gives any AI coding agent hard safety guardrails: confirmation before destructive commands, no force pushes, no secret leaks, no writes outside the repo, and honest test reporting.

Most agent accidents are not model failures. They are missing guardrails: a `rm -rf` nobody approved, a force push to a shared branch, a `.env` file committed "for convenience". This skill closes those holes with one file.

## Install

```bash
npx skills-install clements23/agent-guardrail-skill
```

Or manually copy `skills/agent-guardrail/` into your agent's skills directory:

| Agent | Destination |
| --- | --- |
| Claude Code | `~/.claude/skills/agent-guardrail/SKILL.md` |
| OpenAI Codex | `~/.codex/skills/agent-guardrail/SKILL.md` |
| Cursor | `~/.cursor/skills/agent-guardrail/SKILL.md` |
| Gemini CLI | `~/.gemini/skills/agent-guardrail/SKILL.md` |

For project-scoped protection, copy it to `.claude/skills/agent-guardrail/SKILL.md` inside the repository and commit it so every contributor's agent gets the same rules.

## What it blocks

1. **Destructive commands** (`rm -rf`, force push, `git reset --hard`, database drops, killing foreign processes) require explicit confirmation with the exact command shown first.
2. **Out-of-repo writes**: shell profiles, OS settings, SSH keys and credential stores are off limits unless the user names them directly.
3. **Secret exposure**: keys and tokens are redacted from output, never committed, never sent anywhere.
4. **History rewriting**: amend, rebase and force-push on pushed branches are refused unless explicitly requested.
5. **False success claims**: tests, lint and builds must actually run before being reported as passing.
6. **Ambiguity**: when two destructive readings of a request are plausible, the agent asks instead of guessing.

## Why a skill and not a system prompt

System prompts get truncated, forgotten in long sessions, and differ per tool. A skill is a file in your repository, versioned alongside your code, loaded on demand by every major agent, and reviewable in pull requests like any other config.

## Customize

Edit `skills/agent-guardrail/SKILL.md` directly. Add project-specific rules (allowed commands, deploy targets, review requirements) in a new numbered section. Keep each rule imperative and unambiguous: agents follow rules they can check mechanically.

## Related projects

- [skills-install](https://github.com/clements23/skills-install): the installer used above, works with Claude Code, Codex, Cursor and Gemini.
- [skill-doctor](https://github.com/clements23/skill-doctor): validates skill files, including this one.
- [claude-skills-leaderboard](https://github.com/clements23/claude-skills-leaderboard): live ranking of the most starred skill repos.
- [marketing-agency-skills](https://github.com/clements23/marketing-agency-skills): business skills for marketing agencies.

## License

MIT. See [LICENSE](LICENSE).
