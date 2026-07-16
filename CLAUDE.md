# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A minimalist personal blog built with Jekyll, deployed to GitHub Pages at `https://lialexlin.github.io/blog`.

## Architecture

- **Jekyll static site** - GitHub Pages runs Jekyll automatically, no local build required
- **Markdown articles** - Place `.md` files at root with frontmatter; they become pages at `/:slug`
- **Two layouts**: `_layouts/default.html` (site chrome: sticky nav + footer), `_layouts/post.html` (nests in default; adds TOC, reading progress, article shell)
- **Single stylesheet**: `styles.css` — the **lialexlin design system** (DM Sans + DM Mono, navy `#1c2b4a` accent). Tokens and prose styles are pulled from the claude.ai/design project `019dd1ca-a689-7f36-a153-a15ba8d705f5` (source of truth; local skill mirror: `~/.claude/skills/lialexlin-design/`). Re-sync via DesignSync when the design project changes; don't fork token values here.
- **Chinese mirror**: `zh/` holds translated articles + its own `index.html` (`lang: zh` frontmatter switches nav labels and loads Noto Sans TC)

## Adding New Articles

1. Create `article-name.md` at repository root using **kebab-case** (e.g., `book-of-the-year-naval-ravikant.md`). The filename becomes the URL slug.
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

- Use `N\.` (escaped period) for numbered lists only when blockquotes interrupt the list (which resets Markdown numbering). For uninterrupted lists, use standard `N.` syntax
- Add blank lines before section headers for proper rendering
- Blockquotes (`>`) are used for answers/responses in Q&A format

## Local Development

### Prerequisites

**macOS:**
```bash
# Ruby comes pre-installed, but install a newer version via Homebrew
brew install ruby
echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

**Windows:**
```bash
# Install Ruby via RubyInstaller: https://rubyinstaller.org/
# Download "Ruby+Devkit" version, run installer with default options
# Restart terminal after installation
```

Verify installation:
```bash
ruby -v    # Should show 3.x
gem -v     # Should show gem version
```

### First-time Setup

```bash
# Install Bundler (Ruby package manager)
gem install bundler

# Install project dependencies
bundle install
```

### Running Locally

```bash
# Start Jekyll dev server with live reload
bundle exec jekyll serve

# Opens at http://localhost:4000
# Auto-rebuilds on file changes
```

Alternative (no Jekyll processing, static files only):
```bash
python3 -m http.server 8000
```

## Deployment

Push to `main` branch - GitHub Actions deploys automatically to GitHub Pages.
