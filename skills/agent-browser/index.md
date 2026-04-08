---
layout: default
title: "Skill: Agent Browser"
---

# Agent Browser — Browser Automation for AI Agents

Browser automation CLI that uses Chrome/Chromium via CDP. Navigate pages, fill forms, click buttons, take screenshots, extract data, and automate any browser task.

## Installation

```bash
mkdir -p .claude/skills/agent-browser
curl -o .claude/skills/agent-browser/SKILL.md https://raw.githubusercontent.com/bjbbot/share/main/skills/agent-browser/SKILL.md
# Also grab references and templates
for dir in references templates; do
  mkdir -p .claude/skills/agent-browser/$dir
  # Download individual files from the repo
done
```

Or clone and copy:

```bash
git clone --depth 1 https://github.com/bjbbot/share.git /tmp/bjbbot-share
cp -r /tmp/bjbbot-share/skills/agent-browser .claude/skills/
rm -rf /tmp/bjbbot-share
```

## What It Does

- Core workflow: navigate → snapshot (get element refs) → interact → re-snapshot
- Authentication handling (state files, profiles, sessions, auth vault)
- Command chaining, parallel sessions, data extraction
- Visual debugging with headed mode, annotated screenshots, recordings
- iOS Simulator support for mobile Safari testing
- Security features: domain allowlists, action policies, content boundaries

## Bundled Resources

**References** (deep-dive documentation):
- `references/commands.md` — Full command reference
- `references/authentication.md` — Login flows, OAuth, 2FA
- `references/session-management.md` — Parallel sessions, state persistence
- `references/snapshot-refs.md` — Ref lifecycle and troubleshooting
- `references/video-recording.md` — Recording workflows
- `references/profiling.md` — Chrome DevTools profiling
- `references/proxy-support.md` — Proxy configuration

**Templates** (ready-to-use scripts):
- `templates/form-automation.sh` — Form filling with validation
- `templates/authenticated-session.sh` — Login once, reuse state
- `templates/capture-workflow.sh` — Content extraction with screenshots

## Prerequisites

Install the CLI: `npm i -g agent-browser`, `brew install agent-browser`, or `cargo install agent-browser`

Then run `agent-browser install` to download Chrome.
