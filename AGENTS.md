# AGENTS.md — Shawn Mix Personal Site

Personal website for Shawn Mix — blog, digital garden (Obsidian notes), resume, and links hub. Built on a customized [Jekyll Garden](https://github.com/Jekyll-Garden/jekyll-garden.github.io) theme.

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

> macOS ships with Ruby 2.6. Always use Homebrew Ruby 3.2 at `/opt/homebrew/opt/ruby@3.2/bin/` for Jekyll 4.

---

## Architecture

### Single Layout Pattern

All pages share one layout: `_layouts/Post.html`. It branches using Liquid conditionals on `page.permalink` and `page.content-type`:

| Condition | Page type |
|---|---|
| `permalink: /` | Homepage — renders `pages/index.md` via `Content.html` |
| `permalink: /notes` | Notes index — search + feed |
| `permalink: /blog` | Blog index — post listing |
| `content-type: notes` | Individual note — back button + backlinks |
| `content-type: post` | Blog post — back button + date + read time |
| `content-type: static` | Static page (about, resume, etc.) |

### Key Files

| File | Purpose |
|---|---|
| `_config.yml` | Site config, feature toggles; menu is empty (nav is via landing page cards) |
| `_layouts/Post.html` | Universal layout; theme attribute set here |
| `_includes/Nav.html` | Top nav — square logo left, theme toggle right; all theme JS lives here |
| `_includes/Footer.html` | Empty spacer — no copyright, no credits |
| `_includes/Feed.html` | Notes feed list (`feed-container` wrapper) |
| `_includes/Backlinks.html` | Backlinks grid on note/post pages |
| `assets/css/style.css` | All styles — plain CSS, no Sass |
| `pages/index.md` | Landing page — name, bio, 2×2 card grid |
| `pages/about.md` | About page |
| `pages/resume.md` | Resume (placeholder, specialized layout planned) |
| `pages/notes.md` | Notes index |
| `pages/blog.md` | Blog index |
| `_notes/` | Digital garden notes (Obsidian-compatible, `[[wiki links]]` supported) |
| `_posts/` | Blog posts — filename must be `YYYY-MM-DD-title.md` |

### Collections

- **Notes**: `_notes/` — published at `/notes/:name`
- **Posts**: `_posts/` — published at `/blog/:title/`

---

## CSS Variable System

All values live in `:root` (light) and `[data-theme="dark"]` (dark) in `style.css`. Never use hardcoded values — always reference or add a variable.

### Spacing

| Variable | Value |
|---|---|
| `--space-xs` | `0.4rem` |
| `--space-sm` | `0.8rem` |
| `--space-md` | `1.2rem` |
| `--space-lg` | `2rem` |
| `--space-xl` | `3rem` |
| `--back-button-offset` | `8rem` |

### Type Scale

| Variable | Value | Usage |
|---|---|---|
| `--scale-xs` | `0.8rem` | Small labels |
| `--scale-sm` | `0.933rem` | Back button, captions |
| `--scale-meta` | `0.875rem` | Post metadata (date, read time) |
| `--scale-base` | `1rem` | Body text |
| `--scale-lg` | `1.2rem` | Subheadings |

### Font Weights

| Variable | Value |
|---|---|
| `--weight-light` | `300` |
| `--weight-medium` | `400` |
| `--weight-bold` | `600` |

Font: **Inter** (Google Fonts), loaded at weights 300/400/600. Loaded via `@import` in `style.css` only — no separate `<link>` tag in the layout.

### Line Heights

| Variable | Value | Usage |
|---|---|---|
| `--line-height` | `1.5` | Default — headings, code, search results |
| `--line-height-relaxed` | `1.6` | Blockquotes, list items |
| `--line-height-loose` | `1.7` | Body paragraphs |

### Colors — Catppuccin

| Variable | Dark (Mocha) | Light (Latte) |
|---|---|---|
| `--bg` | `#181825` Mantle | `#eff1f5` Base |
| `--bg2` | `#1e1e2e` Base | `#e6e9ef` Mantle |
| `--text` | `#cdd6f4` Text | `#4c4f69` Text |
| `--title` | `#ffffff` White | `#1e1e2e` Dark |
| `--brand` | `#45475a` Surface 1 | `#9ca0b0` Surface 1 |
| `--border` | `#313244` Surface 0 | `#ccd0da` Surface 0 |

Accent hover color (not a variable — used inline): `rgba(137, 180, 250, 0.22)` — Catppuccin Blue at low opacity.

---

## Design Conventions

- **Dark mode is default** — theme is set via inline `<script>` in `<head>` before first paint (prevents flash). JS reads `localStorage` and falls back to `'dark'`.
- **Theme toggle** — filled circle SVG, top-right nav. Click handler lives in `Nav.html`.
- **Navigation** — no hamburger menu. All navigation is via the landing page 2×2 card grid.
- **Links** — `color: var(--text)`, `text-decoration: underline` (1px), no color change on hover.
- **No footer content** — no colophon, credits, or copyright.
- **Max content width** — `48rem`, centered.

### Hover Behavior

| Element | Hover effect |
|---|---|
| Landing page cards | `rgba(137, 180, 250, 0.22)` blue tint + border stays visible |
| Backlinks grid items | Same blue tint |
| Notes/blog feed list items | None — no highlight |
| Back button | Opacity 0.7 → 1 |

### External Link Arrows

CSS `::after` on `a[href^="http"]` — theme-aware SVG stroke (`#4c4f69` light / `#cdd6f4` dark). Suppressed on: nav, footer, search, feed wrappers. On card grid: suppressed on `<a>` wrapper, applied to `h4::after` so the arrow appears beside the title, not after the description.

### Back Buttons

- Text: `← Back to Notes` / `← Back to Blog`
- Desktop (≥768px): `position: fixed; left: var(--back-button-offset); top: var(--back-button-offset)`
- Mobile: inline, above the title

### Blog Post Metadata

Rendered beneath `<h1>` on post pages:

```liquid
{{ page.date | date: "%b %-d, %Y" }} &middot; {{ read_mins }} min read
```

- Read time: `page.content | number_of_words | divided_by: site.reading_speed`, floored at 1. Speed configured in `_config.yml` (`reading_speed: 200` wpm)
- Style: `--scale-meta`, `--weight-light`, `opacity: 0.5`, class `.post-meta`

---

## Adding Content

### New blog post

File: `_posts/YYYY-MM-DD-title.md`

```yaml
---
title: "Post Title"
date: YYYY-MM-DD
feed: show
---
```

### New note (digital garden)

File: `_notes/Public/Note Title.md`

```yaml
---
title: "Note Title"
feed: show
date: YYYY-MM-DD
---
```

### New static page

File: `pages/slug.md`

```yaml
---
title: "Page Title"
layout: Post
content-type: "static"
permalink: /slug
---
```

---

## Future Work

- Design and implement a proper monogram/initials SVG logo to replace the placeholder square in the top-left nav
- Build a Links page (`/links`) as a specialized layout — similar to the Notes feed (no search), but each entry has a URL and a short description snippet; replaces the current external LinkTree redirect
- Add in a "credits" link bottom right like source repo - use for linking to people I owe credit to - career, inspiration, this page, etc
- Footer for connecting: simple outline logos (GitHub, LinkedIn, Buy Me a Coffee / PayPal), right-aligned
- Deployment config — GitHub Pages with custom domain `shawnmix.com` (remove Cloudflare redirect rule pointing shawnmix.com → shawnmix.info first)
- Real Obsidian notes sync

---

## References

- Catppuccin palette: https://catppuccin.com/palette/
- Design inspiration: https://hiran.in
- Inspiration source repo: https://github.com/hfactor/website
- Jekyll Garden theme: https://github.com/Jekyll-Garden/jekyll-garden.github.io
