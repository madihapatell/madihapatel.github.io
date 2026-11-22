# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Madiha Patel's personal blog/portfolio, a Jekyll site built on the [Mundana theme](https://github.com/wowthemesnet/mundana-theme-jekyll) (Bootstrap 4, jQuery, lunr search). The theme files are vendored into this repo, not loaded as a gem. It's hosted on GitHub Pages and built with the `github-pages` gem (Jekyll 3.10).

## Commands

```bash
bundle config set --local path vendor/bundle && bundle install
LANG=C.UTF-8 LC_ALL=C.UTF-8 bundle exec jekyll serve   # http://127.0.0.1:4000/madihapatel.github.io/
LANG=C.UTF-8 LC_ALL=C.UTF-8 bundle exec jekyll build   # outputs to _site/
```

The UTF-8 locale is required in minimal containers, or Sass fails with "Invalid US-ASCII character". There are no tests or linters.

## Site structure

- **Three sections in the nav:** About (`_pages/about.html`), Blogs (`_pages/blogs.html`), Contact (`_pages/contact.html`). `index.html` is the home page: an intro hero, Mundana's 4-post grid, and a paginated "All Stories" list. Page 1 skips the 4 posts already shown in the grid via `offset`.
- **The blog has two sections**, selected by a custom front-matter key on each post:
  - `section: creator` → "Creator Diaries" (personal food/travel/lifestyle/creator-journey posts)
  - `section: marketing` → "Content & Marketing" (content writing, SEO, digital marketing articles)

  `_pages/blogs.html` filters with `where: "section", ...`. A post with no `section` won't appear on the Blogs page.
- **Post front matter:** `title`, `section`, `categories` (one short label shown as "In X"; `text-capitalize` is applied, so write acronyms in caps, e.g. `SEO`), `tags` (`featured` puts the post in the sidebar's Featured list), and `image` (path without a leading slash, e.g. `assets/images/cover-x.svg`). Layout and author (`madiha`) come from `_config.yml` defaults.
- **Hire-me CTA:** `_includes/hire-cta.html` (links to LinkedIn) is used at the bottom of the About page, in the Blogs sidebar, and on every post in place of the theme's newsletter box.
- **Contact is LinkedIn only** (`site.linkedin` in `_config.yml`). Don't add email, phone or forms. The resume this content came from has placeholder contact details.
- **Styling:** `assets/css/main.css` (theme's Bootstrap build) and `assets/css/theme.css` (Mundana styles) are vendored theme files. Put site-specific CSS in `assets/css/custom.css`. Palette: mint `#e8f3ec`, green `#03a87c`, blush `#f7e3dc`, terracotta `#d9785f`.

## Gotchas

- The repo is `madihapatell/madihapatel.github.io`, and the owner's username differs from the repo name, so GitHub Pages serves it as a **project site** at `https://madihapatell.github.io/madihapatel.github.io/`. That's why `baseurl` is `/madihapatel.github.io`. All internal links and asset paths must be prefixed with `{{ site.baseurl }}`. If the repo is ever renamed to `madihapatell.github.io`, set `baseurl: ''`.
- `theme: null` in `_config.yml` stops the `github-pages` gem from injecting its default Primer theme.
- `permalink: /:title/`, so post URLs are just the slug (no date).
- Bootstrap JS is served locally from `assets/js/bootstrap.js`. jQuery, Popper, Font Awesome and Google Fonts load from CDNs.
