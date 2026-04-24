# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal website for Noah Schell. Built with Astro, hosted on Cloudflare Pages. Dark monochrome theme, minimal and text-focused.

## Commands

```
npm run dev       # Start dev server
npm run build     # Build static site to dist/
npm run preview   # Preview production build locally
```

## Architecture

- **Framework:** Astro (static output, no client-side JS)
- **Layout:** `src/layouts/Base.astro` — shared shell with nav, Google Fonts (Inter), global styles
- **Styles:** `src/styles/global.css` — all styling in one file, CSS custom properties for theming
- **Pages:** `src/pages/index.astro` (home), `src/pages/projects.astro` (projects)
- **Hosting:** Cloudflare Pages (static build, output in `dist/`)
