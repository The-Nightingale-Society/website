# The Nightingale Society — Website

The live site is a plain static site (no build step) hosted on **GitHub Pages**. See `style-guide.md` for the color/font system every page shares.

**Handing this off to a non-technical volunteer?** Point them at `UPDATING-CONTENT.md` — it covers routine updates (swap the book pick, add an event, add a team member, publish an essay) with no HTML knowledge required.

## Pages

| Page | File |
|---|---|
| Home | `index.html` |
| About / Our Story | `about.html` |
| Current & Past Reads | `reads.html` |
| Events | `events.html` |
| Writing Competition & Essays | `writing.html` |
| Join / Contact | `join.html` |

Every page shares the same nav bar and footer (see the `.site-nav` / `.site-footer` markup near the top/bottom of each file). There's no shared-include mechanism since there's no build step — if the nav links ever change, update the nav block in all six files the same way.

## Deploying (GitHub Pages)

1. Push this repo to GitHub (any repo name).
2. On GitHub: **Settings → Pages** → under "Build and deployment", set **Source** to **Deploy from a branch** → **Branch: `main`**, folder **`/ (root)`** → **Save**.
3. GitHub gives you a URL like `https://<username>.github.io/<repo-name>/` within a minute or two. `index.html` becomes the homepage automatically.
4. Optional custom domain: **Settings → Pages → Custom domain**, plus a DNS record at your domain registrar pointing at GitHub Pages (GitHub shows the exact record to add once you enter the domain).
5. Every `git push` to `main` redeploys automatically — no separate publish step, unlike the old Google Sites paste-in workflow.

The `.nojekyll` file at the repo root tells GitHub Pages to serve the files as-is instead of running them through Jekyll (not needed for a plain HTML site, and Jekyll would otherwise ignore some file patterns by default).

## Live content: one Google Sheet drives almost the whole site

Every page except the nav/footer chrome pulls its content from **[Nightingale Society — Website Content](https://docs.google.com/spreadsheets/d/1ROOwcdW6NzdlVxAoMm2XwHDUNeS1P2yLajQpHyYAv7s/edit)** on every page load — no commit needed to change content. See `UPDATING-CONTENT.md` for the volunteer-facing guide; the short version:

| Sheet tab | Page(s) |
|---|---|
| Reads | `reads.html` (Currently Reading / Past Reads), and the flying book covers on `index.html` |
| Events | `events.html` |
| About | `about.html` (mission paragraph) |
| Team | `about.html` (team cards) |
| Writing | `writing.html` (competition facts) |
| Essays | `writing.html` (essay cards) |
| Join | `join.html` |

The sheet must stay shared as "Anyone with the link — Viewer" or the site can't read it. If that ever breaks, each page falls back to content hardcoded in the file (`FALLBACK_*` constants near the bottom of each `<script>`) rather than showing anything broken. Because these are real top-level pages (not iframe embeds), there's no sandbox uncertainty about the fetch working — it just works.

There's no tooling to add tabs to an *existing* Google Sheet from outside Sheets itself, so if the sheet ever needs to be rebuilt from scratch, the cleanest path is a new file with the same tab names/columns, with its ID swapped into the `SHEET_ID` constant near the top of each page's `<script>` (and the sheet needs re-sharing, since sharing doesn't carry over to a new file).

## Images just work now

Every image reference (`assets/nightingale-logo-transparent.png`, book covers, etc.) uses a plain relative path, and GitHub Pages serves the whole repo — so local images work in production exactly like they do in local preview. Nothing needs to be re-uploaded to Google Drive or hosted externally, unlike the old Google Sites setup. The one place external hosting still matters is content added *through the Google Sheet* (book covers, team photos) — those still take a Google Drive share link or direct image URL, same as before, since they're not files in this repo.

## The hero: logo badge + flying book chains

`index.html` has two moving parts:

- **The logo badge** sits in the open space to the right of the headline — it's laid out with flexbox (`hero__content` fixed-width on the left, `hero__logo-slot` taking the remaining space and centering the badge in it), so it stays centered between the end of the text and the hero's right edge at any viewport width, no hardcoded position needed.
- **Flying book chains** — Discord-style: every few seconds (randomized), a little train of 2–3 toon-shaded books spawns off-canvas, swoops across the top of the hero, loops once, trails sparkle particles behind the lead book, fades out, and disappears — then a new chain spawns again after a random pause (up to 2 chains can overlap so it never feels empty). Books are colored from the site's own palette (rust, sand, parchment) so they read as one system with the buttons rather than a separate illustration style. Rendered with three.js (CDN, no build step), toon-shaded with an ink-outline look — same core rendering technique used on rockrobotics.org (toon shading + outline shader + requestAnimationFrame loop), built out here into a spawn/flight/fade lifecycle instead of objects idling in place. It:

- Pauses automatically when scrolled out of view or the tab is hidden (battery/performance friendly).
- Respects `prefers-reduced-motion` (skips motion, keeps the shapes visible).
- Hides on narrow mobile viewports in favor of a simpler static layout (same fallback pattern as the reference site).

The `try/catch` around WebGL setup hides the canvas gracefully if three.js ever fails to load (e.g. the CDN is unreachable), and the hero still looks complete with just the text and logo.

## Writing Competition / Essays — adding real essays later

This is now sheet-driven (see above) — open the **Essays** tab in the Google Sheet, one row per essay. Leave `Status = pending` and `Link` blank for unpublished entries — renders as a "Coming Soon" card. Once an essay is ready, set `Status = published` and `Link` to wherever the full essay lives. No commit needed; see `UPDATING-CONTENT.md`.

## Legacy: `embeds/` (Google Sites paste-in versions)

Before moving to GitHub Pages, this site was built as six self-contained files meant to be pasted into Google Sites' "Embed code" block per page. Those original files are kept in `embeds/` in case this project ever needs to go back to embedding into another site builder, but **they are not part of the live GitHub Pages site** and are no longer kept in sync with the root-level pages — treat the root-level `.html` files as the source of truth going forward.
