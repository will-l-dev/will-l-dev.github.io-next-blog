# CLAUDE.md — Somehow at Next

Personal conference blog documenting Google Cloud Next 2026 (Las Vegas, April 22–24).
Written by Will Louzado, Senior Platform Engineer at Beyond.

Live at: https://will-l-dev.github.io/will-l-dev.github.io-next-blog/

---

## Critical rules for agents

- **Never push to the remote without explicit confirmation from the user.** Always show what you intend to commit/push and wait for approval before running `git push`.
- Never add "Co-Authored-By: Claude" or any AI attribution to commits or post content.
- Never rewrite the author's voice — fix typos and structure only.

---

## Stack

- [Hugo](https://gohugo.io/) static site generator (extended)
- [Stack theme v4](https://github.com/CaiJimmy/hugo-theme-stack) via Hugo Modules
- GitHub Pages via GitHub Actions (push to `master` → auto-deploy)
- Pre-commit hooks: conventional commits, 2048KB image limit, gitleaks, whitespace

---

## Content sections

| Section | Path | Purpose |
|---|---|---|
| `post` | `content/post/` | End-of-day write-ups (Day 0, Day 1, Day 2, Day 3) |
| `agenda` | `content/agenda/` | Individual session posts |
| `food-events` | `content/food-events/` | Restaurants, networking events, bars |
| `travel` | `content/travel/` | Flights, hotels, transfers |
| `page` | `content/page/` | Static pages (about, archives, search) |

Posts in `post/` have a custom permalink: `/p/:slug/`. All other sections use default paths.

---

## Draft workflow

`_drafts/` is gitignored — nothing in it is ever committed or deployed. It is the working area.

**To publish a post:**

1. Copy the folder from `_drafts/<section>/<post-name>/` to `content/<section>/<post-name>/`
2. Remove `draft: true` from the front matter
3. Rename any images to kebab-case (see image workflow below)
4. Commit and push to `master`

GitHub Actions builds and deploys automatically. No manual deploy step needed.

**To unpublish a post:**

Delete the folder from `content/<section>/<post-name>/` and push.

---

## Image workflow

All images must be under **2048KB** (enforced by pre-commit hook).

**Compress before committing:**
```bash
sips --resampleWidth 2000 --setProperty formatOptions 75 image.jpg
```

**Naming convention:** kebab-case descriptive names. Never use original `IMG_YYYYMMDD_HHMMSS.jpg` filenames in published posts.

Examples:
- `strip-view.jpg` not `IMG_20260421_201745.jpg`
- `arena-entrance.jpg` not `Arena Entrance.jpg`
- `vibe-coding-live.jpg` not `Vibe Coding Live.jpg`

Draft folders may contain original filenames — rename on copy to content.

**Favicon:** lives in both `static/favicon.ico` (browser fallback) and `assets/img/favicon.png` (Stack theme uses Hugo's resource pipeline from `assets/`, not `static/`).

---

## Photo organisation

Unprocessed photos from the trip are stored in `_drafts/photos/<date>/`:

- `_drafts/photos/apr20/` — arrival night (10 photos)
- `_drafts/photos/apr21/` — partner summit / BrewDog day (15 photos)
- `_drafts/photos/apr22/` — Day 1 conference (97 photos)
- `_drafts/photos/apr23/` — Day 2 conference (85 photos)
- `_drafts/photos/apr24/` — Day 3 + return (52 photos)

Timestamps are in US Pacific Time (Vegas local). Early-hours Apr 24 shots (00:xx–03:xx) are likely from the Thursday night Beyond Bar event running late.

---

## Front matter reference

### post (daily write-ups)
```yaml
title: "Day N — April DD — Title"
description: ""
date: 2026-04-22T22:00:00-07:00
image: "cover.jpg"
categories: ["Daily Write-ups"]
tags: []
series: ["Google Cloud Next 2026"]
```

### agenda (session posts)
```yaml
title: "Session Title"
description: ""
date: 2026-04-22T09:00:00-07:00
image: ""
categories: ["Agenda"]
tags: []
series: ["Google Cloud Next 2026"]
session_date: "2026-04-22"
rating: 0
```

### food-events
```yaml
title: "Venue Name or Event Name"
description: ""
date: 2026-04-22T20:00:00-07:00
image: ""
categories: ["Food & Events"]
tags: []
series: ["Google Cloud Next 2026"]
event_type: "restaurant"   # restaurant | networking | expo | drinks
venue: "Full address"
```

### travel
```yaml
title: "Route or Venue"
description: ""
date: 2026-04-20T21:00:00-07:00
image: ""
categories: ["Travel Log"]
tags: []
series: ["Google Cloud Next 2026"]
travel_type: "flight"      # flight | hotel | transfer
destination: "Full address or airport"
departure_time: ""
arrival_time: ""
```

---

## Commit conventions

Enforced by pre-commit hook. Valid types:

```
post      — publishing or updating blog content
agenda    — session posts
feat      — new site feature
fix       — bug fix (broken links, layout, favicon, etc.)
chore     — maintenance (dependency updates, config)
style     — CSS / theme changes
ci        — GitHub Actions changes
docs      — documentation
refactor  — code restructure
```

Example: `post: publish opening keynote with photos and queue story`

**Never** include "Co-Authored-By: Claude" or any AI attribution in commits or post content.

---

## Internal links

Hugo is deployed to a subdirectory (`/will-l-dev.github.io-next-blog/`), so root-relative links like `/food-events/post-name/` will break. Always use Hugo's `relref` shortcode for internal links:

```markdown
[read that post]({{< relref "/food-events/apr21-team-dinner-brewdog" >}})
```

---

## Writing style

- **Voice:** Will's own — first person, direct, honest. Light editing only. Fix typos and structure; do not rewrite or compress his words.
- **Tone:** Practitioner angle. Will career-changed from Recruitment to Senior Platform Engineer — posts are written from earned experience, not assumed expertise.
- **Comments:** No code comments, no AI-generated filler. Every sentence should be something Will would have written.
- **Links:** Hyperlink people, venues, products, and Wikipedia references where relevant. External links only — no guessing URLs.
- **Photos:** Add captions that describe what's actually in the image. Attribution required for any third-party images (e.g. `© Google Street View`).

---

## Local development

Requires Hugo extended and Go installed locally.

```bash
hugo server --buildFuture --disableFastRender
# open http://localhost:1313/will-l-dev.github.io-next-blog/
```

`--buildFuture` is needed because posts are dated during the conference (April 22–24 2026).

---

## Update theme

```bash
hugo mod get -u github.com/CaiJimmy/hugo-theme-stack/v4
hugo mod tidy
git add go.mod go.sum
git commit -m "chore: update Stack theme"
```
