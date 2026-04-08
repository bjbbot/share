---
layout: default
title: "Skill: Codex CLI Integration"
---

# Codex CLI Integration for Claude Code

**Source**: [skills-directory/skill-codex](https://github.com/skills-directory/skill-codex)

Enable Claude Code to invoke the OpenAI Codex CLI (`codex exec` and session resumes) for automated code analysis, refactoring, and editing workflows.

## Installation

Copy the `SKILL.md` below into your project at `.claude/skills/codex/SKILL.md`.

## SKILL.md

```markdown
---
name: codex
description: Use when the user asks to run Codex CLI (codex exec, codex resume) or references OpenAI Codex for code analysis, refactoring, or automated editing
---

# Codex Skill Guide

## Prerequisites Check
Before running any Codex command, verify the CLI is installed by running `codex --version`. If the command is not found or fails, install it automatically:
npm install -g @openai/codex
Then confirm with `codex --version` before proceeding. If installation fails, report the error and ask the user for guidance.

## Running a Task
1. Ask the user (via `AskUserQuestion`) which model to run (`gpt-5.4`, `gpt-5.3-codex-spark`, or `gpt-5.3-codex`) AND which reasoning effort to use (`xhigh`, `high`, `medium`, or `low`) in a single prompt with two questions.
2. Select the sandbox mode required for the task; default to `--sandbox read-only` unless edits or network access are necessary.
3. Assemble the command with the appropriate options:
   - `-m, --model <MODEL>`
   - `--config model_reasoning_effort="<xhigh|high|medium|low>"`
   - `--sandbox <read-only|workspace-write|danger-full-access>`
   - `--full-auto`
   - `-C, --cd <DIR>`
   - `--skip-git-repo-check`
   - `"your prompt here"` (as final positional argument)
4. Always use --skip-git-repo-check.
5. When continuing a previous session, use `codex exec --skip-git-repo-check resume --last` via stdin. Resume syntax: `echo "your prompt here" | codex exec --skip-git-repo-check resume --last 2>/dev/null`. All flags have to be inserted between exec and resume.
6. By default, append `2>/dev/null` to all `codex exec` commands to suppress thinking tokens (stderr). Only show stderr if the user explicitly requests it.
7. Run the command, capture stdout/stderr (filtered as appropriate), and summarize the outcome for the user.
8. After Codex completes, inform the user: "You can resume this Codex session at any time by saying 'codex resume' or asking me to continue with additional analysis or changes."

### Quick Reference
| Use case | Sandbox mode | Key flags |
| --- | --- | --- |
| Read-only review or analysis | `read-only` | `--sandbox read-only 2>/dev/null` |
| Apply local edits | `workspace-write` | `--sandbox workspace-write --full-auto 2>/dev/null` |
| Permit network or broad access | `danger-full-access` | `--sandbox danger-full-access --full-auto 2>/dev/null` |
| Resume recent session | Inherited from original | `echo "prompt" \| codex exec --skip-git-repo-check resume --last 2>/dev/null` |
| Run from another directory | Match task needs | `-C <DIR>` plus other flags `2>/dev/null` |

## Following Up
- After every `codex` command, use `AskUserQuestion` to confirm next steps or decide whether to resume.
- When resuming, pipe the new prompt via stdin: `echo "new prompt" | codex exec resume --last 2>/dev/null`.
- Restate the chosen model, reasoning effort, and sandbox mode when proposing follow-up actions.

## Critical Evaluation of Codex Output
Codex is powered by OpenAI models with their own knowledge cutoffs and limitations. Treat Codex as a colleague, not an authority.
- Trust your own knowledge when confident.
- Research disagreements using WebSearch or documentation before accepting claims.
- Don't defer blindly — Codex can be wrong about model names, library versions, or best practices.

## Error Handling
- Stop and report failures whenever `codex --version` or `codex exec` exits non-zero.
- Ask permission before using high-impact flags (`--full-auto`, `--sandbox danger-full-access`).
- Summarize warnings or partial results and ask how to adjust.
```

## Notes

- Requires `codex` CLI installed and on PATH (`npm install -g @openai/codex`)
- Requires valid OpenAI credentials configured for Codex
- Our version adds an auto-install prerequisite check not in the upstream skill
