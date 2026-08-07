# Personal portfolio

Bento-style personal portfolio built with **[Astro](https://astro.build)**.

---

## Features

- 🧩 **Bento-grid layout** — sleek, minimal, single-page-first design
- 🎨 **Dark mode base** with a white mode planned from the Paper style
- 📱 **Fully responsive**
- 📁 **Projects** section for personal work
- 🚀 **Performance & SEO optimized** — sitemap, robots.txt, Open Graph tags
- ☁️ Ready to deploy on **[Netlify](https://www.netlify.com/)** (SSR)

## Tech Stack

| Area       | Tools                                                                                                                             |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Framework  | [Astro](https://astro.build) (SSR)                                                                                                |
| Styling    | [UnoCSS](https://unocss.dev/)                                                                                                     |
| Icons      | [astro-icon](https://github.com/natemoo-re/astro-icon) and Remix Icons                                                           |
| Animation  | [Motion](https://motion.dev/) and [GSAP](https://gsap.com/)                                                                      |
| Hosting    | [Netlify adapter](https://docs.astro.build/en/guides/integrations-guide/netlify/)                                                 |

## Prerequisites

- **Node.js** `24.13.0` (see [`.nvmrc`](.nvmrc) — run `nvm use`)
- **[pnpm](https://pnpm.io/)** (this repo uses `pnpm@10`)

## Getting Started

```bash
# 1. Clone
git clone https://github.com/Ladvace/astro-bento-portfolio
cd astro-bento-portfolio

# 2. Install dependencies
pnpm install

# 3. Start the dev server (http://localhost:4321)
pnpm dev
```

## Make It Yours

Run the interactive setup to personalize the site:

```bash
pnpm site-setup
```

This walks you through your name, links, email, location/timezone and more, updating `src/site-config.ts` and writing `SITE_URL` to `.env`. Restart the dev server afterwards.

A few things the script **doesn't** cover:

- Swap the avatar/memoji image — replace `src/assets/me-dither.webp` with your own.
- Remove (or replace with your own ID) the **Umami analytics** script tag in `src/layouts/BasicLayout.astro`.

## Scripts

| Command           | Description                          |
| ----------------- | ------------------------------------ |
| `pnpm dev`        | Start the dev server                 |
| `pnpm build`      | Production build                     |
| `pnpm preview`    | Preview the production build locally |
| `pnpm check`      | Type-check with `astro check`        |
| `pnpm eslint`     | Lint `src`                           |
| `pnpm format`     | Format with Prettier                 |
| `pnpm site-setup` | Interactive personalization          |

## Deploy on Netlify 🚀

Deploying on Netlify is optional. Link this repository to your Netlify account and configure `SITE_URL` plus any Umami variables in the project settings.

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/Ladvace/astro-bento-portfolio)

## License

Released under the [MIT License](LICENSE).

## Author

**Patrick Girardi** — [github.com/trickgirardi](https://github.com/trickgirardi)
