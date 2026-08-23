# blog

Jekyll site, published by GitHub Pages on push to `main`. Stack and layouts read from `_config.yml`, `Gemfile`, `_layouts/`.

- Everything committed at the repo root is served publicly, this file included. Nothing private belongs here.
- `index.html` generates every listing, count and the hero stat from page frontmatter. Never hand-edit them. `wip: true` files a post under Work in progress; `index: false` hides it entirely.
- A root filename is the URL slug. Renaming a published post breaks its inbound links.
- `styles.css` mirrors the lialexlin design system (claude.ai/design project `019dd1ca-a689-7f36-a153-a15ba8d705f5`, the source of truth). Re-sync from there; never fork token values into this repo.
- `zh/` is the Chinese mirror with its own `index.html`; `lang: zh` frontmatter switches nav labels and loads Noto Sans TC.

Writing, publishing, or previewing a post: skill `blog-post`.
