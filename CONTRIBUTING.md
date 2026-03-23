# Contributing to CS Resources

Thanks for your interest in contributing! This document covers how the project works and how to get set up locally.

---

## How the Site Works

This repo contains a single `README.md` which serves as the index page of the site. It is rendered by [Jekyll](https://jekyllrb.com/) via GitHub Pages and published at [cs-resources.badrchoubai.dev](https://cs-resources.badrchoubai.dev).

Because `README.md` is the site's homepage, changes to it are immediately reflected on the live site after merging to `main`. Keep this in mind when editing.

Additional content is organized into Jekyll collections. Each collection is a top-level folder prefixed with `_` (e.g. `_rcc/`, `_cs1030/`) and must be declared in `_config.yml` to be rendered by Jekyll.

---

## Local Development

### Prerequisites

- Ruby
- Bundler (`gem install bundler`)

### Setup

Install dependencies:

```bash
bundle install
```

Start the local development server:

```bash
bundle exec jekyll serve --livereload
```

The site will be available at `http://localhost:4000`. Changes to `README.md` or any file in `_layouts/` or `_includes/` will reload the browser automatically.

### Project Structure

```
.
├── README.md                        # Site content (index page)
├── _config.yml                      # Jekyll configuration
├── _layouts/
│   └── default.html                 # Main layout template
├── _includes/                       # Reusable HTML partials
├── _roadrunner-connect/             # Collection: Roadrunner Connect Club
│   ├── index.md                     # Served at /roadrunner-connect/
│   └── workshop-git.md              # Served at /roadrunner-connect/workshop-git/
├── assets/                          # Static assets (images, CSS)
├── Gemfile                          # Ruby dependencies
└── CONTRIBUTING.md                  # This file
```

---

## Making Changes

### Editing Content

All site content lives in `README.md`. When editing:

- Keep the list-based format for resources — avoid adding tables as they don't render well on mobile
- Follow the existing structure: a bold category heading (`**Category**`) above a list of resources
- Each resource should follow the pattern: `[**Title**](url) — Brief description.`

### Adding a New Collection

Collections are used for topic-specific content like course notes or workshop writeups. To add one:

1. Create a top-level folder prefixed with `_`, e.g. `_cs1030/`
2. Register it in `_config.yml` under `collections`:

```yaml
collections:
  roadrunner-connect:
    output: true
    permalink: /roadrunner-connect/:name/
  cs1030:
    output: true
    permalink: /cs1030/:name/
```

3. Add an `index.md` for the collection's landing page with an explicit permalink in its frontmatter:

```yaml
---
title: CS 1030
permalink: /cs1030/
---
```

The explicit permalink is required because Jekyll would otherwise resolve `index.md` to `/cs1030/index/` rather than `/cs1030/`.

4. Add any additional pages alongside `index.md`. They will be served at `/cs1030/:name/` automatically based on their filename, with no extra frontmatter needed beyond a title.

**Gotchas:**

- `output: true` is required — without it Jekyll silently skips rendering the collection entirely
- Do not add a top-level `layout:` key to `_config.yml` — the layout is already applied globally via `defaults`. A stray top-level `layout:` key is ignored by Jekyll and just causes confusion
- Links between collection pages should use relative paths (e.g. `./workshop-git/`) rather than absolute paths, as absolute paths can break depending on whether `baseurl` is set

### Editing the Layout

The layout lives in `_layouts/default.html`. It uses [Pico CSS](https://picocss.com/) for styling. When editing the layout:

- Keep the `<main class="container" id="content">` structure intact — the JS that handles table scrolling depends on `#content`
- Reusable partials go in `_includes/` and can be pulled in with `{% include filename.html %}`

---

## Submitting Changes

1. Fork the repository
2. Create a branch (`git checkout -b my-change`)
3. Make your changes and test locally with `bundle exec jekyll serve`
4. Open a pull request against `main` with a short description of what you changed and why
