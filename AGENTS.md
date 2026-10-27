# Repository Guidelines: shiroiyuki.github.io

This repository hosts the personal blog for **shiroiyuki (ゆうき)**, powered by Astro and the Firefly theme with fullscreen anime wallpapers, frosted glass cards, and automated GitHub Actions deployment.

## Project Structure & Content Organization

- **Blog Posts**: `src/content/posts/` (Markdown `.md` and MDX `.mdx` files).
  - Drafts can be marked with `draft: true` in the frontmatter to prevent public deployment.
- **Site Configurations**:
  - `src/config/siteConfig.ts`: Site title, author profile, language, and feature toggles.
  - `src/config/backgroundWallpaper.ts`: Wallpaper mode (`fullscreen` / `banner`), images, and blur effects.
  - `src/config/profileConfig.ts`: Social links and author bio.
- **Static Assets & Icons**: `public/` (contains custom `favicon.ico`, `public/favicon/` icons, and music/video assets).
- **Core Components & Layouts**: `src/components/`, `src/layouts/`, and `src/styles/`.

## Key Commands (pnpm only)

Always use `pnpm` (enforced by the project):

- `pnpm dev`: Start local Astro development server with hot-reload (`http://localhost:4321`).
- `pnpm build`: Generate static production build into `dist/` (includes LQIPs, font subsets, and Pagefind search index).
- `pnpm preview`: Preview production build locally.
- `pnpm new-post`: Interactive helper to scaffold a new blog post.

## Deployment & Workflow

- **Branch**: `main` is the production branch.
- **Deployment**: Any push to `main` triggers `.github/workflows/deploy.yml` which builds and deploys the site to GitHub Pages (`https://shiroiyuki.github.io/`).
- Direct push to `main` is the preferred workflow for this personal blog.
