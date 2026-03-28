# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

GTM (Go-To-Market) workspace for Auxora.ai -- an AI marketing engine for US solopreneurs ($200/month, "Cursor for Marketing"). This repo contains research, plans, and operational documents. No application code lives here.

**Product**: https://staging.auxora.ai/dashboard (production: app.auxora.ai)
**Team**: Hui Li (CEO), Tingyong (engineer), Yuhong (engineer), Yiming (intern), Calder (GTM intern)
**Reddit account**: u/BeatImpress___

## Repo Structure

- Root: research artifacts (`info.md`, `calder_onboarding.pdf`) and agent configs (`AGENTS.md`)
- `docs/plans/`: execution plans, reports, and guides (`.md` primary, occasional `.docx` for external sharing)
- `docs/screenshots/`: product screenshots referenced by reports -- always use relative paths (`../screenshots/filename.png`), never absolute or raw GitHub URLs

Note: root-level PNG files are legacy duplicates of `docs/screenshots/` and should not be referenced in new documents.

## Other Agent Config

`AGENTS.md` provides parallel guidance for non-Claude agents (e.g. Codex). Keep it in sync with this file when conventions change.

## Commands

No build pipeline. Useful review commands:

```bash
find docs/plans -name '*.md' | sort | tail -5   # find recent plans
find docs -maxdepth 2 -type f | sort             # review document inventory
```

## Working Conventions

### File Naming

Plan filenames: `YYYY-MM-DD-type-topic.md`, lowercase hyphenated. `type` tokens: `feat` (execution plan), `guide` (how-to), `report` (research/audit output).

### Frontmatter

All plan/report files must include YAML frontmatter:

```yaml
---
title: 标题
type: report | feat | guide
date: YYYY-MM-DD
author: Name
audience: Name (Role)
---
```

### Writing

- All documentation in Chinese; technical terms keep English
- Keep plans concise -- target ~120 lines, avoid bloat
- Verify Markdown links, dates, and owner names stay consistent across documents
- New files go under `docs/` unless they're root-level research artifacts
- Screenshots go in `docs/screenshots/`, referenced with relative paths

### Pre-commit Checks

Before committing, verify:
- Frontmatter fields complete and date correct
- Dates, owner names, and deliverables consistent throughout the document
- Screenshot paths reference `docs/screenshots/` with relative paths (not root-level PNGs)
- No `.DS_Store`, credentials, or sensitive data staged

### Commits

Use `docs:` scope prefix with imperative subject. Example: `docs: add Case A diagnosis report`

## Key Context

- 7 paying customers, 0% churn -- customer interviews are the highest-leverage GTM activity
- Product fully launches Apr 1, 2026. Content referencing the product should account for this timeline
- GTM strategy: "calibrate before distributing" -- understand customer language before Reddit/SEO/content
- Three target verticals: therapists in private practice, pest control operators, freelance consultants
