# AGENTS.md - Development Guide

## Project Overview

This is a **Hugo blog** with a **Vue.js 3** frontend. The Hugo site is in the root directory, and the interactive Vue application lives in the `custom-web/` subdirectory.

## Build Commands

### Hugo Site (Root Directory)

```bash
# Build the Hugo site
hugo

# Development server with live reload
hugo server

# Build for production (minified)
hugo --minify

# Specific Hugo version used in CI: 0.128.1
```

### Vue Frontend (custom-web/ Directory)

```bash
cd custom-web

# Install dependencies
npm install
# or
pnpm install

# Development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

### Running Tests

**No test framework is currently configured** for this project.

If you add tests in the future, common patterns would be:
- Vitest: `npm run test` or `npm run test -- --run` for single run
- Jest: `npm test`

## Code Style Guidelines

### General

- Use **Vue 3 Composition API** with `<script setup>` syntax
- Use **JavaScript** (not TypeScript)
- Use **pnpm** preferred, npm also works

### Vue Component Structure

```vue
<script setup>
import { ref, computed, onMounted } from 'vue'
import SomeComponent from './components/SomeComponent.vue'
import { someUtility } from './utils'
</script>

<template>
  <div class="component-name">
    <!-- Template content -->
  </div>
</template>

<style scoped>
.component-name {
  /* Scoped CSS */
}
</style>
```

### Imports

- Vue core imports first
- Third-party imports second
- Local imports third
- Use absolute imports from `@/` (configured in vite.config.js)

### Naming Conventions

- **Components**: PascalCase (e.g., `HomeView.vue`, `Game2048.vue`)
- **Files**: kebab-case for utilities, PascalCase for components
- **Variables/functions**: camelCase
- **Constants**: SCREAMING_SNAKE_CASE
- **CSS classes**: kebab-case

### Templates

- Use self-closing tags for void elements (`<input />`, `<br />`)
- Use `v-bind:` or `:` shorthand
- Use `v-on:` or `@` shorthand

### CSS

- Use **scoped styles** in Vue components
- Prefer CSS custom properties for theming
- Keep styles simple; avoid deep selectors when possible

### Error Handling

- Use try/catch for async operations
- Handle errors gracefully in user-facing components
- Log errors appropriately for debugging

### Vue Router

- Use `createWebHashHistory` for SPA routing
- Define routes in `src/router/index.js`
- Use consistent route naming (kebab-case)

## Project Structure

```
/                     # Hugo blog root
├── content/          # Blog posts (Markdown)
├── layouts/          # Hugo layouts
├── static/           # Static assets
├── themes/           # Hugo themes
├── config.toml       # Hugo configuration
└── custom-web/      # Vue.js frontend
    ├── src/
    │   ├── components/  # Reusable Vue components
    │   ├── views/       # Page-level components
    │   ├── router/      # Vue Router configuration
    │   ├── assets/     # Static assets
    │   ├── App.vue     # Root component
    │   └── main.js     # Entry point
    ├── index.html
    └── vite.config.js
```

## Adding New Vue Pages

1. Create a new `.vue` file in `src/views/`
2. Add route in `src/router/index.js`:

```javascript
{
  path: '/new-page',
  name: 'new-page',
  component: () => import('../views/NewPage.vue')
}
```

## Hugo Content

- Add Markdown posts to `content/posts/`
- Use front matter for metadata:

```yaml
---
title: "Post Title"
date: 2024-01-01
draft: false
tags: ["tag1", "tag2"]
categories: ["category1"]
---
```

## CI/CD

GitHub Actions workflow is in `.github/workflows/pages.yml`:
- Builds Hugo site on push to main
- Deploys to GitHub Pages
- Uses Hugo 0.128.1

## Dependencies

### Vue (custom-web)
- vue: ^3.5.24
- vue-router: 4
- vite: ^7.2.4
- @vitejs/plugin-vue: ^6.0.1

### Hugo (root)
- Version: 0.128.1 (see CI workflow)
- Theme: PaperMod
