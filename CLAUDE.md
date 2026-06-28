# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-file personal resume website for Fan Zhang, served as a static page via GitHub Pages at the custom domain `resume.fanfly.dev` (set in `CNAME`). The entire site — markup, CSS, and JS — lives in `index.html`, which GitHub Pages serves at the site root. There is no build step, no framework, no dependencies installed locally; the only external resources are Google Fonts (Fraunces / Inter / JetBrains Mono) loaded over CDN.

## Working on it

- **Preview locally:** open `index.html` directly in a browser (`open index.html`), or serve the directory with `python3 -m http.server` and visit `localhost:8000`. No compilation.
- **Deploy:** push to `origin/main` (GitHub repo `fz172/resume`). GitHub Pages publishes automatically and serves `index.html` at the apex domain.
- No tests, linter, or package manager. The `.gitignore` is the GitHub Pages / Jekyll default boilerplate — there is no actual Jekyll content, so those tools are not in play.

## Architecture notes (things that span the file)

All of the following live inline in `index.html`:

- **Theming** is driven by CSS custom properties scoped under `html[data-theme="light"]` and `html[data-theme="dark"]`. On load, the inline `<script>` picks a theme from `prefers-color-scheme`. To restyle colors, edit the two `:root`-style variable blocks — do not hardcode colors in component rules.
- **There are two theme toggle buttons** that must stay in sync: `t1` in the sidebar and `t2` in the mobile topbar (the topbar only shows below the 860px breakpoint). Their icon/label spans are paired as `i1`/`l1` and `i2`/`l2`; `setIcons()` updates both. Any new toggle UI needs matching `i#`/`l#` elements or the sync logic breaks.
- **Scrollspy** uses an `IntersectionObserver` that maps each `#nav a` link's `href` to a `<section>` of the same `id`. Adding or renaming a section requires a matching nav link *and* section `id`, or the active-link highlighting silently stops working.
- **Responsive layout** flips at `max-width:860px`: the sticky 264px sidebar (`.side`) is hidden and the `.topbar` appears; grids collapse to one column.

## Content placeholders to fill

Parts of the resume are intentionally stubbed and should be replaced with real values before sharing: project card links (`href="#"`), the contact email (`mailto:you@example.com`), and the GitHub / YouTube contact rows ("add your handle", "add link").
