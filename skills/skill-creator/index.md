---
layout: default
title: "Skill: Skill Creator"
---

# Skill Creator

A guide for creating effective Claude Code skills — modular packages that extend Claude's capabilities with specialized knowledge, workflows, and tool integrations.

## Installation

```bash
mkdir -p .claude/skills/skill-creator
curl -o .claude/skills/skill-creator/SKILL.md https://raw.githubusercontent.com/bjbbot/share/main/skills/skill-creator/SKILL.md
# Also grab the helper scripts
mkdir -p .claude/skills/skill-creator/scripts
for f in init_skill.py package_skill.py quick_validate.py; do
  curl -o .claude/skills/skill-creator/scripts/$f https://raw.githubusercontent.com/bjbbot/share/main/skills/skill-creator/scripts/$f
done
```

## What It Does

- Walks through a structured skill creation process (understand, plan, init, edit, package, iterate)
- Provides `init_skill.py` to scaffold new skills with proper structure
- Provides `package_skill.py` to validate and zip skills for distribution
- Provides `quick_validate.py` for fast validation checks
- Teaches progressive disclosure design (metadata → SKILL.md → bundled resources)

## Bundled Resources

- `scripts/init_skill.py` — Scaffold a new skill directory
- `scripts/package_skill.py` — Validate and package a skill as a zip
- `scripts/quick_validate.py` — Quick validation of skill structure
