# CLAUDE.md

Personal website for Nick Semenkovich, a physician-scientist at the Medical College of Wisconsin. Built with Jekyll and served by GitHub Pages at `nick.semenkovich.com` (see `CNAME`).

## Stack

- **Jekyll** on the `github-pages` gem (no `Gemfile` is checked in; `.gitignore` and `_config.yml` exclude it — install `gem install github-pages` locally)
- **Plugins:** `jekyll-sitemap`, `jekyll-feed`, `jekyll-seo-tag`
- **Kramdown (GFM)** with `rouge` syntax highlighting
- **Sass** in `_sass/` (partials: base, typography, nav, layout, post, responsive); entrypoint `assets/css/main.scss`
- **Fonts** loaded from Google Fonts: Inter (400/500/600), JetBrains Mono (400)

## Repo layout

- `index.md` — home page bio (uses `layout: default`, not the page layout, because of custom bio flex layout)
- `blog.html` — post index at `/blog` (uses `layout: page`)
- `404.html` — at `/404.html` (no `page.title`, so no `.page-heading` is rendered)
- `_layouts/` — `default.html` (shell), `page.html` (default + optional h1), `post.html` (full article with reading-time + tags)
- `_includes/` — `head.html`, `header.html` (nav), `footer.html`
- `_sass/` — all styles; compiled via `assets/css/main.scss`
- `_config.yml` — permalinks are `/blog/:year/:month/:title/`; default layouts wired per scope
- `_make_favicon.sh` / `_make_thumbnails.sh` — one-shot ImageMagick helpers; both require `brew install imagemagick`. `_make_thumbnails.sh` expects `images/` (source) and `tn/images/` (dest); neither exists in the repo yet.
- `headshot.png` — used by `index.md` and as the source for `favicon.ico`
- There is no `_posts/` directory yet — the blog index falls through to the empty-state message.

## Local dev

```
gem install github-pages
bundle exec jekyll serve --livereload
```

(The `bundle exec` workflow in the README presumes you create a `Gemfile` locally — none is committed.)

## Conventions

- Color tokens are hard-coded stone/neutral hex values (e.g., `#FAFAF9` bg, `#1C1917` text, `#2563EB` link). There is no color-variables file — if you edit one, grep across `_sass/`.
- Content width: `.page-content` is `max-width: 800px`; `.content-narrow` (used by post bodies) is `max-width: 680px`.
- Navigation lives in `_includes/header.html`; external links get `class="nav-external"` which adds a `→` glyph via CSS.
- `footer.html` prints the current year from `site.time` and links to the GitHub source.
- Responsive breakpoints are 768px and 480px in `_sass/_responsive.scss`.
- Body type is justified (`text-align: justify` in `_sass/_typography.scss`).

## Known issues / rough edges (from a quick review)

- **Duplicate `<title>` tags.** `_includes/head.html:13` renders a manual `<title>`, and `{% seo %}` on line 21 also emits one. Fix: either remove the manual `<title>` or pass `{% seo title=false %}`.
- **Dead CSS selector.** `_sass/_layout.scss:60` targets `.blog-index .page-title`, but `_layouts/page.html:5` renders the class `.page-heading`. Rename or remove.
- **`Gemfile` missing but referenced.** `README.md` tells users to `bundle exec jekyll serve`, yet `Gemfile`/`Gemfile.lock` are git-ignored and excluded by `_config.yml`. New contributors will need to create one themselves.
- **`_make_thumbnails.sh` silently no-ops.** It globs `images/*.png` and `images/*.jpg`, but no `images/` directory exists.
- **Favicon is heavy.** `favicon.ico` is ~240 KB because it's generated from the full-resolution `headshot.png` at many sizes.
- **README tip is stale.** The note about `permalink: /` and sitemap duplicates no longer applies — `index.md` uses the default permalink.

None of these block builds; the site renders and deploys. They're worth cleaning up opportunistically.

## Deploy

Push to `main` on `semenko/semenko.github.io`; GitHub Pages builds and serves at the custom domain in `CNAME` (`NICK.SEMENKOVICH.COM`). Domain is on the HSTS preload list (see comment in `_includes/head.html`).
