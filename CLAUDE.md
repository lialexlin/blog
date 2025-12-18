# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A minimalist personal blog built with Jekyll, deployed to GitHub Pages at `https://lialexlin.github.io/blog`.

## Architecture

- **Jekyll static site** - GitHub Pages runs Jekyll automatically, no local build required
- **Markdown articles** - Place `.md` files at root with frontmatter; they become pages at `/:slug`
- **Two layouts**: `_layouts/default.html` (base), `_layouts/post.html` (articles)
- **Single stylesheet**: `styles.css` with DM Sans font from Google Fonts

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

- Use `N\.` (escaped period) for numbered lists to prevent Markdown from resetting numbering after blockquotes
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
