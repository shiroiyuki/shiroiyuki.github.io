# Repository Guidelines: shiroiyuki.github.io

This repository hosts the personal blog for **shiroiyuki (ゆうき)** (`https://shiroiyuki.github.io/`), built with Astro 7, Svelte 5 islands, Tailwind CSS 4, and TypeScript (customized from the Firefly theme).

## Project Structure & Module Organization

- **Main Source (`src/`)**:
  - `src/content/posts/`: Blog posts (`.md` and `.mdx`). Set `draft: true` in frontmatter to hide unfinished posts from production builds.
  - `src/content/dynamic/`: Timestamped micro-status updates (`.md`).
  - `src/content/projects/`: Project showcase entries (`.md` and `.mdx`).
  - `src/content/spec/`: Standalone page content (`about.md`, `friends.mdx`).
  - `src/config/`: Site configuration modules (`siteConfig.ts`, `backgroundWallpaper.ts`, `profileConfig.ts`, `navBarConfig.ts`, etc.) with matching type definitions in `src/types/`. Prefer imports from `@/config` when available.
  - `src/pages/`, `src/layouts/`, `src/components/`, `src/styles/`, `src/utils/`, `src/plugins/`: Core routing, UI components, utilities, and Markdown/Rehype/Remark plugins.
- **Static & Managed Assets**:
  - `public/`: Static files served directly at root (`favicon.ico`, `public/favicon/`, wallpapers, audio).
  - `src/assets/`: Source-managed and optimized images (`src/assets/images/logo/shiroiyuki-logo.png`, wallpapers).
- **Automation (`scripts/`)**: Build-time and authoring helper scripts (`new-post.js`, `new-dynamic.js`, `generate-lqips.ts`, `generate-github-card-data.ts`, `subset-fonts.ts`, `run-pagefind.ts`).

## Build, Writing, and Development Commands

Always use `pnpm` (enforced by `preinstall`):

- `pnpm install`: Install dependencies.
- `pnpm dev` / `pnpm start`: Start the local Astro dev server (`http://localhost:4321`).
- `pnpm build`: Run full production build pipeline into `dist/` (generates GitHub card data, LQIPs, VNDB covers, Astro static build, PIO asset pruning, font subsets, inline script minification, and Pagefind search index).
- `pnpm preview`: Preview the production `dist/` build locally.
- `pnpm new-post <filename>`: Scaffold a new post in `src/content/posts/` (supports nested paths and auto-converts Chinese characters in `slug` to pinyin).
- `pnpm new-d <content>` / `pnpm new-dynamic <content>`: Create a timestamped dynamic entry in `src/content/dynamic/`.
- `pnpm check`: Run Astro diagnostics (`astro check`).
- `pnpm type-check`: Run TypeScript check (`tsc --noEmit --isolatedDeclarations`).
- `pnpm format`: Format `./src` and `./scripts` with Biome.
- `pnpm lint`: Run Biome checks and safe fixes on `./src` and `./scripts`.
- `pnpm lqips`: Regenerate Low-Quality Image Placeholders (`src/constants/lqips.json`).
- `pnpm github-cards`: Refresh cached GitHub repository card metadata.

## Coding Style & Conventions

- **Formatter & Linter**: Biome (`biome.json`) is used for formatting and linting (tabs for indentation, double quotes for JS/TS strings).
- **Naming**: Keep Astro and Svelte components in `PascalCase` (`PostCard.astro`, `Search.svelte`), config modules in `camelCase` ending with `Config.ts`, and utilities in `kebab-case` (`date-utils.ts`). Keep `src/types/` aligned with `src/config/`.
- **Content Preservation**: Never delete existing posts, dynamics, or sample templates in `src/content/` unless explicitly instructed by the user.

## Verification & Deployment Workflow

- Before pushing significant template or config changes, verify with `pnpm check`, `pnpm type-check`, and `pnpm build`.
- **Deployment**: `main` is the single production branch. Pushing to `main` triggers `.github/workflows/deploy.yml` (Node 24 + `pnpm`) to automatically build and deploy to GitHub Pages (`https://shiroiyuki.github.io/`).
- Use Conventional Commits (`feat: ...`, `fix: ...`, `docs: ...`, `chore: ...`). Do not commit secrets or tokens in config files.
