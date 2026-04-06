# 📘 thapar25.github.io

[![GitHub Pages](https://img.shields.io/badge/GitHub-Pages-blue.svg)](https://pages.github.com/)
[![Powered by Jekyll](https://img.shields.io/badge/Powered%20by-Jekyll-lightgrey.svg)](https://jekyllrb.com/)

A knowledge base blog powered by Obsidian and Jekyll. Articles are drafted in Obsidian, converted to Markdown, and automatically published to GitHub Pages.

---

## ⚙️ Project Structure Overview

This site uses the Jekyll static site generator. All article content must be written as clean Markdown files and placed within the `_posts/` directory.

*   📂 `_posts/`: Contains all published articles. **New articles must go here.**
*   📄 `_config.yml`: Global site configuration (Title, Theme, etc.).
*   📂 `assets/`: Site-wide images, CSS, and JavaScript.
*   `.gitignore`: Crucially ignores the local Obsidian vault (`.obsidian/`) to keep the repository clean.

## ✍️ How to Write an Article (The Workflow)

The primary workflow revolves around the Obsidian export process.

1.  **Draft:** Write your article in Obsidian (or Notion).
2.  **Metadata:** Manually ensure the article's content starts with the Jekyll **YAML Front Matter** block at the very top of the Markdown file.
3.  **Clean:** Copy the fully formatted Markdown content.
4.  **Paste & Commit:** Paste the content into a new file in the local `_posts/` directory (e.g., `2024-05-28-new-article.md`).
5.  **Publish:** Commit the new file and push to GitHub. Jekyll handles the rest!

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