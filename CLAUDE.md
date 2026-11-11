# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Small React 18 + Vite 3 practice app ("Learn & Master GitHub Actions"), meant as a target for practicing GitHub Actions CI/CD workflows. There is no `.github/` directory yet; workflows would run the npm scripts below.

## Commands

- `npm run dev` — start Vite dev server
- `npm run build` — production build (`vite build`)
- `npm run preview` — preview the built bundle
- `npm run lint` — ESLint on `src` (`--ext .jsx --fix`, so it **auto-fixes files in place**)
- `npm test` — Vitest, single run (`vitest run`)
- Single test file: `npx vitest run src/components/MainContent.test.jsx`
- Single test by name: `npx vitest run -t "should render a button"`

## Architecture

- Component tree: `main.jsx` → `App` → `MainContent` (owns `helpVisible` state, toggle button) → `HelpArea` (static `HELP_ITEMS` array) → `HelpBox` (title/text, uses `prop-types`).
- Each component's CSS is imported by the component itself (`HelpArea.css`, `HelpBox.css`); global styles are in `src/index.css`.
- Tests live beside components (`*.test.jsx`) and use Vitest globals + jsdom + Testing Library; config sits in the `test` block of `vite.config.js`, setup in `src/test/setup.js` (loads jest-dom matchers).
- `vite-plugin-eslint` runs ESLint during dev/build, so lint errors (e.g. missing semicolons, enforced by the `semi: always` rule) can fail the build.
- Only `.jsx` files are linted (`--ext .jsx`); `.js` files are not.
