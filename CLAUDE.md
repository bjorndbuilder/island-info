# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Hugo static site providing information for remote workers/digital nomads on Koh Lanta, Thailand. Deployed to lantanomads.com via GitHub Pages.

## Commands

- **Local preview:** `hugo server --watch` (serves at http://localhost:1313)
- **Build:** `hugo --minify`
- **Lint:** Markdown linting runs in CI via `markdownlint-cli2` on `content/**/*.md`. No local lint command is configured; install `markdownlint-cli2` to run locally: `npx markdownlint-cli2 "content/**/*.md"`

## Deployment

Pushing to `main` triggers the GitHub Actions deploy workflow (`.github/workflows/deploy.yml`), which lints, builds with Hugo 0.169.0, and deploys the `public/` directory to GitHub Pages.

## Architecture

- **Content:** All site content lives in `content/` as Markdown files with YAML front matter (`title`, `description`, `group`, `weight`, `icon`). Each `.md` file becomes a page. `_index.md` is the homepage content.
- **Layouts:** Four Hugo templates in `layouts/`:
  - `_default/baseof.html` — base HTML shell (header, footer, CSS link)
  - `_default/single.html` — individual content page
  - `_default/list.html` — section listing
  - `index.html` — homepage, lists pages **grouped by the `group` front matter param**, not all `RegularPages`
- **Styling:** Single CSS file at `static/css/styles.css`, plus inline styles in templates.
- **Config:** `config.toml` — minimal Hugo config (baseURL, title, description).

## Branching

- Feature changes and bugfixes should always be applied in a separate branch, not directly on `main`.

## Commits

- Use the [Conventional Commits](https://www.conventionalcommits.org/) format (e.g., `feat:`, `fix:`, `docs:`, `chore:`).

## Hugo Gotchas

- Do not use `jsonify` to output values inside Hugo templates. It double-encodes strings (wraps in extra quotes and escapes inner quotes). Use direct interpolation instead (e.g., `"name": "{{ .Title }}"`).

## Content Conventions

- Every new content page **must** set `group`, `weight` and `icon` in front matter, otherwise it is silently omitted from the homepage and becomes an orphan page (in the sitemap, but unreachable by crawlers and users). Valid `group` values are defined in `layouts/index.html`: `getting-started`, `work`, `food-and-going-out`, `explore`, `practical`.
- Also link new pages contextually from a topically related page, not just from the homepage.
- Content files link to locations with either a Google Maps search link (`https://www.google.com/maps/search/?api=1&query=Place+Name+Koh+Lanta`) or a Google Maps short link to an exact pin (`https://maps.app.goo.gl/...`). Prefer a short link when you have the exact location — especially for small or hard-to-find spots — otherwise a search link is fine.
- Markdownlint config (`.markdownlint.json`) disables: line length (MD013), multiple top-level headings (MD025), trailing punctuation in headings (MD026), ordered list numbering (MD029), and link/image reference definitions (MD060).

## Fact-Checking

When adding or editing content that includes factual claims (prices, travel times, distances, regulations, phone numbers, business names, etc.), always verify the information by searching the web before committing. This site is a practical guide — inaccurate information can cost people time and money.
