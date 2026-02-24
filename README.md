# Purple Haze

A Zola theme with Catppuccin colors built for developer tool landing pages and documentation. Four modes, dark/light theming, full-text search, and keyboard navigation out of the box.

**Live examples:** [arcanist.sh](https://arcanist.sh) (product) &middot; [hx docs](https://arcanist.sh/hx/) (docs) &middot; [bhc docs](https://arcanist.sh/bhc/) (docs)

## Quick start

```bash
cd your-zola-site
git submodule add https://github.com/arcanist-sh/purple-haze themes/purple-haze
```

```toml
# config.toml
theme = "purple-haze"

[extra]
mode = "product"  # "product" | "docs" | "blog" | "site"
```

## Modes

### Product

Marketing landing pages for developer tools. Hero section, feature grid, install command, testimonials, benchmarks, footer links.

```toml
[extra]
mode = "product"

[extra.product]
tagline = "Next-generation Haskell tooling"
subtitle = "Built in Rust for maximum performance."
install_command = "curl -fsSL https://example.com/install.sh | sh"

[[extra.product.features]]
icon = "<svg>...</svg>"
title = "Fast builds"
description = "5.6x faster cold builds than alternatives."

[[extra.product.footer_links]]
title = "Resources"
[[extra.product.footer_links.links]]
text = "Docs"
url = "/docs/"
```

### Docs

Documentation with a collapsible, resizable sidebar, table of contents, previous/next navigation, version picker, and edit-on-GitHub links.

```toml
[extra]
mode = "docs"

[extra.docs]
versioned = true
default_version = "latest"
versions = [
  { version = "latest", url = "https://docs.example.com" },
  { version = "0.5.x", url = "https://docs.example.com/0.5" },
]
edit_url = "https://github.com/org/repo/tree/main/content"
```

### Blog

Article listings with cards, tags, search, and pagination.

```toml
[extra]
mode = "blog"
```

### Site

General-purpose homepage with avatar, bio, social links, and recent posts.

```toml
[extra]
mode = "site"
```

## Configuration

### SEO and metadata

```toml
[extra]
author = "Your Name"
author_type = "Organization"  # or "Person"
keywords = "haskell, tooling, rust"
og_image = "img/og-image.png"
og_image_width = 1200
og_image_height = 630
og_image_alt = "Project description"
twitter_site = "@handle"
sameAs = ["https://github.com/org", "https://x.com/handle"]
```

The theme generates JSON-LD structured data automatically: `WebSite`, `Organization`/`Person`, `WebPage`, `TechArticle` (for pages), and `BreadcrumbList` (for nested content). Product and docs modes add `SoftwareApplication` and `FAQPage` schemas.

Open Graph and Twitter Card meta tags are generated from page frontmatter with fallback to site config.

### Navigation

```toml
[[extra.nav_links]]
name = "Docs"
url = "/docs/"

[[extra.nav_links]]
name = "GitHub"
url = "https://github.com/org/repo"
external = true
```

### Social links

```toml
[extra.social]
github = "https://github.com/org"
twitter = "https://x.com/handle"
discord = "https://discord.gg/invite"
mastodon = "https://fosstodon.org/@handle"
```

### Header and layout

```toml
[extra]
fixed_header = true       # Sticky header (default for product/docs)
show_theme_toggle = true  # Show light/dark/auto toggle
```

### CTAs (product mode)

```toml
[extra.cta_primary]
text = "Get Started"
url = "/docs/"

[extra.cta_secondary]
text = "View on GitHub"
url = "https://github.com/org/repo"
```

### Search

Enable Zola's built-in search index:

```toml
build_search_index = true
```

The theme provides a search overlay triggered by `/` or `Cmd+K` / `Ctrl+K` with keyboard navigation (arrow keys, Enter to select, Escape to close).

## Features

### Dark / light / auto

Three-way theme toggle persisted to `localStorage`. Respects `prefers-color-scheme` in auto mode. No flash of unstyled content — the theme script runs synchronously in `<head>`.

### Catppuccin colors

Full [Catppuccin](https://catppuccin.com) palette exposed as CSS custom properties:

| Role | Dark (Mocha) | Light (Latte) |
|------|-------------|---------------|
| Primary | `#cba6f7` mauve | `#8839ef` mauve |
| Background | `#1e1e2e` base | `#eff1f5` base |
| Text | `#cdd6f4` text | `#4c4f69` text |
| Links | `#cba6f7` mauve | `#7287fd` lavender |
| Code | `#f9e2af` yellow | `#df8e1d` yellow |
| Success | `#a6e3a1` green | `#40a02b` green |
| Error | `#f38ba8` red | `#d20f39` red |

### Typography

- **Geist Sans** — body text (variable weight, loaded from CDN)
- **Geist Mono** — code blocks (variable weight)
- **Clash Display** — headlines and brand text (from Fontshare)

### Code blocks

Syntax highlighting with Catppuccin themes (light and dark). Language labels, one-click copy button with visual feedback. Supports 100+ languages.

### Keyboard navigation

| Key | Action |
|-----|--------|
| `/` or `Cmd+K` | Open search |
| `Escape` | Close overlays |
| `Arrow keys` | Navigate search results; prev/next page (docs) |
| `Enter` | Select search result |

### Accessibility

- Skip-to-content link
- Semantic landmarks (`<main>`, `<nav>`, `<footer>`)
- ARIA labels on interactive elements
- `aria-labelledby` on content sections
- `aria-live` regions for dynamic content
- `prefers-reduced-motion` respected
- Keyboard-navigable throughout
- Screen reader support for search, theme toggle, navigation

### Responsive

Mobile-first with breakpoints at 640px, 1024px, and 1280px. Sidebar collapses to an overlay on mobile. Navigation uses a hamburger menu with full-screen overlay.

### Print

Print-optimized stylesheet hides navigation, sidebars, and interactive elements. Forces light background for readability.

## Templates

| Template | Purpose |
|----------|---------|
| `base.html` | Root layout, SEO meta, JSON-LD, scripts |
| `landing.html` | Product landing page with hero, features, CTAs |
| `page.html` | Single page / article with metadata |
| `section.html` | Section index with listings and search |
| `blog.html` | Blog listing with cards |
| `home.html` | Homepage for site/blog modes |
| `404.html` | Error page |
| `print.html` | Print-friendly layout |

### Partials

`header.html` `footer.html` `sidebar.html` `search.html` `theme-toggle.html` `nav-overlay.html` `toc-overlay.html` `nav-buttons.html`

### Macros

- **`nav.html`** — `nav_links`, `sidebar_nav`, `breadcrumbs`, `toc`, `prev_next`
- **`ui.html`** — `tag`, `tag_list`, `button`, `pill_button`, `section_header`, `pagination`, `social_links`, `avatar`
- **`posts.html`** — `post_row`, `post_card`, `post_grid`

## SCSS architecture

```
sass/
├── style.scss          # Entry point
├── tokens/             # Design tokens (colors, spacing, typography)
├── base/               # Reset, fonts, base typography
├── components/         # UI components (layout, nav, sidebar, code, search, ...)
├── modes/              # Mode-specific overrides (product, blog)
└── patterns/           # Reusable patterns (cards, buttons, lists, sections)
```

Colors, spacing, and typography are defined as CSS custom properties in the tokens layer, making the theme easy to customize without modifying component styles.

## Requirements

- Zola >= 0.19.0
- Fonts loaded from CDN (Geist from jsDelivr, Clash Display from Fontshare) — no build step needed

## License

MIT
