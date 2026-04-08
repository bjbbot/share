---
layout: default
title: "Skill: Webapp Testing"
---

# Webapp Testing — Playwright Testing Toolkit

Toolkit for testing local web applications using Python Playwright. Supports verifying frontend functionality, debugging UI behavior, capturing screenshots, and viewing browser logs.

## Installation

```bash
mkdir -p .claude/skills/webapp-testing/scripts .claude/skills/webapp-testing/examples
curl -o .claude/skills/webapp-testing/SKILL.md https://raw.githubusercontent.com/bjbbot/share/main/skills/webapp-testing/SKILL.md
curl -o .claude/skills/webapp-testing/scripts/with_server.py https://raw.githubusercontent.com/bjbbot/share/main/skills/webapp-testing/scripts/with_server.py
for f in console_logging.py element_discovery.py static_html_automation.py; do
  curl -o .claude/skills/webapp-testing/examples/$f https://raw.githubusercontent.com/bjbbot/share/main/skills/webapp-testing/examples/$f
done
```

## What It Does

- Decision tree for choosing static vs dynamic testing approach
- Server lifecycle management via `with_server.py` (supports multiple servers)
- Reconnaissance-then-action pattern for dynamic web apps
- Wait for `networkidle` before DOM inspection

## Bundled Resources

- `scripts/with_server.py` — Manages server startup/shutdown around test runs (supports multi-server)
- `examples/element_discovery.py` — Discovering buttons, links, inputs
- `examples/console_logging.py` — Capturing console logs
- `examples/static_html_automation.py` — Using file:// URLs for local HTML

## Prerequisites

Python with Playwright: `pip install playwright && playwright install chromium`
