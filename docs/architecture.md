# Architecture

Astro 5 static site — no server, no runtime JS. Builds to plain HTML/CSS in `dist/`.

## Stack

| Layer | Tool |
|---|---|
| Framework | [Astro 5](https://astro.build) — file-based routing, zero JS by default |
| Styling | [Tailwind v4](https://tailwindcss.com) via `@tailwindcss/vite` |
| Prose | `@tailwindcss/typography` — styles Markdown-rendered HTML |
| Content | Astro Content Collections (Content Layer API) |
| Images | Astro `<Image>` — resizes and converts to WebP at build time |

## Directory structure

```
src/
├── assets/          # images (processed by Astro <Image>)
├── content/
│   └── blog/        # .md post files — filename = URL slug
├── content.config.ts  # blog collection schema
├── layouts/
│   ├── BaseLayout.astro      # HTML shell, nav, footer
│   └── BlogPostLayout.astro  # post header + prose wrapper
├── pages/
│   ├── index.astro           # /
│   └── blog/
│       ├── index.astro       # /blog
│       └── [id].astro        # /blog/:slug
└── styles/
    └── global.css   # Tailwind + typography plugin imports
public/
└── CNAME            # custom domain for GitHub Pages
.github/workflows/
└── deploy.yml       # build + deploy on push to main
```

## Blog post schema

Defined in `src/content.config.ts`:

```ts
title: z.string()
description: z.string()
pubDate: z.coerce.date()       // accepts "2024-01-15" strings
updatedDate: z.coerce.date().optional()
tags: z.array(z.string()).default([])
draft: z.boolean().default(false)
```
