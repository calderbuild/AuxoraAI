# Repository Guidelines

## Project Structure & Module Organization
This repository is document-first. Keep top-level research artifacts in the root, and put working plans under [`docs/plans/`](./docs/plans/). Current examples include `info.md` for market research, `calder_onboarding.pdf` for onboarding material, and `docs/plans/2026-03-23-feat-auxora-gtm-execution-plan.md` for execution planning. Follow the existing filename pattern for new plans: `YYYY-MM-DD-type-topic.md`.

## Build, Test, and Development Commands
No application build pipeline is configured in this workspace. Use lightweight review commands instead:

- `rg --files .` lists tracked working files quickly.
- `sed -n '1,120p' info.md` previews a Markdown file without opening an editor.
- `find docs -maxdepth 2 -type f | sort` reviews document inventory before adding new files.

Before submitting changes, verify links, headings, and filenames manually. For Markdown-heavy edits, keep diffs small and easy to review.

## Coding Style & Naming Conventions
Write documentation in concise, business-ready prose. Prefer Markdown with clear `#` / `##` headings, short paragraphs, and flat bullet lists. Keep plan files dated and descriptive. Use lowercase, hyphenated filenames for new Markdown files, except when preserving an established pattern such as `2026-03-23-feat-auxora-gtm-execution-plan.md`. Avoid creating new top-level folders unless the content cannot fit under `docs/`.

## Testing Guidelines
There is no automated test suite yet. Treat review quality as the baseline:

- confirm Markdown renders cleanly,
- verify internal file references and external links,
- check that dates, owners, and deliverables stay consistent across edited documents.

If you add scripts or code later, include runnable validation commands in this file as part of the same change.

## Commit & Pull Request Guidelines
This workspace snapshot does not include local Git history, so no repository-specific commit convention could be inspected. Use short, imperative subjects with a scope when helpful, for example: `docs: tighten GTM execution plan`. Keep each commit focused on one document or one decision. Pull requests should state the purpose, summarize changed files, note any follow-up questions, and include screenshots only when visual assets such as `image.png` are updated.

## Security & Content Handling
Do not commit credentials, private customer data, or internal-only notes copied from external systems. Large binary assets should be added only when necessary; prefer linking source material in the relevant plan or research document.
