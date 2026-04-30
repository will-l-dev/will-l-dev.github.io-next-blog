# HANDOFF — Somehow at Next

Machine migration handoff. Read this first when picking up the project on a new machine.

---

## New Machine Setup

### 1. Clone this backup repo

```bash
git clone https://github.com/will-l-dev/beyond-next-blog-backup.git beyond-next-blog
cd beyond-next-blog
```

### 2. Restore _drafts and Claude memory

```bash
git checkout drafts-backup -- _drafts/
git checkout drafts-backup -- _claude-memory/
```

### 3. Restore Claude memory files

The `_claude-memory/` folder contains the memory files Claude uses across sessions.
Copy them to the correct location (adjust `<username>` for the new machine's username):

```bash
mkdir -p ~/.claude/projects/-Users-<username>-Documents-beyond-next-blog/memory/
cp _claude-memory/*.md ~/.claude/projects/-Users-<username>-Documents-beyond-next-blog/memory/
```

Check `_claude-memory/MEMORY_PATH.txt` for the exact original path structure.

### 4. Swap remotes

This backup repo is for storage only. Point origin back at the live GitHub Pages repo:

```bash
git remote rename origin backup
git remote add origin https://github.com/will-l-dev/will-l-dev.github.io-next-blog.git
```

### 5. Run the site locally

```bash
hugo server --buildFuture --disableFastRender
# http://localhost:1313/will-l-dev.github.io-next-blog/
```

Requires Hugo extended and Go installed.

---

## Project Overview

**Blog:** "Somehow at Next" — personal conference blog documenting Google Cloud Next 2026 (Las Vegas, April 22–24). Written by Will Louzado, Senior Platform Engineer at Beyond (Qodea).

**Live site:** https://will-l-dev.github.io/will-l-dev.github.io-next-blog/

**Stack:** Hugo + Stack theme v4, GitHub Pages via GitHub Actions. Push to `master` → auto-deploy.

**Public repo:** https://github.com/will-l-dev/will-l-dev.github.io-next-blog

---

## What Is Published (as of 2026-04-30)

### Agenda

| Post | Rating |
|---|---|
| Opening Keynote: The Agentic Cloud | — |
| Red-Green Refactor & Secure | — |
| Full Stack Improv with AI | — |
| Automating Excellence: Gemini & Config Connector | 5 |
| Lights, Camera, AI Action (Glance) | 3 |
| Self-Confidence: I'm Not Enough | 5 |
| AI DevOps Velocity | 5 |
| Developer Keynote: Agents in the Autonomous Era | 4 |
| Hunting Threats Against AI Infrastructure | 4 |
| Platform Engineering Meetup | 3 |
| Vibe from Code to Cloud | 5 |
| PR Roaster (Multi-Agent) | 4 |

### Food & Events

- Pret at Heathrow (Apr 20)
- BrewDog team dinner (Apr 21)
- Wahlburgers (Apr 22)
- House of Blues client lunch (Apr 23)
- Beyond Bar @ BrewDog Rooftop (Apr 23)

### Travel

- Swindon → Heathrow (Apr 20)
- LHR → Las Vegas (Apr 21)
- Luxor Hotel
- Las Vegas → LHR

### Daily Write-ups

- Day 0 — April 21
- Day 1 — April 22

---

## What Is Left to Publish

| # | Post | Section | Status |
|---|---|---|---|
| 1 | Architect Flight Simulator | Agenda (Day 3) | Photos + meme ready in `_drafts/agenda/apr24-architect-flight-simulator/`. Rough notes in `index.md`. Post NOT written yet. |
| 2 | Expo Hall | Food & Events | `_drafts/food-events/apr23-expo-hall/` — photos compressed. Parked — covers multiple visits across Day 2, needs consolidating into one post. |
| 3 | Day 2 write-up | Daily Posts | `_drafts/post/day-2-apr23/` — not started. Wait until all Day 2 agenda + food content is published. |
| 4 | Day 3 write-up | Daily Posts | `_drafts/post/day-3-apr24/` — not started. Wait until Architect Simulator is done. |
| 5 | Heathrow → Swindon (return) | Travel | Empty draft — needs writing. Return train journey from Heathrow to Swindon after landing. |
| 6 | Memes | All agenda posts | All memes removed from published posts. Generate them yourself using the suggestions below and `_drafts/meme-suggestions.md`. Add as `agenda-meme.jpg` in each post folder, insert after the intro section with `## Agenda Meme` heading. |

---

## Agenda Meme Suggestions

All memes removed from published posts pending manual regeneration. Generate via https://imgflip.com.
Place in each post's content folder as `agenda-meme.jpg`. Insert after intro (after speakers line, before first content section) using:

```markdown
---

## Agenda Meme

![description](agenda-meme.jpg)

---
```

### 1. Opening Keynote: The Agentic Cloud
**Template:** Drake Hotline Bling
- ❌ Reading the vendor changelog
- ✅ Attending a 3-hour keynote that IS the vendor changelog

### 2. Red-Green Refactor & Secure
**Template:** Two Buttons (sweating)
- Button 1: Deploy green (proven zero-downtime strategy)
- Button 2: Keep red (it works, don't touch it)

### 3. Full Stack Improv with AI
**Template:** Gru's Plan
- Step 1: AI generates the feature
- Step 2: You say "yes, and"
- Step 3: AI says "yes, and" back
- Step 4: You now own a distributed microservices architecture

### 4. Automating Excellence: Gemini & Config Connector
**Template:** And It's Gone (South Park)
- Panel 1: Your consistent infrastructure state
- Panel 2: ...aaaand a user ClickOps through the console

### 5. Lights, Camera, AI Action (Glance)
**Template:** Tumbleweed / empty office
- Caption: "The editing team, six months after Glance deployed their AI pipeline"

### 6. Self-Confidence: I'm Not Enough
**Template:** Distracted Boyfriend
- Girlfriend (ignored, left): Kubernetes session
- Boyfriend: Me
- Woman being looked at (right): Mindset session

### 7. AI DevOps Velocity
*(No meme — removed, not replacing)*

### 8. Developer Keynote: Agents in the Autonomous Era
**Template:** Drake Hotline Bling
- ❌ Hello world agent demo
- ✅ Full Las Vegas marathon simulator with 10,000 runners built live on stage

### 9. Hunting for Threats Against AI Infrastructure
**Template:** Spider-Man Pointing at Himself
- Left: AI used to attack AI infrastructure
- Right: AI used to defend AI infrastructure

### 10. Platform Engineering Meetup
**Template:** Matrix Morpheus / "What If I Told You"
- Top: What if I told you
- Bottom: Platform Engineering ROI was right in front of you?

### 11. Vibe from Code to Cloud
**Template:** Distracted Boyfriend
- Girlfriend (ignored): IaC, security policies, CI/CD config, blast radius analysis
- Boyfriend: Me
- Woman being looked at: Vibing an entire app in 20 minutes

### 12. PR Roaster (Multi-Agent)
*(No meme — removed, not replacing)*

---

## What Is NOT in This Backup

The `drafts-backup` branch was taken on 2026-04-30. The following were created after that and are only in `_drafts/` locally (not on the backup branch):

- `_drafts/meme-suggestions.md` — full meme suggestions list (duplicated above)
- `_drafts/meme-review/` — copies of the generated meme images for review

Everything else in `_drafts/` is captured on this branch. The `master` branch of this repo is fully in sync with the live site.

---

## Key Conventions

- `_drafts/` is gitignored — never committed to the public repo
- Images must be under 2048KB (pre-commit hook enforces this)
- Compress: `sips --resampleWidth 2000 --setProperty formatOptions 75 image.jpg`
- Internal links: use `{{< relref "/section/post-name" >}}`
- Commit types: `post:`, `agenda:`, `feat:`, `fix:`, `chore:`, `style:`, `ci:`, `docs:`
- Never add Co-Authored-By or AI attribution to commits

---

## Notes for Claude

- Will career-changed from Recruitment to Senior Platform Engineer — posts written from earned-practitioner angle
- Never rewrite his voice — fix typos and structure only
- Never use "Worth it?" as a section heading
- The meme theme was Will's idea — all agenda posts should eventually have one
- "Qody" / "Qodea" = Will's company (Beyond, trading as Qodea)
- The site is deployed at a subdirectory path — always use relref for internal links, never root-relative paths
- PDF slides extracted with: `pdftoppm -jpeg -r 150 -f PAGE -l PAGE input.pdf prefix` (outputs ~2000x1125px)
- Gitleaks false positives on slash-separated words (e.g. `analyser/judge`) — rephrase rather than use --no-verify
