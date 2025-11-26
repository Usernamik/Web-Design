# Vue Dating Lab

Minimal Vue 3 + TypeScript + Router project scaffold with Tailwind CSS (v4) integration.

Quick start (Windows):

1. Open terminal in project root `e:/Work Space/Web-Design/laba6`
2. Install dependencies:

```bash
npm install
```

3. Run dev server:

```bash
npm run dev
```

4. Open the URL printed by Vite (usually http://localhost:5173)

What is included:
- `src/App.vue` — main layout and navigation
- `src/router/index.ts` — routes for Home / About / Dating
- `src/views/ContactView.vue` — Dating UI with `UserCard` list and buttons
- `src/components/UserCard.vue` — Tailwind-styled card component
- `src/assets/css/index.css` — imports Tailwind

Notes:
- After `npm install`, Vite + Tailwind plugin will process styles automatically.
- To enable dark mode locally, set `class="dark"` on `<html>` or configure Tailwind's dark mode in real project.
