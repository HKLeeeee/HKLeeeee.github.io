# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Local dev server (http://localhost:4000)
bundle exec jekyll serve

# Production build
bundle exec jekyll build

# New post via jekyll-compose
bundle exec jekyll post "Post Title"
bundle exec jekyll draft "Draft Title"
```

## Architecture

Jekyll blog using [Hydejack 9.1](https://hydejack.com/) theme. Deployed via GitHub Pages (main branch) or Netlify.

**Key directories:**
- `_posts/` — blog posts, organized in subdirectories by category (e.g., `친절한SQL튜닝/`)
- `_featured_categories/` — category definition pages
- `_featured_tags/` — tag definition pages
- `_layouts/` — custom layout overrides: `search.html`, `sidebar.html`, `my-head.html`, `my-body.html`
- `_data/authors.yml` — author profile (name, bio, social links, picture)
- `_config.yml` — site-wide settings, menu, plugins

**Post front matter pattern:**
```yaml
layout: post
title: Post Title
description: >
  ~160 char description
sitemap: true
categories: CategoryName
tags: [tag1, tag2]
```

**Math rendering:** KaTeX via `kramdown-math-katex` gem. Not supported on GitHub Pages — use Netlify for math-heavy posts.

**Search:** `simple-jekyll-search` (npm package), wired into `_layouts/search.html`.

## Deployment

- GitHub Pages: push to `main` → auto-deploy (no KaTeX math support)
- Netlify: `jekyll build` → `_site/`, uses `netlify.toml` config (`RUBY_VERSION = "2.7.1"`)

## Content Categories

Current categories: `AI`, `computer`, `example`, `SQLTuning` (친절한SQL튜닝 book study)
