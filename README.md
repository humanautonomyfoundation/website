# Human Autonomy Foundation — Website

Static marketing site built with [Astro](https://astro.build), deployed to
Cloudflare Pages. Currently a coming-soon landing page.

## Requirements

Node **22+** (Astro 7 requires it). The repo pins `22` in `.nvmrc`:

```bash
nvm use
```

## Getting started

```bash
npm install
npm run dev      # http://localhost:4321
```

## Scripts

| Command                | Does                                            |
| ---------------------- | ----------------------------------------------- |
| `npm run dev`          | Dev server with hot reload on `:4321`           |
| `npm run build`        | Type-check, then build static output to `dist/` |
| `npm run preview`      | Serve the built `dist/` locally                 |
| `npm run check`        | Astro/TypeScript diagnostics only               |
| `npm run format`       | Prettier write across the repo                  |
| `npm run format:check` | Prettier check (no writes)                      |

## Layout

```
src/
  consts.ts            Site name, tagline, status, contact email — edit copy here first
  components/          Small shared pieces (wordmark)
  layouts/Base.astro   <head>, meta/OG tags, canonical URL
  pages/index.astro    Coming-soon landing page
  pages/404.astro      Not-found page
  styles/global.css    Design tokens (light + dark) and resets
public/                Served as-is at the site root (favicon, robots.txt)
```

Colors, spacing, and fonts are CSS custom properties defined in
`src/styles/global.css`. Dark mode follows the visitor's OS setting via
`prefers-color-scheme` — change a token there and both themes stay in sync.

## Deploying

Cloudflare Pages, configured by `wrangler.toml` (`pages_build_output_dir = "dist"`).

One-time setup in the Cloudflare dashboard → **Workers & Pages → Create → Pages
→ Connect to Git**:

- Repository: `humanautonomyfoundation/website`
- Build command: `npm run build`
- Build output directory: `dist`
- Environment variable: `NODE_VERSION` = `22`

After that, pushes to `main` deploy automatically and pull requests get preview
URLs.

`site` in `astro.config.mjs` is set to `https://humanautonomyfoundation.org` —
it's the base for canonical and Open Graph URLs. Update it if the domain changes.
