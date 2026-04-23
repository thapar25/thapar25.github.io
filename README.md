# 📘 thapar25.github.io

[![GitHub Pages](https://img.shields.io/badge/GitHub-Pages-blue.svg)](https://pages.github.com/)
[![Powered by Jekyll](https://img.shields.io/badge/Powered%20by-Jekyll-lightgrey.svg)](https://jekyllrb.com/)

A knowledge base blog powered by Obsidian and Jekyll. Articles are drafted in Obsidian, converted to Markdown, and automatically published to GitHub Pages.

[![Deploy](https://github.com/thapar25/thapar25.github.io/actions/workflows/deploy.yaml/badge.svg)](https://github.com/thapar25/thapar25.github.io/actions/workflows/deploy.yaml)

---

## ⚙️ Project Structure Overview

This site uses the Jekyll static site generator. All article content must be written as clean Markdown files and placed within the `_posts/` directory.

*   📂 `_posts/`: Contains all published articles. **New articles must go here.**
*   📄 `_config.yml`: Global site configuration (Title, Theme, etc.).
*   📂 `assets/`: Site-wide images, CSS, and JavaScript.
*   `.gitignore`: Crucially ignores the local Obsidian vault (`.obsidian/`) to keep the repository clean.

## ✍️ How to Write an Article (The Workflow)

Articles are written directly in Obsidian inside `_posts/blog/` — the vault root. No copy-paste step needed.

1.  **Draft:** Write your article in Obsidian inside `_posts/blog/`.
2.  **Metadata:** Add the Jekyll YAML Front Matter block at the top of the file.
3.  **Link:** Use `[[filename|display text]]` wikilinks to connect related posts — they render as real links on the site and appear as edges in Obsidian's Graph View.
4.  **Publish:** Commit and push — GitHub Actions builds automatically.

### 🔗 Wikilinks & Graph View

This site uses [`jekyll-wikilinks`](https://github.com/manunamz/jekyll-wikilinks) to convert Obsidian's native `[[wikilink]]` syntax into real HTML links at build time.

- **In Obsidian:** `[[2026-04-19-luna-backend|The Underdog Stack]]` renders as a clickable link and draws an edge in Graph View.
- **On the site:** The same link becomes `<a href="/2026/04/19/luna-backend.html">The Underdog Stack</a>`.
- **Backlinks:** Each post automatically shows a "Linked mentions" section listing every post that links to it — mirroring Obsidian's backlinks panel.

The graph you see in Obsidian is the exact same link structure search engines crawl.

### ⭐️ Required Front Matter Format

Every file in `_posts/` **must** begin with this block, adjusting the details below:

```yaml
---
layout: post
title: "Article Title Goes Here"
date: 2024-05-28 12:00:00 -0500
categories: [category1, category2]
tags: [tag1, tag2]
description: "2-3 sentence summary for search results and social sharing"
---
```

The `description` field is essential for SEO—it appears in search engine results and social media previews.

> ⚠️ **Note:** Obsidian's `.obsidian` folder is correctly added to `.gitignore` and should not be committed.

## 🚀 Local Setup & Running

If you need to test the site locally:

1.  **Prerequisites:** Ensure you have Ruby and the Jekyll gem installed.
2.  **Installation:** `bundle install`
3.  **Serve:** `bundle exec jekyll serve`
4.  Visit `http://127.0.0.1:4000` in your browser.

## 🔍 SEO Features

The site is optimized for search engines:

- **Meta Tags** — Auto-generated from post descriptions via `jekyll-seo-tag`
- **Sitemap** — Auto-generated at `/sitemap.xml` for search engine discovery
- **Robots.txt** — Configured to guide crawler behavior
- **Open Graph Tags** — Social media preview optimization
- **RSS Feed** — Content distribution via `/feed.xml`
- **Google Analytics** — Traffic monitoring and insights

For best SEO results, always include a meaningful `description` in your post front matter.

## 📖 Built With

*   [Obsidian](https://obsidian.md/) - Writing Environment
*   [Jekyll](https://jekyllrb.com/) - Static Site Generator
*   [GitHub Pages](https://pages.github.com/) - Hosting
