# Somehow at Next

Personal blog documenting Google Cloud Next 2026 — Las Vegas, April 22–24.

Written by Will Louzado, Senior Platform Engineer at [Beyond](https://www.bynd.com/).

**Read it here: https://will-l-dev.github.io/will-l-dev.github.io-next-blog/**

---

This is a personal conference blog, not a template or starter project. If you've landed here looking for the content, the link above is where you want to be.

## Stack

- [Hugo](https://gohugo.io/) static site generator (extended)
- [Stack theme v4](https://github.com/CaiJimmy/hugo-theme-stack) via Hugo Modules
- GitHub Pages via GitHub Actions — push to `master` deploys automatically

## Publishing workflow

Drafts live in `_drafts/` (gitignored). To publish a post:

1. Copy the folder from `_drafts/<section>/post-name/` to `content/<section>/post-name/`
2. Remove `draft: true` from front matter
3. Rename images to kebab-case
4. Commit and push to `master`
