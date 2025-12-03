# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A minimalist personal blog built with Jekyll, deployed to GitHub Pages at `https://lialexlin.github.io/blog`.

## Architecture

- **Jekyll static site** - GitHub Pages runs Jekyll automatically, no local build required
- **Markdown articles** - Place `.md` files at root with frontmatter; they become pages at `/:slug`
- **Two layouts**: `_layouts/default.html` (base), `_layouts/post.html` (articles)
- **Single stylesheet**: `styles.css` with Urbanist font from Google Fonts

## Adding New Articles

1. Create `article-name.md` at repository root
2. Add frontmatter:
   ```yaml
   ---
   layout: post
   title: Article Title
   date: YYYY-MM-DD
   ---
   ```
3. Add entry to `index.html` manually

## Markdown Formatting Notes

- Use `N\.` (escaped period) for numbered lists to prevent Markdown from resetting numbering after blockquotes
- Add blank lines before section headers for proper rendering
- Blockquotes (`>`) are used for answers/responses in Q&A format

## Local Development

```bash
# Serve locally (requires Jekyll installed)
bundle exec jekyll serve

# Or use Python for quick static preview (no Jekyll processing)
python3 -m http.server 8000
```

## Deployment

Push to `main` branch - GitHub Actions deploys automatically to GitHub Pages.
