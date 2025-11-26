# Vue 3 + Vite + Tailwind (Lab example)
# Vue 3 + Vite + Tailwind (Lab example)

This repository is a minimal scaffold for the Lab task: integrate Tailwind CSS (v4) into a Vue 3 + Vite project and refactor styles to utility-first classes.

Quick steps to run locally:

1. Install dependencies (run in project root):

   npm install

2. Optionally ensure Tailwind packages are installed as devDependencies:

   npm install -D tailwindcss @tailwindcss/vite

3. Run dev server:

   npm run dev

Open http://localhost:5173

What I changed / created:
- `vite.config.ts` — registers `@tailwindcss/vite` plugin
- `tailwind.config.cjs` — Tailwind configuration with `darkMode: 'class'` and `content` paths
- `src/assets/css/index.css` — single `@import "tailwindcss"` (Tailwind v4 style)
- `src/main.ts` — imports the CSS and sets up router
- `src/components/UserCard.vue` — refactored to Tailwind utilities, supports dark theme and `isActive` conditional classes
- `src/views/ContactView.vue`, `AboutView.vue`, `HomeView.vue` — simple view components
- `src/App.vue` — nav styled with Tailwind and a theme toggle button
- `package.json` — scripts and devDependencies (you must run `npm install` locally)

Dark mode and configuration notes
- I added `tailwind.config.cjs` with `darkMode: 'class'` and the `content` paths so Tailwind can tree-shake unused utilities. You can extend colors and plugins in this file.
- The app includes a theme toggle in the top-right of the navigation. It saves the preference to `localStorage` and toggles the `dark` class on the `html` element so Tailwind's `dark:` utilities apply.

Toggle theme manually:

```html
<!-- add or remove the `dark` class to enable/disable dark styles -->
<html class="dark"> ... </html>
```

Programmatic toggle:

- The toggle button in the nav updates the `localStorage` key `theme` with `dark` or `light` and applies the `dark` class on the root element automatically.

To customize Tailwind (colors, plugins, etc.) edit `tailwind.config.cjs`.

Report template answers are included in the repository for your lab report; ask if you want them copied into a separate document.
