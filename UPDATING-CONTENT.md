# Updating the Website — No Coding Needed

**Nearly everything on the site is controlled by one Google Sheet.** Editing it updates the live site automatically — no code, no GitHub, no re-publishing. Just edit a cell, reload the site.

**The sheet:** **[Nightingale Society — Website Content](https://docs.google.com/spreadsheets/d/1ROOwcdW6NzdlVxAoMm2XwHDUNeS1P2yLajQpHyYAv7s/edit)**

Open its **Read Me** tab first — it has the same instructions as below, kept next to the data itself. The sheet has one tab per section of the site:

| Tab | Controls |
|---|---|
| **Reads** | Currently Reading + Past Reads, and the book covers on the flying-book homepage animation |
| **Events** | The Upcoming Events list |
| **About** | The mission statement paragraph |
| **Team** | The team member cards |
| **Writing** | The Writing Competition facts (theme, deadline, prize, etc.) |
| **Essays** | The submitted essay cards |
| **Join** | The Join page's invitation text and contact links |

**This file must stay shared as "Anyone with the link — Viewer"** (Share → General access, top right of the sheet) or the site can't read it. If sharing ever gets switched to restricted, the site doesn't break — it just quietly falls back to old content baked into the page until sharing is fixed.

## Two kinds of tabs

**List tabs** (Reads, Events, Team, Essays) — one row = one card on the site. Add a row, delete a row, reorder rows (drag by the row number) — the site follows automatically, in the order the rows appear top to bottom.

**Field / Value tabs** (About, Writing, Join) — a short list of individual settings, one per row. Don't rename anything in the **Field** column; just edit the **Value** column next to it.

## Reads tab

- One row per book. **Status** is either `Current` (exactly one row — the big "Currently Reading" card) or `Past` (the Past Reads grid, newest first — keep rows in that order).
- When a new month starts: change the current book's row from `Current` to `Past`, then add a new row above it with `Status = Current` for the new pick.
- **Cover** also feeds the flying book covers on the homepage — no separate place to update those anymore.
- See **"Adding a cover or photo"** below for the Cover column.

## Events tab

Columns: `Month`, `Day`, `Title`, `Meta`, `Description`. `Month`/`Day` are the two lines on the little date badge (e.g. `Sep` / `12`). List soonest-first.

## About tab

One row, `Mission` — the paragraph under "Why the Nightingale Society exists."

## Team tab

Columns: `Name`, `Role`, `Bio`, `Photo`. Add or remove rows freely — the cards automatically re-center no matter how many there are. Leave `Photo` blank to show the person's initials instead.

## Writing tab

Rows: `Year`, `Theme`, `Deadline`, `Prize`, `Submit To`, `Description` — the competition facts shown at the top of the Writing page.

## Essays tab

Columns: `Title`, `Author`, `Blurb`, `Status`, `Link`. Leave `Status = pending` and `Link` blank until an essay is ready — it shows as "Coming Soon." When it's ready, set `Status = published` and put the essay's link (a Google Doc, PDF, or anywhere else it lives) in `Link`.

## Join tab

Rows: `Description` (the invitation paragraph), `Email`, `RSVP Link`, `Instagram` — used for both buttons and the contact line at the bottom of the Join page.

## Adding a cover or photo

The **Cover** (Reads, and via Reads the homepage animation) and **Photo** (Team) columns can't use a picture straight off your computer — they need a web address (URL). Easiest way, no technical skills needed:

1. Find the picture (search "[book title] book cover", or use a headshot — right-click → Save Image, or a screenshot works too).
2. Upload it to [Google Drive](https://drive.google.com) (drag the file in, or File → Upload).
3. Right-click the file in Drive → **Share** → set to **"Anyone with the link"** → **Copy link**.
4. Paste that link directly into the Cover/Photo cell — for example:
   ```
   https://drive.google.com/file/d/1AbCdEfGhIjKlMnOp/view?usp=sharing
   ```

You don't need to edit the link — paste it exactly as Drive gives it to you. The site automatically converts a Drive share link into a working image. A direct image URL from anywhere else (Imgur, Amazon, etc.) works too, pasted as-is.

## If you ever need to change the site's design instead of its content

Everything above covers content. If you ever need to change layout, colors, or add a whole new page — that's still done by editing the actual `.html` files (`index.html`, `about.html`, `reads.html`, `events.html`, `writing.html`, `join.html`) directly on GitHub:

1. Go to the file on github.com, click the **pencil icon** (Edit this file).
2. Make your change.
3. Scroll down, click **"Commit changes..."** → **"Commit directly to the `main` branch"**.

The live site updates within a minute or two — no separate publish step.
