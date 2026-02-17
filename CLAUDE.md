# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A Hugo static site providing information for remote workers/digital nomads on Koh Lanta, Thailand. Deployed to lantanomads.com via GitHub Pages.

## Commands

- **Local preview:** `hugo server --watch` (serves at http://localhost:1313)
- **Build:** `hugo --minify`
- **Lint:** Markdown linting runs in CI via `markdownlint-cli2` on `content/**/*.md`. No local lint command is configured; install `markdownlint-cli2` to run locally: `npx markdownlint-cli2 "content/**/*.md"`

## Deployment

Pushing to `main` triggers the GitHub Actions deploy workflow (`.github/workflows/deploy.yml`), which lints, builds with Hugo 0.114.0, and deploys the `public/` directory to GitHub Pages.

## Architecture

- **Content:** All site content lives in `content/` as Markdown files with YAML front matter (`title` and `description`). Each `.md` file becomes a page. `_index.md` is the homepage content.
- **Layouts:** Four Hugo templates in `layouts/`:
  - `_default/baseof.html` — base HTML shell (header, footer, CSS link)
  - `_default/single.html` — individual content page
  - `_default/list.html` — section listing
  - `index.html` — homepage, lists all `RegularPages`
- **Styling:** Single CSS file at `static/css/styles.css`, plus inline styles in templates.
- **Config:** `config.toml` — minimal Hugo config (baseURL, title, description).

## Commits

- Use the [Conventional Commits](https://www.conventionalcommits.org/) format (e.g., `feat:`, `fix:`, `docs:`, `chore:`).

## Hugo Gotchas

- Do not use `jsonify` to output values inside Hugo templates. It double-encodes strings (wraps in extra quotes and escapes inner quotes). Use direct interpolation instead (e.g., `"name": "{{ .Title }}"`).

## Content Conventions

- Content files use Google Maps search links for locations: `https://www.google.com/maps/search/?api=1&query=Place+Name+Koh+Lanta`
- Markdownlint config (`.markdownlint.json`) disables: line length (MD013), multiple top-level headings (MD025), trailing punctuation in headings (MD026), ordered list numbering (MD029), and link/image reference definitions (MD060).

## Fact-Checking

When adding or editing content that includes factual claims (prices, travel times, distances, regulations, phone numbers, business names, etc.), always verify the information by searching the web before committing. This site is a practical guide — inaccurate information can cost people time and money.
