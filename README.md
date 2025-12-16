Robotics Project — Site scaffold

This repository contains a scaffold for a GitHub Pages site (Jekyll) for your robotics project report. Edit the markdown pages to add content and drop images, videos, code, and CAD files into subfolders.

Quick start

1. Add your content to the markdown files (Introduction, Design, Implementation, Results, Conclusion, Team, Additional Materials).
2. Commit and push to GitHub (main branch).
3. Enable GitHub Pages in your repository settings: set source to `gh-pages` (if using the Actions deploy) or to `main` branch and root if you prefer a simple Jekyll build.

Notes

- The site uses a simple custom layout in `_layouts/default.html` and a navigation include in `_includes/nav.html`.
- The GitHub Actions workflow builds the site and deploys to GitHub Pages via `peaceiris/actions-gh-pages` on pushes to `main`.

If you want, I can:
- Switch deployment to use the `pages` action instead,
- Add a `Gemfile` and `bundle` configuration,
- Create a `docs/`-based site instead of deploying via Actions.

Tell me which option you prefer or add your resources and I'll integrate them.