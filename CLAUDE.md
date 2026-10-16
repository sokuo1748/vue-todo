# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

A todo app, split into two independently-developed halves:

- `frontend/` — Vue 3 + TypeScript + Vite + Pinia. Currently the stock Vite scaffold (`App.vue`, `main.ts`, one placeholder component); no routes, stores, or todo-specific code exist yet.
- `backend/` — reserved for a Python backend. Not scaffolded yet (empty directory).

There is no root-level `package.json` — work inside `frontend/` for all frontend commands.

## Product spec

The app is not yet implemented against this spec; use it to guide structure (data model, filters) when building out `frontend/` and `backend/`:

1. **Add a todo item** — records a description, a done/not-done status, and an optional due time.
2. **Four filter tags**: 已完成 (completed), 未完成 (not done), 待辦中 (in progress), 暫訂事項 (tentative).
3. **暫訂事項 (tentative) items never show a time** — tentative is the one status that has no due time, even if one was set.

## Commands

All commands run from `frontend/`:

```bash
npm install        # install deps
npm run dev         # start Vite dev server
npm run build       # type-check (vue-tsc -b) then production build
npm run preview     # preview the production build
```

No lint or test scripts are configured yet in `frontend/package.json`. `backend/` has no commands yet since it has no code.

## Architecture notes

- `frontend/src/main.ts` creates the Vue app and installs Pinia (`createPinia()`) before mounting — any new global store must be registered through this Pinia instance, not instantiated ad hoc.
- Uses `<script setup>` SFCs (per the Vue 3 + TS template); no Vue Router is installed.
- `vite.config.ts` only wires up `@vitejs/plugin-vue` — no path aliases or other plugins configured.
- TypeScript config is split per Vite's template convention: `tsconfig.json` is a references-only root, `tsconfig.app.json` covers `src/`, `tsconfig.node.json` covers Vite config itself.
