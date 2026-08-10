# The Nightingale Society — Website

The live site is a single scrollable page (`index.html`, no build step) hosted on **GitHub Pages**. See `style-guide.md` for the color/font system.

**Handing this off to a non-technical volunteer?** Point them at `UPDATING-CONTENT.md` — it covers routine updates (swap the book pick, add an event, add a team member, publish an essay) with no HTML knowledge required.

## Structure

Everything lives in one file, `index.html`, as a sequence of `<section>`s the visitor scrolls through — there's no click-through page navigation. The sticky nav bar at the top links to each section by anchor (`#home`, `#about`, `#reads`, `#events`, `#writing`, `#join`) and smooth-scrolls to it; a scroll-spy highlights whichever section is currently in view as you scroll.

| Section | Anchor |
|---|---|
| Home / hero | `#home` |
| About / Our Story / Team | `#about` |
| Current & Past Reads | `#reads` |
| Events | `#events` |
| Writing Competition & Essays | `#writing` |
| Join / Contact | `#join` |

## Deploying (GitHub Pages)

1. Push this repo to GitHub (any repo name).
2. On GitHub: **Settings → Pages** → under "Build and deployment", set **Source** to **Deploy from a branch** → **Branch: `main`**, folder **`/ (root)`** → **Save**.
3. GitHub gives you a URL like `https://<username>.github.io/<repo-name>/` within a minute or two. `index.html` becomes the homepage automatically.
4. Optional custom domain: **Settings → Pages → Custom domain**, plus a DNS record at your domain registrar pointing at GitHub Pages (GitHub shows the exact record to add once you enter the domain).
5. Every `git push` to `main` redeploys automatically.

The `.nojekyll` file at the repo root tells GitHub Pages to serve the files as-is instead of running them through Jekyll (not needed for a plain HTML site, and Jekyll would otherwise ignore some file patterns by default).

## Live content: Currently Reading & Past Reads (+ hero book covers)

The Reads section doesn't need a new commit when the book pick changes — it fetches live from a Google Sheet on every page load: **[Nightingale Society — Website Content](https://docs.google.com/spreadsheets/d/1pULfn9fQH4S8YiucXL0LiDyVxicLmAZ95svPWh9MDDk/edit)** (see its "Read Me" tab). Edit the sheet, reload the page, done — see `UPDATING-CONTENT.md` for the exact steps. The sheet must stay shared as "Anyone with the link — Viewer"; if that ever breaks, the page falls back to the content hardcoded in the file rather than showing anything broken.

That same live data also feeds the hero's flying books: every book cover from the sheet (current + all past reads, deduplicated) gets used as a texture on the flying-book chains, instead of a fixed two-cover list. Both the Reads section and the hero share a single fetch of the sheet (`window.NS_READS_PROMISE`) rather than hitting it twice.

This is the only section that's sheet-driven. (An earlier attempt to make every section — Events, Team, Writing — pull from the sheet was tried and reverted; everything else uses the plain hand-edited arrays described in `UPDATING-CONTENT.md`.)

## Images just work now

Every image reference (`assets/nightingale-logo-transparent.png`, book covers, etc.) uses a plain relative path, and GitHub Pages serves the whole repo — so local images work in production exactly like they do in local preview. Nothing needs to be re-uploaded to Google Drive or hosted externally. The one place external hosting still matters is content added *through the Google Sheet* (book covers) — those still take a Google Drive share link or direct image URL, since they're not files in this repo.

## The hero: logo badge + flying book chains

The `#home` section has two moving parts:

- **The logo badge** sits in the open space to the right of the headline — it's laid out with flexbox (`hero__content` fixed-width on the left, `hero__logo-slot` taking the remaining space and centering the badge in it), so it stays centered between the end of the text and the hero's right edge at any viewport width, no hardcoded position needed.
- **Flying book chains** — Discord-style: every few seconds (randomized), a little train of 2–3 toon-shaded books spawns off-canvas, swoops across the top of the hero, loops once, trails sparkle particles behind the lead book, fades out, and disappears — then a new chain spawns again after a random pause (up to 2 chains can overlap so it never feels empty). Most books are colored from the site's own palette (rust, sand, parchment); about 4 in 10 show a real book cover instead (see "Live content" above for where those come from). Rendered with three.js (CDN, no build step), toon-shaded with an ink-outline look — same core rendering technique used on rockrobotics.org (toon shading + outline shader + requestAnimationFrame loop), built out here into a spawn/flight/fade lifecycle instead of objects idling in place. It:

- Pauses automatically when scrolled out of view or the tab is hidden (battery/performance friendly).
- Respects `prefers-reduced-motion` (skips motion, keeps the shapes visible).
- Hides on narrow mobile viewports in favor of a simpler static layout (same fallback pattern as the reference site).

The `try/catch` around WebGL setup hides the canvas gracefully if three.js ever fails to load (e.g. the CDN is unreachable, or the browser/environment has no WebGL support), and the hero still looks complete with just the text and logo.

## Writing Competition / Essays — adding real essays later

Open `index.html` and find the `essays` array (inside the `<script>` block below the `#writing` section). Each entry looks like:

```js
{ title: "Essay Title", author: "Author Name", blurb: "One-line teaser or status", status: "pending", link: "" }
```

- Leave `status: "pending"` and `link: ""` for unpublished entries — renders as a "Coming Soon" card.
- Once an essay is ready, set `status: "published"` and `link` to wherever the full essay lives (a shared Google Doc link, a PDF, or a new page in this repo).
- Add or remove objects in the array for however many entries you have, then commit and push — GitHub Pages redeploys automatically.

## Legacy: `embeds/` (Google Sites paste-in versions)

Before moving to GitHub Pages, this site was built as six self-contained files meant to be pasted into Google Sites' "Embed code" block per page. Those original files are kept in `embeds/` in case this project ever needs to go back to embedding into another site builder, but **they are not part of the live GitHub Pages site** and are no longer kept in sync with `index.html` — treat `index.html` as the source of truth going forward.
