# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install      # Install dependencies
npm run dev      # Start dev server on port 3000 (auto-opens browser)
npm run build    # Production build → outputs to build/
```

No test or lint scripts are configured.

## Architecture

This is a single-page React + TypeScript game built with Vite and Tailwind CSS v4.

**Entry points**: `index.html` → `src/main.tsx` → `src/App.tsx`

**Game logic** lives entirely in `src/App.tsx`:
- 3 treasure boxes, one randomly assigned treasure at init
- Opening a box: +$100 for treasure, -$50 for skeleton
- Game ends when treasure is found OR all boxes are opened
- `initializeGame()` randomizes box contents; `openBox(id)` handles scoring and win/loss logic

**Assets**:
- `src/assets/` — chest/key PNG images (closed, opened-treasure, opened-skeleton, key cursor)
- `src/audios/` — `chest_open.mp3` (treasure) and `chest_open_with_evil_laugh.mp3` (skeleton)

**UI components**: `src/components/ui/` contains 50+ Radix UI-based components. Currently only `Button` is used in the game. `src/components/figma/ImageWithFallback.tsx` wraps images with error fallback.

**Styling**: Tailwind CSS v4 utility classes + CSS custom properties defined in `src/styles/globals.css`. Amber/gold color theme. Responsive: 1-column mobile → 3-column desktop grid. Dark mode supported via CSS variables.

**Animations**: Uses `motion/react` (Framer Motion) for box flip (180° rotate), scale, and fade-in effects.
