# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

Landing page for **FetchPosts** — a native macOS app that lets users download their LinkedIn post history and engagement metrics. The site is deployed at `fetchposts.com` via GitHub Pages.

## Stack

- **Jekyll** (static site generator) with the `github-pages` gem
- **Tailwind CSS** loaded via CDN (`https://cdn.tailwindcss.com`) — no build step required
- **Freemius** for checkout (`checkout.freemius.com`)
- **Lemon Squeezy** JS included in layout footer (legacy, may be unused)
- Fonts: Inter (body) + Space Grotesk (headings), Material Symbols Outlined icons

## Development commands

```bash
# Install dependencies
bundle install

# Run local dev server (auto-reloads on changes)
bundle exec jekyll serve

# Build to _site/
bundle exec jekyll build
```

The site runs at `http://localhost:4000` by default.

## Project structure

- `index.html` — main landing page (self-contained HTML with inline Tailwind config; does NOT use a layout)
- `_layouts/default.html` — shared layout used by blog and static pages; contains nav, footer, Lemon Squeezy script
- `_layouts/post.html` — wraps `default.html`; renders post title, date, image, and Markdown body
- `_posts/` — Jekyll blog posts in Markdown with front matter (`title`, `description`, `date`, `image`)
- `blog/index.html` — blog listing page using `{% for post in site.posts %}`
- `privacy-policy.html`, `terms-of-service.html` — static legal pages using `default` layout
- `assets/` — images and app screenshots
- `_config.yml` — site title, URL, plugins (`jekyll-seo-tag`, `jekyll-sitemap`)

## Key design details

- Color palette mirrors LinkedIn: primary `#0A66C2`, dark surface `#1D2226`, light bg `#F3F2EF`
- Dark mode via Tailwind's `class` strategy (toggled by adding/removing `dark` class on `<html>`)
- The Tailwind config is duplicated between `index.html` and `_layouts/default.html` — keep them in sync when changing theme tokens
- `index.html` is standalone (no Jekyll layout) and contains the full nav/footer inline

## Adding a blog post

Create `_posts/YYYY-MM-DD-slug.md` with this front matter:

```yaml
---
layout: post
title: "Post title"
description: "Short description shown in listing and meta tags"
date: YYYY-MM-DD
categories: [analytics, guide]
image: /assets/images/filename.png
---
```

## Deployment

Deployed automatically via GitHub Pages on push to `main`. The `CNAME` file sets the custom domain to `fetchposts.com`.
