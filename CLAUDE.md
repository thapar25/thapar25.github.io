# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A personal knowledge base blog built with **Jekyll** and authored in **Obsidian**, hosted on **GitHub Pages**. Theme: Minima (with a planned migration to Chirpy noted in `_config.yml`).

## Common Commands

```bash
bundle install                  # Install gem dependencies
bundle exec jekyll serve        # Start dev server at http://127.0.0.1:4000
bundle exec jekyll build        # Build static site to _site/
```

## Architecture

- **`_posts/`** — Published blog posts. Files must be named `YYYY-MM-DD-title.md`.
- **`_posts/blog/`** — Obsidian vault directory (drafts authored here; `.obsidian/` config is gitignored).
- **`_config.yml`** — Site metadata, theme (`minima`), and plugins (`jekyll-feed`, `jekyll-sitemap`).
- **`_site/`** — Generated output; excluded from git.

## Post Front Matter

Every post in `_posts/` requires this YAML front matter:

```yaml
---
layout: post
title: "Post Title"
date: YYYY-MM-DD HH:MM:SS +0000
categories: [category1, category2]
tags: [tag1, tag2]
---
```

## Publishing Workflow

1. Write in Obsidian (`_posts/blog/`)
2. Add Jekyll front matter
3. Move to `_posts/` with `YYYY-MM-DD-title.md` naming
4. Commit and push — GitHub Pages builds automatically
