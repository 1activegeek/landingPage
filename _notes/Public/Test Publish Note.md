---
date: '2026-02-22'
feed: show
tags:
- test
- technology
title: Pipeline Test Note
---

# Pipeline Test Note

This is a test note to verify the Obsidian → Jekyll sync pipeline is working correctly.

## What This Tests

- Frontmatter transformation (Obsidian fields stripped, Jekyll fields set)
- Content passes through correctly
- `[[Wikilinks]]` are preserved as-is
- The note appears in `_notes/Public/` in the landing page repo

## Sample Content

Here is some sample markdown content:

- Bullet point one
- Bullet point two
- Bullet point three

> A blockquote to test formatting

```javascript
// A code block
const hello = "world";
```

If this note appears on shawnmix.com, the pipeline is working.