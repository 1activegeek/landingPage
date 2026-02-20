# AGENTS.md — Shawn Mix Personal Site

This file provides guidelines for AI agents working in this Jekyll repository.

## Project Overview

Personal website for Shawn Mix — a blog, digital garden (Obsidian notes), resume landing page, and links hub. Built on a customized [Jekyll Garden](https://github.com/Jekyll-Garden/jekyll-garden.github.io) theme.

## Commands

```bash
# Install dependencies
bundle install

# Run local dev server
export PATH="/opt/homebrew/opt/ruby@3.2/bin:$PATH"
bundle exec jekyll serve

# Build static site
bundle exec jekyll build
```

> **Note:** macOS ships with Ruby 2.6. Use the Homebrew Ruby 3.2 at `/opt/homebrew/opt/ruby@3.2/bin/` for Jekyll 4.

## Architecture

### Single Layout Pattern
All pages use one layout: `_layouts/Post.html`. It branches via Liquid conditionals on `page.permalink` and `page.content-type`:
- `permalink: /` — Homepage (renders `pages/index.md` content when `preferences.homepage.enabled: true`)
- `permalink: /notes` — Notes index (search + feed)
- `permalink: /blog` — Blog index (post listing)
- `content-type: notes` — Individual note
- `content-type: post` — Blog post
- `content-type: static` — Static page (about, resume, etc.)

### Key Files

| File | Purpose |
|---|---|
| `_config.yml` | Site config, feature toggles, menu (empty — nav is via landing page cards) |
| `_layouts/Post.html` | Universal layout — `data-theme="dark"` set here for default dark mode |
| `_includes/Nav.html` | Top nav — logo left, dark mode toggle right; all theme JS lives here |
| `_includes/Footer.html` | Minimal empty footer (no copyright, no credits) |
| `assets/css/style.css` | All styles — plain CSS, no Sass preprocessor |
| `pages/index.md` | Landing page — name, bio, 4-card grid |
| `pages/about.md` | About page |
| `pages/resume.md` | Resume placeholder (will become specialized layout) |
| `pages/notes.md` | Notes index page |
| `pages/blog.md` | Blog index page |
| `_notes/` | Digital garden notes (Obsidian-compatible, wiki links supported) |
| `_posts/` | Blog posts (date-prefixed, e.g., `2024-01-15-title.md`) |

### Collections
- **Notes**: `_notes/` — published at `/notes/:name`, support `[[wiki links]]`
- **Posts**: `_posts/` — published at `/blog/:title/`

## Color Scheme — Catppuccin

| Mode | Variable | Value | Color Name |
|---|---|---|---|
| Dark (default) | `--bg` | `#181825` | Mocha Mantle |
| Dark | `--bg2` | `#1e1e2e` | Mocha Base |
| Dark | `--text` | `#cdd6f4` | Mocha Text |
| Dark | `--title` | `#ffffff` | White |
| Dark | `--brand` | `#45475a` | Mocha Surface 1 |
| Dark | `--border` | `#313244` | Mocha Surface 0 |
| Light | `--bg` | `#eff1f5` | Latte Base |
| Light | `--bg2` | `#e6e9ef` | Latte Mantle |
| Light | `--text` | `#4c4f69` | Latte Text |
| Light | `--title` | `#1e1e2e` | Dark |
| Light | `--brand` | `#9ca0b0` | Latte Surface 1 |
| Light | `--border` | `#ccd0da` | Latte Surface 0 |

All colors are CSS custom properties in `:root` (light) and `[data-theme="dark"]` (dark) in `assets/css/style.css`.

## Design Conventions

- **Dark mode is default** — `data-theme="dark"` on `<html>` in `Post.html`; JS defaults to dark when no localStorage preference exists
- **Dark mode toggle** — top-right of nav bar (in `Nav.html`); shows sun icon in dark, moon in light
- **Navigation** — no hamburger menu; users navigate via the landing page card grid
- **Links** — same color as body text (`var(--text)`), thin 1px underline, no color change on hover
- **No colophon, no credits, no copyright footer**
- **Font** — Inter (Google Fonts), 15px base
- **Max content width** — 48rem centered

## Landing Page Cards

The 4-card grid on `pages/index.md`:
1. **Notes** → `/notes`
2. **Resume** → `/resume`
3. **Blog** → `/blog`
4. **Links** → `http://1activegeek.com/linkfree/` (external)

## Adding Content

### New note (digital garden):
Place a `.md` file in `_notes/` with front matter:
```yaml
---
title: "Note Title"
feed: show
date: 2024-01-15
---
```

### New blog post:
Place a `.md` file in `_posts/` named `YYYY-MM-DD-title.md` with front matter:
```yaml
---
title: "Post Title"
date: 2024-01-15
---
```

### New static page:
Place a `.md` file in `pages/` with front matter:
```yaml
---
title: "Page Title"
layout: Post
content-type: "static"
permalink: /page-slug
---
```

## Future Work

- Migrate old blog posts from separate Jekyll repo
- Profile photo at `/assets/img/profile.jpg`
- Custom resume layout (specialized page type)
- Deployment config (GitHub Pages / Cloudflare Pages)
- Bring in LinkTree-style page as a specialized layout
- Real Obsidian notes sync
- Enhance `/blog/` page to show dates/read times
- Add teaser snippets for blog posts like https://nichehunt.app/blog
- Footer for connecting (simple outline logos for popular links: github, linkedin, buy me a coffee/paypal with coffee logo) all right aligned

## References
Catppuccin Color Palette: https://catppuccin.com/palette/
Inspiration Source: https://hiran.in 
Source Repo: https://github.com/hfactor/website
Jekyll Garden Theme: https://github.com/Jekyll-Garden/jekyll-garden.github.io/
