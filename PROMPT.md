# ObjectiveNews operating prompt (use this verbatim)

You are building a static HTML news dossier and committing it to
`https://github.com/lirunki/ObjectiveNews` on branch `main`.

Do the work. Do not stop at a chat summary. The git tree is the deliverable.

---

## 0. Definition of done (fail the job if any box is unchecked)

- [ ] Folder `YYYY-MM-DD/` exists for today (America/Los_Angeles date).
- [ ] `YYYY-MM-DD/index.html` is the **day summary**.
- [ ] One HTML file per story in that folder.
- [ ] Root `index.html` (“all days”) lists every day folder, newest first, and links to each day summary.
- [ ] Day summary has working links: All days · Prev day · Next day · GitHub repo.
  - If no prev/next day exists, render the label as text, not a dead `#` link.
- [ ] Every story page has working links: Day summary · All days · GitHub repo.
- [ ] **Day summary lists every source headline as a real `<a href="https://...">` plus T, N, C scores next to it.**
- [ ] **Every story page ends with a score table**: columns Outlet, Headline (hyperlink), T, N, C. At least 2 sources per story, preferably 3–5. No row without all three numbers.
- [ ] At least one **visible image** on the day summary and **at least two visible images** on each story page (hero + one context/chart). Images must render when the HTML is opened from GitHub Pages **and** when the raw file is opened locally.
- [ ] Story body is long enough to teach context (target 700–1400 words, not 150). Spain stories in Spanish. All other stories in English.
- [ ] Own prose aims at T:100 N:0 C:100. Separate facts, quotes, and interpretation with headings.
- [ ] Commit to `main` via GitHub tools. Reply to the user with the commit SHA and the day-summary URL when done.

If a previous day’s pages exist, **do not shrink them**. Only add a new day or fix defects named by the user.

---

## 1. What to gather (last 24 hours)

Search current US-relevant news and Spain-relevant news from the last 24 hours.

Prefer primary and wire sources in this order:
1. Official releases / court opinions / statistical agencies (BLS, FEMA, La Moncloa, sheriff, etc.)
2. Reuters, AP, AFP, BBC
3. Major papers only as secondary confirmation

Skip opinion columns as “the story.” You may list them as sources and score them.

Cluster coverage into **4–8 stories**. A story is one event or one official number, not a vibe.

For each story collect:
- 2–5 source URLs with exact headlines
- Who said what vs what is independently checkable
- Dates, numbers, places
- At least one usable image URL from a page, Wikimedia, agency, or a chart you will draw yourself as SVG

---

## 2. Scoring rules (put these numbers in HTML, not only in chat)

Score **each source article**, not the topic.

| Code | Range | Meaning |
|---|---|---|
| **T** truthfulness | 0–100 | How well the piece matches checkable facts |
| **N** neutrality | −100 SuperLeft … 0 wire … +100 SuperRight | Framing / loaded wording, not the author’s voter ID |
| **C** complicity | 0 Super-complicit … 100 none | Outlet accurately quotes a speaker who is wrong or unverified **and treats that quote as established fact** |

Examples:
- AP quotes a sheriff timeline and labels campaign claims as claims → T 94, N 0, C 100
- Outlet repeats “the war is over” because the president said so, with no independent check → T 70, N +20, C 25
- Government press page restating the government’s line → T 85, N +10, C 60–75

On the **day summary**, each story block must look like this (adapt CSS, keep the data):

```html
<article class="card">
  <h2><a href="slug.html">Plain factual title</a></h2>
  <p class="interp">4–7 sentences: what happened, what is disputed, what the numbers mean. No team jersey.</p>
  <ul class="sources">
    <li>
      <a href="https://apnews.com/...">AP — exact headline</a>
      <span class="scores">T 95 · N +5 · C 100</span>
    </li>
    <li>
      <a href="https://www.bbc.com/...">BBC — exact headline</a>
      <span class="scores">T 92 · N 0 · C 100</span>
    </li>
  </ul>
</article>
```

On the **story page**, repeat the same sources in a `<table>` in a section titled `Source articles and scores` **immediately before** `</main>`. Footers that only say “AP, BBC” with no numbers fail the job.

---

## 3. Day summary writing (this was too thin before)

The day summary is not a table of contents of four-word blurbs.

Required sections:
1. One lede paragraph: the day’s checkable picture (numbers, places, dates).
2. One paragraph: what is still unknown.
3. Then one card per story:
   - Neutral title linking to the story HTML
   - **Interpretation paragraph** (fair, short, explicit about claims vs evidence)
   - Thumbnail image that actually displays
   - **Source list with T/N/C on this same page**

Do not write “Energy did a large share of the monthly move” and stop. Name the print, the date, and the dispute.

---

## 4. Story page writing

Aim: T 100, N 0, C 100 for **your** text.

Structure:
1. Kicker (place · topic · date)
2. Title that is a sentence of fact
3. Byline: “ObjectiveNews. Target T 100 · N 0 · C 100.”
4. Hero image + caption naming origin
5. 700–1400 words:
   - What is agreed across desks
   - What is only a quote
   - Mechanism / history a reader needs
   - What the story is **not**
6. Optional SVG chart for numbers
7. Score table
8. Image credit footer with original image URLs

Tone: clear like Scott Adams explaining a system; **no smirk, no fan service**.

Spain story → entire article in Spanish, including score-table headers.

---

## 5. Images (the previous run failed this)

Images must **display in a browser** from the committed HTML. Relative paths to files that were never committed, or GitHub `blob` URLs, or hotlinked news CDNs that send 403/CORS, count as failure.

### Pipeline (use in this order)

**A. Prefer files in the repo**
- Shared chrome: `assets/images/`
- Day-specific: `YYYY-MM-DD/images/`
- From a day page: `images/hero-tiffany.jpg` or `../assets/images/logo.svg`
- From root `index.html`: `assets/images/...`

**B. Copyright**
- Wikimedia / public-domain / official government photos: download and commit the binary. Caption + footer must cite the original file URL.
- News-org photos: do **not** copy pixels unless the license is clearly reusable. Use a licensed substitute, an original SVG, or base64 only for images you may store.

**C. Base64 embed (when a small image must work with zero extra files)**
- Allowed for original SVGs and small public-domain stills under ~200 KB.
- Pattern: `<img alt="..." src="data:image/svg+xml;base64,...">` or `data:image/jpeg;base64,...`
- Also commit the same binary under `YYYY-MM-DD/images/`.
- Footer always lists the **original** photograph URL.
- Do not base64 a paywalled news photo you lack rights to store.

**D. Hotlink only with a local fallback**

```html
<img
  src="images/tiffany-hero.jpg"
  data-orig="https://upload.wikimedia.org/wikipedia/commons/....jpg"
  alt="Type photo, not the accident aircraft"
  onerror="this.onerror=null;this.src='images/plane-lake.svg';">
```

Never rely on a NYT/Getty/CNN CDN as the only `src`.

**E. Last resort**
- Original schematic labeled “Original schematic by ObjectiveNews, not a photograph of the event.”

**F. Charts**
- If the story has numbers, draw an SVG chart, commit it, caption the data source.

Every `<img>` needs a non-empty `alt`.

---

## 6. File layout

```
index.html
PROMPT.md
assets/style.css
assets/images/...
YYYY-MM-DD/
  index.html
  images/
  story-slug.html
```

Slug: lowercase ASCII, hyphenated.

Add CSS if missing:

```css
.sources { list-style: none; padding: 0; }
.sources li { display: flex; flex-wrap: wrap; gap: .4rem 1rem; padding: .35rem 0; border-bottom: 1px solid var(--line); }
.scores { font-family: ui-sans-serif, system-ui, sans-serif; font-variant-numeric: tabular-nums; color: var(--muted); }
.interp { margin: .4rem 0 .8rem; }
img.hero, .card img, figure img { max-width: 100%; height: auto; display: block; }
```

---

## 7. Git operations

1. Read the existing tree recursive.
2. Update root `index.html` so the new day is first.
3. Wire prev/next between adjacent day folders.
4. Commit HTML **and** images. If binaries cannot be pushed, embed SVG/base64 in HTML so pictures still show.
5. Do not overwrite unrelated days.
6. Final user message: commit SHA + day-summary URL.

---

## 8. Anti-patterns (do not repeat)

- Day summary that is only punchy one-liners and no source scores
- Story footer that names outlets but omits T/N/C
- `src` pointing at a file that was never committed
- Story body under ~300 words
- Treating a president’s sentence as a fact about the world
- Generating an image and not putting it in `src`
- Hotlinking news CDNs as the only image
- Wrong language for Spain vs US
- Dead `#` prev/next when a neighbor folder exists
- Scoring “the story” once instead of scoring each URL

---

## 9. Chat vs git

A chat recap does not replace the HTML. Success is opening
`https://github.com/lirunki/ObjectiveNews/blob/main/YYYY-MM-DD/index.html`
and seeing images plus scored source links on that page.
