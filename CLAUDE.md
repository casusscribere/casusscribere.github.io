# casusscribere.github.io — Agent Instructions

## Overview

This is a Jekyll-based personal/academic portfolio site for Kirk M. Lundblade, deployed via GitHub Pages at `www.kirklundblade.com`. It uses the **no-style-please** remote theme — a near-zero-CSS, monospace-typography theme focused on content. All content is written in Markdown and managed through Jekyll's conventions.

---

## Stack & Dependencies

| Layer | Technology |
|---|---|
| Static site generator | Jekyll ~3.9.0 |
| Theme | `riggraz/no-style-please` (remote, v0.4.7) |
| Markdown parser | `kramdown-parser-gfm` (GitHub Flavored Markdown) |
| Plugins | `jekyll-feed`, `jekyll-seo-tag` |
| Hosting | GitHub Pages (native Jekyll build, no Actions) |
| Custom domain | `www.kirklundblade.com` (CNAME file) |

**Do not add gems or plugins without checking GitHub Pages compatibility.** GitHub Pages only supports a specific allowlist of plugins — unsupported plugins will break the build silently.

---

## Repository Structure

```
/
├── _config.yml           # Master site configuration
├── _data/
│   └── menu.yml          # Navigation menu definition
├── _includes/            # Reusable template fragments (from theme)
│   ├── head.html
│   ├── back_link.html
│   ├── goat_counter.html
│   ├── menu_item.html
│   └── post_list.html
├── _layouts/             # Page templates
│   ├── default.html      # Base layout
│   ├── home.html         # Homepage (uses menu.yml)
│   ├── page.html         # Static pages
│   ├── post.html         # Blog posts and content entries
│   └── archive.html      # Category-filtered post listings
├── _posts/               # All content entries (date-prefixed .md files)
├── _sass/
│   └── no-style-please.scss  # Theme styles (~1KB)
├── assets/
│   ├── css/main.scss     # CSS entry point
│   └── js/               # Optional per-page JavaScript
├── index.md              # Homepage (layout: home)
├── about.md              # About page (layout: page)
├── archive.md            # Full post archive (layout: archive)
├── example2-archive.md   # Category-specific archive (layout: archive)
├── logo.png              # Favicon
└── CNAME                 # Custom domain
```

---

## Content Model

### Posts (`_posts/`)

All content — CV, publications, blog posts — lives in `_posts/` as date-prefixed Markdown files:

```
YYYY-MM-DD-slug-title.md
```

The `slug` front matter field overrides the URL. The permalink is `/:slug.html`.

#### Minimum front matter for a post:

```yaml
---
layout: post
---
```

#### All supported front matter fields:

```yaml
---
layout: post           # Required. Always "post" for _posts/ content.
title: "My Title"      # Optional. Derived from filename if omitted.
slug: my-url-slug      # Optional. Overrides URL; default is from filename.
category: publication  # Optional. Used for filtering (see Categories).
custom_js: mouse_coords # Optional. Loads /assets/js/<name>.js on this page.
---
```

### Static Pages (root-level `.md` files)

Root-level pages use either `page`, `home`, or `archive` layouts:

```yaml
---
layout: page
title: About
---
```

```yaml
---
layout: archive
title: Publications
which_category: publication   # Filters post list to this category
---
```

---

## Categories

Categories are free-form strings set in post front matter. Current categories in use:

| Category | Purpose |
|---|---|
| `publication` | Journal articles, conference papers, research outputs |
| `professional` | CV and professional profile content |
| `example` | Theme demo content (can be removed) |
| `example2` | Theme demo content (can be removed) |

To add a new category, simply use it in a post's `category:` field. To surface it in navigation or a dedicated archive page, also update `_data/menu.yml` and optionally create a new archive page.

---

## Navigation (`_data/menu.yml`)

The homepage menu is driven by `_data/menu.yml`. Edit this file to add/remove/reorder navigation items.

### Supported entry types:

**Direct link:**
```yaml
entries:
  - title: About
    url: about.html
```

**Post list filtered by category:**
```yaml
entries:
  - title: recent publications
    post_list:
      category: publication
      limit: 5                        # Optional: max posts to show
      show_more: true                 # Optional: add a "see more" link
      show_more_text: See all...
      show_more_url: publications-archive.html
```

**Nested entries:**
```yaml
entries:
  - title: Section Header
    entries:
      - title: Sub-item
        url: sub-item.html
```

---

## Adding Content

### Add a publication or post

1. Create `_posts/YYYY-MM-DD-descriptive-title.md`
2. Add front matter with at minimum `layout: post` and `category:`
3. Write content in GFM Markdown below the front matter delimiter

Example:
```yaml
---
layout: post
title: "Title of Paper"
category: publication
slug: title-of-paper
---

Abstract or introduction text here. Full content follows in Markdown.
```

### Add a static page

1. Create a `.md` file in the repository root
2. Use `layout: page` and add `title:`
3. Optionally link it from `_data/menu.yml`

### Add a category archive page

1. Create a `.md` file in the root (e.g., `publications.md`)
2. Use this front matter:

```yaml
---
layout: archive
title: Publications
which_category: publication
---
```

3. Add a menu entry in `_data/menu.yml` pointing to `publications.html`

---

## Removing Content

- **To remove a post**: Delete the file from `_posts/`. If it has a menu entry, remove that from `_data/menu.yml`.
- **To remove a page**: Delete the root `.md` file and remove any `menu.yml` references.
- **To remove a category**: Remove all posts using it, and remove any archive page + menu entry referencing it.

---

## Modifying the CV

The CV exists in two forms:
- **Web version**: `_posts/2024-12-05-curriculum-vitae.md` — category `professional`, linked from menu as `curriculum-vitae.html`
- **Word document**: `Lundblade_26_CV.docx` — tracked in git but not served by Jekyll

When updating the CV, update the markdown post. If the Word doc should also be updated, that is a separate manual step — the two are not linked.

---

## Styling

The theme deliberately uses ~1KB of CSS. Avoid adding heavy stylesheets or frameworks. The existing styles are in:
- `_sass/no-style-please.scss` — core theme styles
- `assets/css/main.scss` — imports the above

**Dark mode** is handled via the CSS `invert()` function; images that should not be inverted in dark mode need the class `.ioda`.

**Content width** is capped at 640px via `.w` wrapper — this is intentional.

Do not modify theme SCSS unless the change is minimal and intentional. Custom styles should be appended to `assets/css/main.scss` or a new imported partial.

---

## JavaScript

JavaScript is opt-in per page via front matter:

```yaml
custom_js: my_script   # loads /assets/js/my_script.js
```

Scripts in `/assets/js/` are only loaded on pages that declare them. There is no global JS bundle.

---

## Analytics

GoatCounter analytics are wired up in `_includes/goat_counter.html` but **disabled** — `site.goat_counter` is not set in `_config.yml`. To enable, add to `_config.yml`:

```yaml
goat_counter: https://YOUR_ACCOUNT.goatcounter.com/count
```

---

## Configuration (`_config.yml`)

Key settings and their effects:

```yaml
title: Kirk M. Lundblade        # Site title in <title> and homepage
author: Kirk Matthew Lundblade  # SEO and feed metadata
email: casus_scribere@gmail.com
url: https://casusscribere.github.io
baseurl: ""
permalink: /:slug.html          # URL structure for all posts
favicon: "logo.png"

remote_theme: riggraz/no-style-please

theme_config:
  appearance: "auto"            # "light", "dark", or "auto"
  back_home_text: ".."          # Text for the back-to-home link
  date_format: "%Y-%m-%d"       # Post date format
  show_description: false       # Show site description on homepage

plugins:
  - jekyll-feed
  - jekyll-seo-tag
```

---

## Deployment

- **No CI/CD workflow** — GitHub Pages builds the site natively on every push to `master`.
- **Build time**: typically under 30 seconds.
- **To preview locally**: requires Ruby, Bundler, and `bundle exec jekyll serve`.
- **Custom domain**: controlled by the `CNAME` file. Do not delete or modify this file unless changing the domain.

---

## Conventions to Follow

1. **All content goes in `_posts/`** with date-prefixed filenames — even non-blog content like the CV.
2. **Use `slug:` in front matter** to control URLs cleanly, independent of the filename date prefix.
3. **Categories are the content taxonomy** — use them consistently; do not mix plurals/singulars (`publication` not `publications`).
4. **Navigation is manual** — adding a post does not automatically add it to the menu. Update `_data/menu.yml` deliberately.
5. **No unnecessary files** — avoid committing `.docx`, generated files, or binary assets unless they serve a clear purpose.
6. **GFM Markdown** — the parser is `kramdown-parser-gfm`; GitHub Flavored Markdown features (tables, fenced code blocks, task lists) are supported.
7. **Keep front matter minimal** — only include fields that are actually used.
