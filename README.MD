This repository contains a website called Lanta Nomands with information for remote workers
coming to Koh Lanta in Thailand. It provides answers to most asked questions like how to 
get there, where to stay and how to get around.

The information itself is stored in Markdown files in the data directory.

---

## Website & Deployment 🔧

A Hugo site has been added to this repository and will be built and deployed to GitHub Pages via GitHub Actions whenever you push to `main`.

Quick start locally:

1. Install Hugo: https://gohugo.io/getting-started/install
2. Preview the site: `hugo server --watch` and open http://localhost:1313
3. Build the static site: `hugo` (the generated site will be in `public/`)

Before publishing, update `config.toml`'s `baseURL` to your GitHub Pages URL (for example: `https://<your-github-username>.github.io/lantanomads/`).

The workflow `.github/workflows/deploy.yml` builds the site with Hugo and deploys `public/` to GitHub Pages using `peaceiris/actions-gh-pages`.


