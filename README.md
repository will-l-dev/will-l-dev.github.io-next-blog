# Somehow at Next

Personal blog documenting Google Cloud Next 2026 — Las Vegas, April 22–24.

Written by Will Louzado, Senior Platform Engineer at [Beyond](https://www.bynd.com/).

Live at: https://will-l-dev.github.io/will-l-dev.github.io-next-blog/

---

## Stack

- [Hugo](https://gohugo.io/) static site generator
- [Stack theme](https://github.com/CaiJimmy/hugo-theme-stack) via Hugo Modules
- GitHub Pages via GitHub Actions

## Local development

Requires Hugo extended and Go installed locally.

```bash
hugo server --buildFuture --disableFastRender
```

Posts are future-dated (conference is April 22–24), so `--buildFuture` is needed to preview them locally.

## Publishing workflow

Drafts live in `_drafts/` (gitignored). To publish a post:

1. Move the folder from `_drafts/<section>/post-name/` to `content/<section>/post-name/`
2. Commit and push to `master`
3. GitHub Actions builds and deploys automatically

## Update theme

```bash
hugo mod get -u github.com/CaiJimmy/hugo-theme-stack/v4
hugo mod tidy
```
