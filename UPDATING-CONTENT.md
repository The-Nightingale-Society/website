# Updating the Website — No Coding Needed

This guide is for whoever runs the site after the initial build — updating the book pick, adding an event, or adding a team member. You don't need to know HTML. You just need to edit a short list of items near the bottom of a file, and copy/paste.

## The pattern (same for every section)

The site lives on GitHub now, so you edit the actual page file directly — no copy/pasting into a different tool afterward. **You can do this entirely in a web browser, no software to install:**

1. Go to the file on github.com (e.g. the repo → `events.html`).
2. Click the **pencil icon** (Edit this file) in the top right of the file view.
3. Scroll down until you find a block that looks like this:

```js
const events = [
  { month: "Sep", day: "12", title: "Monthly Discussion", meta: "7pm · Central Library", desc: "..." },
  { month: "Oct", day: "3",  title: "Writing Night", meta: "7pm · Zoom", desc: "..." },
];
```

Each line inside the `[ ... ]` is **one card** on the page. To change what's on the page:

- **Edit an existing card**: change the text between the quote marks (`"..."`). Don't touch the quote marks, commas, or curly braces `{ }` themselves.
- **Add a card**: copy a whole line (from `{` to `},`), paste it on its own new line, and edit the text inside.
- **Remove a card**: delete its whole line.

That's the entire skill. Every section below uses this same pattern.

**When you're done, scroll to the bottom of the page** and click **"Commit changes..."** → **"Commit directly to the `main` branch"** → **Commit changes**. The live site updates automatically within a minute or two — nothing else to do, no re-pasting into another tool.

(Prefer editing on your own computer instead of in the browser? Any plain text editor works — TextEdit, Notepad, VS Code. Just make sure your change ends up pushed to the `main` branch on GitHub, e.g. via GitHub Desktop: open the app, you'll see the changed file listed, write a one-line summary, and click **Commit to main** then **Push origin**.)

## Currently Reading & Past Reads — `reads.html`

**This section works differently from the rest of the site — it does not use the copy/paste-a-line pattern above.** It reads live from a Google Sheet, so updating it doesn't require touching any code or re-pasting the embed at all.

The sheet: **[Nightingale Society — Website Content](https://docs.google.com/spreadsheets/d/1pULfn9fQH4S8YiucXL0LiDyVxicLmAZ95svPWh9MDDk/edit)** → open the **Reads** tab. Full instructions are also in that sheet's **Read Me** tab.

- One row per book. The **Status** column is either `Current` (exactly one row — shown in the big "Currently Reading" card) or `Past` (shown in the Past Reads grid, newest first — keep the rows in that order).
- When a new month starts: change the current book's row from `Current` to `Past`, then add a new row above it with `Status = Current` for the new pick. Nothing else needs to happen — the site picks it up automatically next time the page loads.
- **Cover**: paste a Google Drive share link (Share → Copy link) or a direct image URL into the Cover column. Leave it blank to show a plain text placeholder.
- Edits typically show up on the live site within seconds — just reload the page. Nothing to re-paste in Google Sites for this section.
- **The sheet must stay shared as "Anyone with the link — Viewer"** (Share → General access) or the site can't read it. If it's ever switched to restricted access, the page silently falls back to the last-known content baked into the file instead of breaking.

**Bonus:** some of the flying books in the homepage animation show real cover art instead of a flat color. That list lives separately in `index.html` — search for `COVER_URLS` near the top of its `<script>` and update it the same way (paste an image URL or a Google Drive share link into the list) whenever the reads change, so the hero stays current too. That one is still edited by hand for now (via the pattern above).

## Upcoming Events — `events.html`

```js
const events = [
  { month: "[Mon]", day: "[DD]", title: "...", meta: "...", desc: "..." },
];
```

`month`/`day` are the two lines shown on the little date badge (e.g. `"Sep"` / `"12"`). List events soonest-first.

## The Team — `about.html`

```js
const leaders = [
  { name: "...", role: "...", bio: "...", photo: "" },
];
```

Add or remove people freely — the cards automatically re-center no matter how many there are. Leave `photo: ""` to show the person's initials in the circle. See **"Adding a book cover or photo"** below for how to fill it in.

## Writing Competition Essays — `writing.html`

```js
const essays = [
  { title: "...", author: "...", blurb: "...", status: "pending", link: "" },
];
```

Leave `status: "pending"` and `link: ""` until an essay is ready to publish — it'll show as "Coming Soon". When it's ready, change `status` to `"published"` and put the essay's link (a Google Doc, PDF, or new page) between the quotes for `link`.

## Adding a book cover or photo

Book covers (`cover`) and team photos (`photo`) work the same way. The page can't use a picture straight off your computer — it needs a web address (URL). The easiest way to get one, **no technical skills needed**:

1. Find a picture of the cover (search "[book title] book cover" and save the image — right-click → Save Image, or a screenshot works too).
2. Upload it to [Google Drive](https://drive.google.com) (drag the file in, or File → Upload).
3. Right-click the file in Drive → **Share** → make sure it's set to **"Anyone with the link"** → **Copy link**.
4. Paste that link directly into the `cover:` or `photo:` field — for example:
   ```js
   cover: "https://drive.google.com/file/d/1AbCdEfGhIjKlMnOp/view?usp=sharing",
   ```
5. Commit the change (see the pattern above) — the live site updates automatically.

You don't need to edit the link or turn it into anything special — paste it exactly as Drive gives it to you. The page automatically converts a Drive share link into a working image.

(If you'd rather host the image somewhere else — Imgur, etc. — any direct image URL works too, as long as it ends up pointing straight at the image file.)

## Things that are safe vs. not safe to touch

✅ Safe: any text between quote marks (`"..."`)
✅ Safe: adding/removing/reordering whole `{ ... },` lines
🚫 Don't touch: anything above the `const ... = [` line, or the HTML/CSS above the `<script>` tag — that's the page's design, not its content
🚫 Don't remove: commas between items, or the `{ }` / `[ ]` brackets

If something looks broken after an edit, the most common cause is a missing comma or quote mark — compare your edited line against the ones above/below it; they should all follow the exact same shape.
