# BlankAstro

This is a bare-bones template of the Astro site running at
[charliekennedy.dev](https://charliekennedy.dev). It's the same underlying
architecture, cut down to just the parts anyone starting a personal site would
want: a blog and static content pages, no personal content attached.

Two content types are set up here, on purpose:

- **Blog posts** (`src/content/blog/`) — dated, tagged, and sorted newest-first
  on `/blog`. This shape fits anything you'd want in a chronological feed:
  updates, write-ups, devlogs.
- **Content pages** (`src/content/specifics/`) — undated, standalone pages like
  About or Contact. Nothing about them assumes a publish date or a place in a
  feed; they just render at their own URL.

Splitting them into two Astro content collections, each with its own schema,
means the frontmatter Astro type-checks is different for each: a blog post
without a `pubDate` is a build error, a content page isn't expected to have one
at all. Two different jobs, two different shapes.

On my own site, I built on top of this exact foundation and expanded it with a
games section, Supabase-backed accounts, leaderboards, and a likes system —
none of which is in this template. Start here, take it as far as you want.

## Architecture overview

Pure static Astro — no backend, no database, no auth. Everything is a build-time
render from markdown content collections.

```text
/
├── src/
│   ├── components/     # Card, Tag, Navigation, Footer, PageHeader, BackLink, BaseHead
│   ├── content/
│   │   ├── config.ts   # collection schemas — blog and specifics
│   │   ├── blog/       # blog posts (.md), empty by default
│   │   └── specifics/  # standalone content pages (.md)
│   ├── layouts/
│   │   └── MainLayout.astro   # <html> shell: BaseHead, Navigation, slot, Footer
│   ├── pages/
│   │   ├── index.astro                  # home page
│   │   ├── blog.astro                   # blog list
│   │   ├── blog/[...slug].astro         # blog post detail (handles draft posts)
│   │   └── specifics/[...slug].astro    # content page detail
│   └── styles/global.css
└── astro.config.mjs
```

`getCollection()` reads whichever `.md` files exist under `src/content/blog/`
and `src/content/specifics/` at build time; `getStaticPaths()` in each
`[...slug].astro` turns those into actual routes. Add a markdown file, get a page.

Deployment isn't included — no GitHub Actions workflow ships with this
template, since that choice is yours to make. If you do want GitHub Pages,
Astro's guide covers it end to end: https://docs.astro.build/en/guides/deploy/github/

---

# Astro Starter Kit: Minimal

*(This is the default readme Astro's own `minimal` template ships with —
left in place below, unedited.)*

```sh
npm create astro@latest -- --template minimal
```

> 🧑‍🚀 **Seasoned astronaut?** Delete this file. Have fun!

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
├── src/
│   └── pages/
│       └── index.astro
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 👀 Want to learn more?

Feel free to check [our documentation](https://docs.astro.build) or jump into our [Discord server](https://astro.build/chat).

---

## Template usage guide

### Adding a content page

Add a markdown file under `src/content/specifics/`, e.g. `src/content/specifics/about.md`:

```yaml
---
title: 'About'
description: 'Optional one-line summary'
---

Your page content here.
```

It appears at `/specifics/about`. Use this collection for anything that isn't a
dated post — About, Contact, whatever you need. Update the links in
`src/components/Navigation.astro` and `src/components/Footer.astro` to point at
your actual pages once you've added some (the included `example.md` is just a
placeholder — delete it once you've made your own).

### Adding a blog post

Add a markdown file under `src/content/blog/`, e.g. `src/content/blog/hello-world.md`:

```yaml
---
title: 'Hello World'
pubDate: 2026-01-01
description: 'Optional one-line summary'
author: 'Your Name'
tags: ["example"]
draft: false
---

Your post content here.
```

It appears at `/blog/hello-world`, listed on `/blog` sorted by `pubDate`
(newest first).

**Draft posts:** set `draft: true` and the post still shows up in the list and
is still clickable, but its page shows a "check back later" placeholder instead
of the real content. Useful for pushing work-in-progress posts to a public repo
without publishing them. Set it back to `false` (or delete the line — it
defaults to `false`) when the post is ready.

### Site metadata

- `astro.config.mjs` — set `site` to your actual domain (feeds canonical URLs).
- `src/components/BaseHead.astro` — default meta description, OG image path.
- `src/components/Footer.astro` — site name, tagline, links, copyright.
- `public/favicon.svg` — replace with your own icon.

---

Now it's yours; take it, break it, and have fun with it.
