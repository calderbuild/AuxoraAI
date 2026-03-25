# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

GTM (Go-To-Market) workspace for Auxora.ai -- an AI marketing engine for US solopreneurs ($200/month, "Cursor for Marketing"). This repo contains research, plans, and operational documents. No application code lives here.

**Product**: https://staging.auxora.ai/dashboard
**Team**: Hui Li (CEO), Tingyong (engineer), Yuhong (engineer), Yiming (intern), Calder (GTM intern)
**Reddit account**: u/BeatImpress___

## Repo Structure

- Root: research artifacts (`info.md` -- AI-generated GTM research/analysis, `calder_onboarding.pdf` -- onboarding package)
- `docs/plans/`: execution plans, named `YYYY-MM-DD-type-topic-plan.md`
  - `type` tokens: `feat` (execution plan), `guide` (how-to), `report` (research/audit output)
  - Latest active plan: run `find docs/plans -name '*.md' | sort | tail -5` to find recent files

## Other Agent Config

`AGENTS.md` provides parallel guidance for non-Claude agents (e.g. Codex). Keep it in sync with this file when conventions change.

## Commands

No build pipeline. Useful review commands:

```bash
rg --files .                              # list tracked files
find docs -maxdepth 2 -type f | sort      # review document inventory
```

## Working Conventions

- All documentation in Chinese (following global CLAUDE.md); technical terms keep English
- Plan filenames: `YYYY-MM-DD-type-topic-plan.md`, lowercase hyphenated
- New files go under `docs/` unless they're root-level research artifacts
- Keep plans concise -- previous iterations bloated to 573 lines and got cut back to ~120
- Verify Markdown links, dates, and owner names stay consistent across documents

## Key Context

- 7 paying customers, 0% churn -- customer interviews are the highest-leverage GTM activity
- Product fully launches Apr 1, 2026. Content referencing the product should account for this timeline
- GTM strategy: "calibrate before distributing" -- understand customer language before Reddit/SEO/content
- Three target verticals: therapists in private practice, pest control operators, freelance consultants
