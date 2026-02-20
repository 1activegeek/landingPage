# Shawn Mix — Personal Site

Personal website, blog, and digital garden for Shawn Mix. Built on a customized [Jekyll Garden](https://github.com/Jekyll-Garden/jekyll-garden.github.io) theme.

## What's Here

- **Landing page** — About me summary with links to major sections
- **Blog** — Long-form writing at `/blog`
- **Notes** — Digital garden of Obsidian notes at `/notes`
- **Resume** — Professional background at `/resume`
- **Links** — External links hub at [1activegeek.com/linkfree](http://1activegeek.com/linkfree/)

## Running Locally

Requires Ruby 3.x. On macOS, install via Homebrew: `brew install ruby@3.2`

```bash
export PATH="/opt/homebrew/opt/ruby@3.2/bin:$PATH"
bundle install
bundle exec jekyll serve
```

Site will be available at `http://localhost:4000`.

## Tech Stack

- [Jekyll](https://jekyllrb.com/) 4.x — static site generator
- [Jekyll Garden](https://github.com/Jekyll-Garden/jekyll-garden.github.io) — base theme (heavily customized)
- [Catppuccin](https://catppuccin.com/) — color scheme (Mocha dark / Latte light)
- [Obsidian](https://obsidian.md/) — note-taking (synced to `_notes/`)
- Plain CSS — no preprocessors or build tools beyond Jekyll

## License

This repository is released into the public domain under the [Unlicense](LICENSE).
