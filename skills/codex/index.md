---
layout: default
title: "Skill: Codex CLI Integration"
---

# Codex CLI Integration for Claude Code

**Source**: [skills-directory/skill-codex](https://github.com/skills-directory/skill-codex)

Enable Claude Code to invoke the OpenAI Codex CLI (`codex exec` and session resumes) for automated code analysis, refactoring, and editing workflows.

## Installation

Copy [`SKILL.md`](SKILL.md) into your project:

```bash
mkdir -p .claude/skills/codex
curl -o .claude/skills/codex/SKILL.md https://raw.githubusercontent.com/bjbbot/share/main/skills/codex/SKILL.md
```

Or manually copy the [raw SKILL.md](https://github.com/bjbbot/share/blob/main/skills/codex/SKILL.md) to `.claude/skills/codex/SKILL.md` in your repo.

## What It Does

- Auto-installs `codex` CLI if not present
- Prompts for model choice and reasoning effort
- Manages sandbox modes (read-only, workspace-write, full-access)
- Supports session resume via `codex exec resume --last`
- Suppresses thinking tokens by default to keep context clean
- Critically evaluates Codex output rather than blindly trusting it

## Notes

- Requires `codex` CLI installed and on PATH (`npm install -g @openai/codex`)
- Requires valid OpenAI credentials configured for Codex
- Our version adds an auto-install prerequisite check not in the upstream skill
