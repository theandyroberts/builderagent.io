# BuilderAgent — Marketing Site

The marketing and SEO site for [BuilderAgent.io](https://builderagent.io). Built with **Astro 5** + **Tailwind 4**, deployed via **Cloudflare Pages** from this GitHub repo.

## Stack

- [Astro 5](https://astro.build) — static site generator (zero JS by default).
- [Tailwind CSS 4](https://tailwindcss.com) — styling, design tokens in `src/styles/global.css`.
- [@astrojs/sitemap](https://docs.astro.build/en/guides/integrations-guide/sitemap/) — auto-generated `sitemap-index.xml`.
- [@astrojs/mdx](https://docs.astro.build/en/guides/integrations-guide/mdx/) — Markdown/MDX blog posts.
- [@astrojs/rss](https://docs.astro.build/en/guides/rss/) — RSS feed at `/rss.xml`.

## Local development

Requires Node 22+ (see `.nvmrc`).

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # outputs to ./dist
npm run preview
```

## Project structure

```
.
├── public/                       # Static, copied as-is to /
│   ├── robots.txt                # SEO
│   ├── favicon.svg
│   ├── logo.svg
│   ├── _headers                  # Cloudflare Pages caching + security
│   └── _redirects                # Cloudflare Pages URL redirects
├── src/
│   ├── components/               # Header, Footer, SEO head
│   ├── content/
│   │   ├── blog/                 # Markdown blog posts
│   │   └── ../content.config.ts  # Content collection schema
│   ├── layouts/
│   │   └── BaseLayout.astro      # HTML shell, SEO, header/footer
│   ├── pages/                    # File-based routing
│   │   ├── index.astro           # /
│   │   ├── features.astro        # /features
│   │   ├── pricing.astro         # /pricing
│   │   ├── use-cases.astro       # /use-cases
│   │   ├── about.astro           # /about
│   │   ├── contact.astro         # /contact
│   │   ├── 404.astro             # /404
│   │   ├── privacy.astro         # /privacy
│   │   ├── terms.astro           # /terms
│   │   ├── rss.xml.ts            # /rss.xml
│   │   ├── blog/
│   │   │   ├── index.astro       # /blog
│   │   │   └── [...slug].astro   # /blog/:slug
│   │   └── docs/
│   │       └── index.astro       # /docs
│   └── styles/
│       └── global.css            # Tailwind import + design tokens
├── astro.config.mjs              # Site URL, integrations, vite plugins
├── tsconfig.json
├── package.json
└── .nvmrc
```

## Deployment — Cloudflare Pages

1. Push this repo to GitHub.
2. In Cloudflare → **Pages** → **Create a project** → **Connect to Git** → select this repo.
3. Set the build settings:
   - **Framework preset**: Astro
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
   - **Node version**: 22 (set via `NODE_VERSION` env var or `.nvmrc`)
4. (Optional) Add a custom domain pointing to the Pages project. The included `_redirects` and `_headers` files apply automatically.

Subsequent pushes to `main` auto-deploy.

## SEO checklist (already wired up)

- ✅ Per-page `<title>` and `<meta description>`
- ✅ Canonical URLs
- ✅ Open Graph + Twitter card tags
- ✅ JSON-LD structured data (Organization on every page; SoftwareApplication on /, FAQPage on /pricing, BlogPosting on every post)
- ✅ Auto-generated `sitemap-index.xml` (Astro sitemap integration)
- ✅ `robots.txt` with sitemap reference + AI-bot opt-out
- ✅ RSS feed at `/rss.xml`
- ✅ Mobile-first responsive design
- ✅ Semantic HTML5 landmarks (`<header>`, `<main>`, `<nav>`, `<footer>`, `<article>`)
- ✅ Skip-to-content link for accessibility
- ✅ Pre-connected Google Fonts for fast LCP
- ✅ Tailwind CSS purging (only used classes ship)

After first deploy, submit `https://builderagent.io/sitemap-index.xml` in **Google Search Console** and **Bing Webmaster Tools** to accelerate indexing.

## Customizing

- **Brand colors** → `src/styles/global.css`, `@theme` block.
- **Fonts** → swap in `SeoHead.astro` (Google Fonts link) and `global.css` (`--font-display` / `--font-body` / `--font-mono`).
- **Navigation links** → `src/components/Header.astro` and `Footer.astro`.
- **Pricing tiers** → `src/pages/pricing.astro`, `tiers` array.
- **Use cases** → `src/pages/use-cases.astro`, `cases` array.
- **Blog posts** → drop new `.md` or `.mdx` files into `src/content/blog/`. Schema is in `src/content.config.ts`.

## Forms

The contact form on `/contact` posts to a placeholder Formspree endpoint. To activate:

1. Create a free form at [formspree.io](https://formspree.io).
2. In `src/pages/contact.astro`, replace `REPLACE-WITH-YOUR-FORMSPREE-ID` with your Formspree ID.

## License

Site code: MIT (yours to do whatever with).
Content: © BuilderAgent. All rights reserved.
