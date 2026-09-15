# CS283 Course Website

Course website for **CS283: Governing Artificial Intelligence: Law, Policy, and
Institutions** (Stanford) — taught **every fall** to both **undergraduate and
law students**. Built with **Jekyll** and hosted on **GitHub Pages**.
(`site.title` holds the full title; `site.short_title` = `CS283` for tab
suffixes.)

- Repo: `CS-AI-Governance/cs-283-website`
- Live URL: https://cs-ai-governance.github.io/cs-283-website/
- Local preview (requires Ruby 3.3 — see below):
  `export PATH="/opt/homebrew/opt/ruby@3.3/bin:$PATH" && bundle exec jekyll serve`
  → http://localhost:4000/cs-283-website/

## Design basis & license (IMPORTANT)

- **Site design** is adapted from MIT's **Missing Semester**
  (`github.com/missing-semester/missing-semester`, CC BY-NC-SA 4.0): the Jekyll
  layouts, includes, `assets/css/main.css` + `syntax.css` (re-themed), lecture
  template, sidenotes, and nav.
- **Course calendar** (the Schedule page) is adapted from **Just the Class**
  (`github.com/kevinlin1/just-the-class`, MIT): the `_modules` collection + a
  definition-list `date : topic : materials` format. Its CSS was re-implemented
  standalone (`assets/css/calendar.css`) — we do **not** depend on Just the Docs.
- Because Missing Semester is ShareAlike, **this site is licensed CC BY-NC-SA 4.0**
  (`LICENSE`), with attributions in `NOTICE`, the `/license/` page, and the footer.
  Keep those intact.

## Working agreement (IMPORTANT)

- **Content and bespoke design are done collaboratively, driven by human input.**
  Apply only design changes the user explicitly requests; do not invent content or
  extra styling. Collection docs (`_modules/*`, `_2026/*`) are clearly-labeled
  **placeholders**, not real course content.

## Theme tokens (defined in `assets/css/theme.css`)

- `--cardinal: #8C1515` (Stanford Cardinal) — nav bar, links, accents.
- `--cardinal-tint: rgba(140,21,21,.15)` — highlights, tinted labels.
- `--cardinal-light: #E8746F` — dark-mode accents.
- `--cream: #FEFFED` — page background.
- Fonts (loaded in `_includes/head.html`): **Courier Prime** (nav bar), **Lato**
  (all headings/titles — bold, cardinal-colored — plus body), Source Code Pro
  (code — TBD). Playfair Display is no longer used. `main.css`/`calendar.css`
  reference the tokens above.

## Structure

- `_config.yml` — `baseurl: /cs-283-website`; `title` (full course title) +
  `short_title: CS283`; `current_year: 2026`; kramdown/GFM; `future: true`
  (lecture/module dates are in the future at build time — required or their pages
  are not written); collections + layout defaults.
- `_layouts/` — `default` (shell, sets `body.layout-<layout>`), `page`, `lecture`
  (two-column: lecture + readings), `module` (JtC calendar).
- `_includes/` — `head`, `nav`, `footer` (attribution), `readings` (the lecture
  readings box), `video`/`scaled_*` helpers.
- `assets/css/` — `theme` (tokens), `main` (adapted MS + home/assignment styles),
  `syntax` (Rouge), `calendar` (JtC modules), `lecture` (lecture grid, readings
  ledger, `/lectures/` index). `assets/js/sidenotes.js`. (Renamed from `static/`.)
- `assets/documents/` — source material, currently the F26 syllabus PDF. **Not
  linked from the site**: it still carries internal to-dos and `XXX` due dates.
- Pages (`layout: page`) live in `pages/` — each declares its own `permalink`, so
  the folder is cosmetic (Jekyll renders front-matter files by permalink from any
  dir, no collection needed): `pages/assignments.md`, `sections.md`, `resources.md`,
  `lectures.md` (lists the `_2026` collection), `license.md`, `schedule.md`. The
  home page `index.md` (`/`) and `404.html` stay at the repo root.
- `pages/schedule.md` (`/schedule/`) renders one 4-column table (date · lecture ·
  slides · deadlines) from `site.modules | where: "year", site.current_year`;
  each module contributes a `<tbody>`. Pages needing more than the 35rem measure
  set `wide: true` in front matter (see `body.is-wide` in `main.css`).
- Collections: `_modules/` (the calendar's thematic units, `output: false`, needs
  `year` + `order`), `_2026/` (lecture pages, `output: true`, `layout: lecture`).

## Conventions

- **All internal links must use `{{ '/path' | relative_url }}`** (and `doc.url |
  relative_url`). MS/JtC upstream used root-absolute paths that 404 under our
  `/cs-283-website` baseurl — always route through `relative_url`.
- New offering next fall: add a `_2027/` collection (mirror the `_2026` config +
  defaults), give new `_modules` docs `year: 2027`, and bump `current_year`.
- **Lecture readings live in front matter**, not prose: each `_2026/*.md` carries
  a `readings:` map with `required:` / `supplementary:` lists of
  `{authors, year, title, venue, pages, url}` (all optional but `title`).
  `_includes/readings.html` renders them and sums each group's stated `pages`
  into the header total. `readings_tbd: true` renders an explicit TBD box for a
  lecture the syllabus has not filled in yet. Page counts and citations come
  from the instructors verbatim — **never invent a `url:` or a page count.**
- **Course units, not weeks**: the calendar is grouped by the *thematic units* of
  the instructors' course map (Course Introduction, Technical Foundations,
  Individual Risks, Societal Risk, National & International Approaches to AI
  Governance, The AI Economy, Living with AI, Outlook) — **not** by calendar week,
  and the units are uneven (1 to 4 lectures each). Each `_2026/*.md` carries
  `unit:` (1–8) + `unit_title:`; `_layouts/lecture.html` prints the title alone
  and `pages/lectures.md` groups by it. There is deliberately no week number
  anywhere on the site. One `_modules` doc per unit, `order:` matching `unit:`.
- **Lecture nav titles**: the hover dropdown in `_includes/nav.html` shows each
  lecture's `nav_title:` (a short form, e.g. `AI Agents` for L3), falling back to
  `title` when it is absent. `/lectures/`, `/schedule/`, and the lecture pages
  themselves all keep the full syllabus `title`. New lectures should carry both.
- **`_modules` docs hold no prose** — just `title`/`year`/`order` and a `rows:`
  list referencing lectures by number (`- lecture: 11`), plus `- section: true`
  and `- note: "…"` rows. `_layouts/module.html` looks each one up in the `_2026`
  collection, so a lecture's date and title are never written twice. A unit may
  span several calendar weeks, so rows are listed in date order and a
  `- section: true` row goes wherever that week's Thu/Fri section falls.
  Per-lecture `slides:` (URL) and `deadlines:` feed the schedule's last two
  columns. `deadlines:` is a **list** of `{label, date}` so one lecture can carry
  more than one badge (L19 closes both the final project and the law paper); the
  `date` (e.g. `Fri Oct 16`) is a separate key so the layout can wrap it in
  `<strong>` — only the date is bold inside a badge. Give both keys even when the
  deadline falls on the lecture's own day. Labels use
  `.label .label-due` / `.label .label-section` (styled in `calendar.css`);
  `.label-due` uses `--cardinal-wash`, one step stronger than the
  `--cardinal-tint` on `.label-section`.
- CSS/JS `<link>`/`<script>` tags in `head.html` carry a `?v={{ site.time | date:
  '%s' }}` cache-buster so each Pages build serves fresh assets (Pages sets
  `max-age=600` on assets). Keep new local assets on that pattern.

## Local Ruby

Use **Ruby 3.3** (`brew install ruby@3.3`, keg-only) to match GitHub Pages'
build (`github-pages` 232 / Jekyll 3.10). Prepend `/opt/homebrew/opt/ruby@3.3/bin`
to `PATH` before bundler. Newer Rubies (3.4+/4.x) drop stdlib libs and
`String#tainted?` that the Pages-pinned Jekyll needs. The `Gemfile` also declares
`csv`/`base64`/`bigdecimal`/`logger` for forward safety.

## Deployment

GitHub Pages builds from `main` (root). Push → auto rebuild. Poll with
`gh api /repos/CS-AI-Governance/cs-283-website/pages/builds/latest -q .status`.

## Content status (Fall 2026, from `assets/documents/F26 AIGov Syllabus.pdf`)

Populated from the syllabus: home (description, logistics, four instructor bios),
`/schedule/` (8 units, 19 lectures), `/lectures/` + 19 lecture pages,
`/assignments/`, `/sections/`, `/resources/`.

**The syllabus PDF is superseded.** The instructors issued an updated course map
that renumbered and regrouped most of the term: the old weekly grouping was
replaced by 8 thematic units, AI Agents moved to L3, AI Evaluations to L4, the
separate Privacy and Copyright lectures merged into L6, AI Harms to L7, AI &
Democracy to L8, AI Infrastructure & Energy to L9, and "Human in an AI Age" to
L17. Treat the PDF as history; the map and the instructors' direct input are the
source of truth. Readings are being replaced lecture by lecture, with URLs, on
the instructors' schedule.

Known gaps — these render as **TBD/TBA** on the site and should not be filled in
by guessing:

- [ ] **Lecture 18 (Mon Nov 30) has no topic at all** — the course map reserves
      the slot and leaves it blank. The page is `ready: false` so `/lectures/`
      lists it without a link.
- [ ] **Lecture 6** (AI, Copyright, Creativity, and Privacy) needs a merged
      reading list. The two superseded lists it was built from are preserved as
      commented YAML inside `_2026/06-copyright-creativity-privacy.md`; delete
      them once the real list lands.
- [ ] Lecture 10 has no summary and no readings (`readings_tbd: true`).
- [ ] Lecture 7 (AI Harms) still carries the reading list and the
      `readings_note: "Assigned in previous weeks."` from when it sat in Week 9,
      and two of its readings are antitrust papers that now sit oddly against
      L15. Revisit when L7's readings are updated.
- [ ] Lecture 14 — Geopolitics and Global AI Governance — is not in the syllabus
      PDF; the instructors added it. (Lecture 16 exists in the PDF's body but is
      missing from its TOC.)
- [ ] Slide decks — every `/schedule/` row shows an inert `[slides]` placeholder
      until a lecture gets a `slides:` URL in its front matter.
- [ ] Reading URLs — the syllabus links only two of ~113 citations.
- [x] Assignment due dates — all set from the updated course map and live on
      `/assignments/`, each with a `deadlines:` badge on the nearest preceding
      lecture in `_2026/`: Milestone 1 Fri Oct 16 → L7, law paper outline Mon
      Oct 19 → L8, public comment Fri Oct 23 → L9, Milestone 2 Fri Oct 30 → L11,
      Milestone 3 Fri Nov 6 → L13, law R-credit draft Mon Nov 16 → L16, and both
      Milestone 4 Fri Dec 4 and the law paper Sat Jan 3 → L19. The course map
      calls the public comment assignment the "RFC"; the site keeps the fuller
      name it already used.
- [ ] Teaching assistants; learning objectives (heading with no bullets);
      section topics, locations, and leaders; office hours for Reuel and Koyejo.
- [x] Favicon — `assets/img/favicon.png`, a 168×168 crop of the white Stanford
      mark on cardinal, wired into `head.html` as `icon` + `apple-touch-icon`.
      Other branding assets under `assets/` are still open.
- [ ] Code/monospace font choice; custom Stanford domain — later.
