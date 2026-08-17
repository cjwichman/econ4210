# Setup

Identical process to the ECON 7102 site. Staging copy lives in Dropbox at
`_teaching/FALL2026/ECON4210/website/`; the git working copy lives outside
Dropbox.

## Dependencies

GitHub Desktop, <https://desktop.github.com>. Nothing else. Any text editor
works, including github.com in a browser.

## Location

Keep the working copy outside Dropbox. Git and Dropbox manage the same
directory and corrupt each other's state.

`~/Documents/GitHub/econ4210` matches the 7102 arrangement. macOS gates
`~/Documents` under Privacy & Security → Files and Folders. If an editor throws
`EPERM`, either grant it Documents Folder access there, or move the repository
to `~/GitHub/econ4210`, which is not gated.

## First publish

1. Copy the contents of the Dropbox staging folder into the working copy.
2. GitHub Desktop → File → Add Local Repository → select the folder. It offers
   to create a repository. Accept. Name it `econ4210`. The folder already has a
   `.gitignore`, so leave those fields alone.
3. Publish repository. Uncheck *Keep this code private*. The first push runs
   about 90 MB and takes a few minutes.
4. On github.com: Settings → Pages → Source: *Deploy from a branch* → `main`
   and `/ (root)`. Save.
5. Load <https://www.caseyjwichman.com/econ4210/>.

Root, not `/docs`. There is no build output directory. `index.html` at the top
of the repository is the page.

The `cjwichman.github.io` user site carries a custom domain, so project sites
serve from `caseyjwichman.com` as well. `cjwichman.github.io/econ4210`
redirects there. Cite the `caseyjwichman.com` address. Do not add a `CNAME`
file to this repository.

A 404 after step 4 means Pages is pointed at the wrong branch or folder.

## Routine

1. Edit `index.html`.
2. GitHub Desktop: summary, Commit to main, Push origin.

Live about a minute later. To check the page first, double-click `index.html`
in Finder — it opens in a browser and renders exactly as it will once pushed,
because there is no build step between the two.

Small edits can be made on github.com without a local checkout: open
`index.html`, click the pencil, commit. Useful from a phone or a borrowed
machine.

## The syllabus PDF

`econ4210_climate_fall2026.tex` compiles in
`_teaching/FALL2026/ECON4210/syllabus/`. It is THE course syllabus: policies,
grading, exam dates, planned course topics, and the book list. It does not
contain the schedule or the reading list -- those live only in `index.html`,
so a schedule change is a one-file edit. Its PDF is the "Syllabus (PDF)" chip
on both pages, renamed `econ4210_fall2026_syllabus.pdf` in the repository.

After recompiling, copy the PDF into the repository, commit, push.

`econ4210_fall2026_public.tex`, in the same folder, is the bare-minimum
public syllabus the USG rule requires. It is entirely external to the site:
updated once a year and posted at
<https://syllabus.gatech.edu/sites/default/files/2026-04/econ4210_fall2026_public.pdf>.
Nothing from it enters the repository.

## Slides

Decks are Keynote, in `_teaching/FALL2026/ECON4210/slides/`. Export to PDF
(and to PowerPoint, deck by deck, for the textbook effort), copy the PDF into
`slides/` as `class06.pdf`, then uncomment that class's slide line in
`index.html`. The line is already written with the right filename.

Compress before posting if a deck runs large. GitHub caps single files at
100 MB, and several of the 2025 lecture PDFs exceed that. Preview: File →
Export, Quartz filter *Reduce File Size*, or export from Keynote at reduced
image quality. Aim for under ~25 MB so pages load quickly.

## Annual rollover

The repository is unversioned so the URL survives. The site shows the current
term only.

Freeze the previous term first. On github.com: Releases → Draft a new release →
Choose a tag → type `fall2026` → Create new tag → Publish release. The state as
taught stays browsable from the Releases page.

Then update dates and topics in `index.html`, including the `data-from` and
`data-to` attributes on each week, recompile the syllabus, swap its PDF in,
push. The public syllabus is refreshed separately at syllabus.gatech.edu and
normally needs only a date change.

The Canvas chip in both page headers points at the term's course shell
(`gatech.instructure.com/courses/<id>`). Canvas issues a new shell each
term, so update that ID at rollover -- it appears once in `index.html` and
once in `materials.html`.

## Failure modes

| Symptom | Cause |
|:--|:--|
| `EPERM` opening a file | macOS Privacy gating on `~/Documents`. See Location above. |
| Page looks broken after an edit | An unclosed tag. Open the file in a browser locally to see where it breaks. |
| A reading or slide link 404s | Filename in the link does not match the file. Case matters. |
| Every week collapsed and none open | The script failed. Weeks carry `open` in the markup, so this only happens if the markup was edited. |
| Push rejected, file too large | GitHub caps single files at 100 MB. Compress in Preview: File → Export, Quartz filter *Reduce File Size*. |
