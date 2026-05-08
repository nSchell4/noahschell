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

- **Framework:** Astro (static output, mostly no client-side JS — exception is `/spriteclub`)
- **Layout:** `src/layouts/Base.astro` — shared shell with nav, Google Fonts (Inter), global styles
- **Styles:** `src/styles/global.css` — all styling in one file, CSS custom properties for theming
- **Pages:** `src/pages/index.astro` (home), `src/pages/projects.astro` (projects), `src/pages/spriteclub.astro` (NES emulator)
- **Hosting:** Cloudflare Pages (static build, output in `dist/`)

## /spriteclub — embedded NES emulator

Plays `public/spriteclub.nes` (a 6502 NES homebrew, source: [github.com/dyoustra/spriteclub](https://github.com/dyoustra/spriteclub)) in-browser via **jsnes**, loaded from `unpkg.com/jsnes@1.2.1` as an inline `<script>`.

jsnes is pure JS and tops out around ~50fps without audio on a fast machine. Audio is **off by default** with a toggle button — `onAudioSample` runs ~44,100×/sec and is the dominant CPU cost; with it off the emulator is meaningfully smoother. The page also shows an FPS counter.

### Why not EmulatorJS

EmulatorJS (RetroArch's `fceumm` core in WASM) was tried and reverted. It runs at 60fps with sound on most setups but on this user's machine it was still slow. The setup is also more involved (~2.5 MB of vendored assets, several config quirks: `compression/extract7z.js` is required because cores are 7z-packed, `EJS_defaultOptions = { webgl2Enabled: "enabled" }` is needed to avoid the slower legacy core, `EJS_disableLocalStorage = true` is needed so partial cached settings don't shadow `defaultOptions`). If revisiting, those are the gotchas to know.

### Updating the ROM

`public/spriteclub.nes` is a copy of `demo.nes` from the SpriteClub repo. To refresh after a game change: rebuild with `cl65 --target nes -o demo.nes demo.s` in the spriteclub repo, then copy the output here as `spriteclub.nes`.
