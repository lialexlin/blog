---
name: blog-post
description: Add, edit, translate or preview a post on Alex's Jekyll blog. Use when publishing a new article, moving a note out of the Obsidian vault onto the blog, adding or updating the Chinese mirror under zh/, or running the site locally to check how a draft renders.
---

# Publishing to the blog

## New post

Create `kebab-case-title.md` at the repo root — the filename becomes the URL slug, so choose it as the permanent link. Frontmatter:

```yaml
---
layout: post
title: Article Title
date: YYYY-MM-DD
---
```

Optional: `wip: true` files it under Work in progress, `index: false` keeps it off every listing, `hide_toc: true` drops the table of contents. Nothing else needs touching — `index.html` builds the listings, counts and hero stat from frontmatter.

Chinese version: same filename under `zh/`, plus `lang: zh`.

## Publishing from the Obsidian vault

Vault syntax does not survive Jekyll. Convert `[[wiki links]]` to `[text]({{ 'slug' | relative_url }})`, strip vault-only frontmatter and dataview blocks, and check the result renders before committing. Commit the article and its image assets only; leave unrelated working-tree changes alone.

## Markdown quirks

- Escape numbered lists as `N\.` **only** when a blockquote interrupts the list — an interruption resets Markdown numbering. Uninterrupted lists use plain `N.`.
- Blank line before every section header, or it will not render as one.
- Blockquotes carry answers in the Q&A posts; that is a convention, not a rendering requirement.

## Preview

`bundle exec jekyll serve` (first time on a machine: `bundle install`, with Ruby 3.x from Homebrew rather than the macOS system Ruby). Live-reloads at port 4000. `python3 -m http.server 8000` serves the raw files with no Jekyll processing, which is enough for a CSS check and nothing else.

Push to `main` deploys. There is no staging site, so a broken layout is live until the next push.
