# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hextra is a Hugo theme for building documentation and blog sites, inspired by Nextra. It uses Tailwind CSS v4, supports 21 languages, and includes features like full-text search (FlexSearch), dark mode, and shortcodes.

The repo contains both the theme source (`/layouts`, `/assets`, `/i18n`, `/data`) and a documentation site (`/docs`) that serves as a live example.

## Development Commands

```bash
npm install                  # Install dependencies (first time)
npm run dev:theme            # Dev server with theme hot-reload (uses dev.toml cache busters)
npm run dev                  # Dev server for docs site only
npm run build:css            # Compile Tailwind CSS to assets/css/compiled/main.css
npm run build                # Production build (hugo --gc --minify)
npm run test                 # Run all Playwright E2E tests
npm run test:a11y            # Accessibility tests (axe-core)
npm run test:mobile-menu     # Mobile menu tests
```

Requires Hugo >= 0.146.0 (extended edition) and Go >= 1.21. Node.js is needed for Tailwind/PostCSS and tests.

## Architecture

**Theme layouts** (`/layouts`):
- `baseof.html` — base HTML skeleton; all pages extend this via `block "main"`
- `docs/` and `blog/` — section-specific layouts
- `_partials/` — reusable components (navbar, sidebar, toc, footer, search, theme-toggle)
- `_partials/scripts/` — conditional script loading (katex, mermaid, medium-zoom, etc.)
- `_shortcodes/` — template shortcodes (card, callout, tabs, steps, badge, filetree, etc.)
- `_markup/` — Markdown render hook overrides (links, headings, codeblocks)

**Assets** (`/assets`):
- `css/styles.css` — Tailwind v4 entry point using `hx:` prefix; component CSS in `css/components/`
- `js/core/` — core JS modules; `js/flexsearch.js` for search; `js/head/` for early-loading scripts

**Documentation site** (`/docs`):
- `docs/hugo.yaml` — site config (multilingual: en, ja, zh-cn)
- `docs/hugo.work` — Hugo workspace file linking the parent theme for local development
- `docs/content/` — Markdown content organized by language

**Data**: `/data/icons.yaml` contains all SVG icon definitions. `/i18n/` has translation strings for 21 locales.

## Key Conventions

- Uses **Conventional Commits** for commit messages
- Tailwind uses custom `hx:` prefix and CSS variables for primary colors (HSL)
- Dark mode via Tailwind `dark:` selector
- Hugo module system (`go.mod`) — theme is imported as a Hugo module by consumers
- Prettier with `go-template` parser for formatting HTML templates
