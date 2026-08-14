# ECON 4210 — Economics of Climate Change

Course website. Static HTML, served from GitHub Pages at
<https://www.caseyjwichman.com/econ4210/>.

Scope is the weekly schedule, the readings, and the slides. Course policies
live in the syllabus PDF and are not repeated here. Assignments, grades, and
book-chapter readings stay on Canvas.

No build step. The HTML files are both the source and what gets served.
Editing one and pushing puts the change live. There is no way to publish a
stale page by forgetting to run something.

## Contents

| Path | |
|:--|:--|
| `index.html` | The schedule. Everything except styling lives here. |
| `materials.html` | Flat list of every posted slide deck and reading. Builds itself. |
| `style.css` | Shared by both pages. Palette is at the top. |
| `readings/` | Journal-article PDFs, named `author-year.pdf`. Book chapters do not go here — Canvas only. |
| `slides/` | Lecture PDFs, named `classNN.pdf`. |
| `econ4210_fall2026_syllabus.pdf` | Full syllabus. Compiled in `syllabus/`, copied here. |
| `econ4210_fall2026_public.pdf` | Public syllabus posted under the USG rule. Compiled in `syllabus/`, copied here. |

## Structure

Each week is a `<details>` block. Each class inside it is an `<article>` holding
two buckets: slides and readings.

```html
<details class="week" id="week4" open data-from="2026-09-14" data-to="2026-09-16">
  <summary><span class="wk">Week 4</span><span class="span">Sep 14–Sep 16</span></summary>

  <article class="meeting">
    <h3><time>Mon Sep 14</time><span class="cn">06</span><span class="topic">Property rights and the commons</span></h3>

    <!-- uncomment when the deck is posted -->
    <!-- <div class="bucket slides"><span class="tag"><svg class="ic"><use href="#i-slides"/></svg>slides</span><a class="chip" href="slides/class06.pdf">class06.pdf</a></div> -->

    <div class="bucket reading">
      <span class="tag"><svg class="ic"><use href="#i-paper"/></svg>readings</span>
      <ul>
        <li><strong>K&amp;O</strong> Chapter 3 — Canvas</li>
      </ul>
    </div>
  </article>
</details>
```

The two buckets are colour-coded by their left rule: moss for slides, teal for
readings. Exam days are `<article class="meeting">` with a
`<span class="badge exam">exam</span>` in the `<h3>` and no buckets.

## The materials page

`materials.html` lists everything in `slides/` and `readings/`. It is not
hand-maintained: at load time it reads both folders through the GitHub contents
API and prints what is actually there, with file sizes. Adding a PDF to either
folder puts it on that page with no further edit.

The repository name is set in one variable at the top of the script, `REPO`.
That is the only thing to change if the repo is ever renamed. The API is
unauthenticated, which is fine at course traffic; if a request fails the page
falls back to a direct link to the GitHub folder view.

This is separate from the schedule. A reading only appears in a class on
`index.html` when its `<li>` is written there.

## Which week is open

Every week carries `open` in the markup, so with scripting disabled the whole
schedule is visible. The script at the bottom of the file closes all but one.

It compares today's date against each week's `data-from` and `data-to`, opens
the match, tags it `this week` in the summary, highlights its number in the nav,
and scrolls to it. Between meetings or before the term it opens the next week
that has not finished; after the term, the last one. A `#week9` hash in the URL
overrides the date.

The attributes are the only thing driving this. Nothing needs maintaining
during the semester.

## Editing

**Post slides.** Every class already has its slides bucket written and
commented out, with the filename filled in. Drop the PDF into `slides/` and
delete the `<!--` and `-->` around it.

**Add a reading.** Copy a neighbouring `<li>` inside the readings bucket and
edit it.

```html
<li>Author Name (2026). “Title of the paper.” <em>Journal Name</em>.
    <a class="dl" href="readings/author-2026.pdf">PDF</a></li>
```

`class="dl"` is the PDF chip, `class="ext"` the external-link chip. Book
chapters get a plain `<li>` ending in `— Canvas` and no file in the repository.

**Write ampersands as `&amp;`** and quotation marks as `“ ”`. Everything else is
plain text.

Reading PDFs are named `<firstauthor>-<year>.pdf` with no class prefix, so
moving a reading to a different class does not mean renaming the file. Slide
PDFs are `class<NN>.pdf`, because a deck belongs to a lecture and the number is
the join between the deck, the schedule, and the syllabus table.

Links must match filenames exactly, case included.

Slides go up before class, clean. Annotated Notability copies stay off the
site.

`<!-- -->` comments do not display. Two carry instructor notes from the Fall
2025 postmortem: the policy-in-practice expansion (class 17) and the merged
uncertainty lecture (class 23).

## Schedule changes

Class numbers belong to the lecture, not to the calendar slot. Class 6 is
Property rights and the commons and its deck is `class06.pdf` whatever date it
lands on. Dates belong to the calendar and do not move. A cancellation or a
delay therefore changes which date a class falls on, and nothing renumbers.

The semester has no slack beyond class 27: 28 classes fill 28 Mon/Wed slots,
four of them exams. Cancelling a lecture means cutting, merging, or dropping a
topic. Exam dates are in the syllabus and should move only as a last resort.

To push everything back one meeting:

1. In the cancelled meeting's `<article>`, delete both buckets and change the
   `<h3>` to the no-class pattern:
   `<h3><time>Mon Sep 14</time><span class="off-label">Cancelled</span></h3>`,
   then set `class="meeting off"` on the article.
2. Working bottom-up, move each `<h3>`, its commented slides bucket, and its
   readings bucket down into the next `<article>`. Bottom-up, because top-down
   overwrites blocks not yet moved. Select the lines and hold Option+Down.
3. Delete the block left stranded at the end.
4. Commit and push.

The `data-from` and `data-to` attributes on each week stay as they are. They
describe the calendar, which has not changed.

## Constraints

`syllabus/econ4210_fall2026_public.tex` is the syllabus posted publicly under
the USG rule. It stays near-constant across years. Course material does not go
in it.

Year-to-year changes go in `index.html` and
`syllabus/econ4210_climate_fall2026.tex`.

Lecture decks are Keynote, exported to PDF for presenting; sources in
`_teaching/FALL2026/ECON4210/slides/`. Decks are being converted to PowerPoint
one at a time through the semester, but the site only ever sees the PDF.

Only journal-article PDFs are posted in `readings/`. Book chapters (Keohane &
Olmstead, Pindyck, Nordhaus, Wagner & Weitzman) are under copyright and are
posted on Canvas for enrolled students only.

No `CNAME` file in this repository. The `cjwichman.github.io` user site already
carries one, and it covers project pages.

## Styling

`style.css` is shared with nothing — it is a copy of the ECON 7102 stylesheet
with the palette changed. The palette lives in the `:root` block at the top.
The primary accent for this course is teal (`--clay: #2f6d78`); 7102 uses clay.
Changing a course colour means changing one variable.

| Variable | Use |
|:--|:--|
| `--paper`, `--card` | Backgrounds |
| `--ink`, `--body`, `--mute`, `--faint` | Text, darkest to lightest |
| `--clay` | Readings bucket, section labels, current week (teal here) |
| `--moss` | Slides bucket |
| `--slate` | Links, class-number chips |
| `--sand` | Due badges |

Metadata is set in `--mono` and prose in `--sans`. Dates, class numbers,
filenames, and labels are all mono, which is what makes the page read as a
schedule rather than an essay.

The two SVG glyphs are defined in a hidden `<svg>` at the top of `<body>` on
each page and referenced with `<use href="#i-slides">` and
`<use href="#i-paper">`.
