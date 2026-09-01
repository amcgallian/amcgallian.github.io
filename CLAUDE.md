# Portfolio Site — CLAUDE.md

Read this fully before touching anything. This repo is Andrew McGallian's personal portfolio site,
prepped for GitHub Pages on 2026-09-01. It is NOT yet published — that's the first job.

## What this is

A static site (no build step, no framework — plain HTML/CSS, `/style.css` shared across pages) built
around real, verified projects from Andrew's MS in Environmental Science and GIS work at the
University of Chicago. Fonts: DM Serif Display + IBM Plex Sans/Mono, loaded via Google Fonts CDN.

## The one rule that matters more than anything else

**Every claim on this site must be something Andrew can personally defend if a recruiter asks about
it.** This site went through a full audit on 2026-09-01 specifically because it *wasn't* meeting that
bar — see "What was wrong and what was fixed" below. Do not add polish, numbers, or technical detail
that isn't traceable to something Andrew has confirmed or that exists in his own code. If you're
tempted to make a bullet more impressive by inferring what a system "must" do, stop — that's exactly
the mistake that was already made once here (see the DuckDB incident below) and once on his resume.

If Andrew asks you to add something and you can't verify it from his files, ask him directly rather
than writing a plausible-sounding version.

## What was wrong and what was fixed (2026-09-01)

This site pre-existed and was mostly AI-generated without a fact-check pass. Found and fixed:
- **Wildfire model page said "Pacific Northwest."** His actual script (`ccc_landsat_processing.py`,
  on his `FELLOWSHIP` external drive) references a Contra Costa County, CA boundary file. Fixed
  everywhere.
- **The cloud-seeding capstone page ("Make It Rain") described an entirely different project** — a
  CNN autoencoder on NEXRAD radar data with a fabricated "Key Result" and a dead GitHub link. His
  actual MS capstone (ENSC 36300) was a literature synthesis and quantitative reanalysis of historical
  cloud seeding studies. Rewrote to match; the page now says it's still being expanded rather than
  claiming a finished result that isn't real.
- **The Chicago Environmental Atlas card claimed DuckDB** for a storage-routing feature that exists in
  the code, but Andrew couldn't explain when asked directly (this project was built with heavy AI
  assistance and he doesn't remember the implementation details). Removed. **Do not re-add DuckDB, a
  "three-tier backend," or the "six-endpoint REST API" framing unless Andrew has confirmed he can
  explain it.**
- **A "Live demo" badge and "Launch app" button** claimed the atlas was live. It isn't — the domain
  (`chicago-environmental-atlas.com`) returns HTTP 530, the tunnel/laptop hosting it is off, and
  Andrew currently doesn't want to pay for hosting. Don't re-add a live-demo claim until it's actually
  live and verified reachable.
- **`/projects/chicago-atlas/` was linked from the homepage and didn't exist.** Built it, using only
  claims traceable to the code and README on the `FELLOWSHIP` drive.
- **TKAP Tools (his QGIS plugin) was entirely absent** despite being his strongest, fully verified,
  publicly working project — published, live plugin feed returns HTTP 200, real users (an
  archaeological field team). Added as the new flagship.
- **North Syrian Inscriptions Map (CoryMap) was entirely absent.** Added — verified from the
  `FELLOWSHIP` drive: `CoryMap/pipeline.ipynb`, ~72 findspots matched against a 2,910-point KMZ
  gazetteer, 600 DPI output in colour and greyscale. **2026-09-01 correction:** the map was
  commissioned by Cory Crawford (Ohio University) for one of his publications — TKAP is where Andrew
  and Crawford met, not the commissioning project. Card/page copy corrected to credit Crawford, not
  TKAP, as the recipient.
- Removed 2 dead "GitHub →" buttons (dissertations-viz, gis-assistant) — no public repo exists for
  either project. Don't add a link back unless a real public repo exists.
- Wired up the real headshot and CV in `about.html` (both files already existed in `assets/`, unused).

## Known open items — do these before or shortly after publishing

1. **`assets/cv.pdf` is stale.** It predates corrections made to Andrew's resume on 2026-09-01
   (graduate GPA is 3.86, not what's on the old CV; Mansueto Institute dates are Jun 2024 – Jul 2025).
   Don't let anyone download it until it's rebuilt. The current source of truth for his resume content
   is `../master-resume.md` (one level up, in the `Job Search` folder) — pull corrected facts from
   there, not from the old CV.
2. **The dissertation-viz page's NLP numbers are unverified.** It cites "4,068 records" via spaCy NER
   with a country breakdown. No code for this specific analysis was found on the `FELLOWSHIP` drive
   during the audit — it's plausible (matches the ambition in his original fellowship proposal) but
   unconfirmed. Ask Andrew to confirm the numbers are real before treating this page as fully trusted.
   Its "to be added" figure placeholders are honest, not a bug — leave them until real figures exist.
3. ~~This repo needs to be pushed and Pages enabled.~~ **Done 2026-09-01.** The site is live at
   `https://amcgallian.github.io`. See "Publishing" below for what actually happened — it initially
   went out under the wrong repo name and had to be fixed.

## Publishing — done, but read this if anything looks broken again

**The repo must be named exactly `amcgallian.github.io`.** Every internal link on this site is an
absolute path (`/style.css`, `/projects/`, etc.), built assuming it serves from a domain root. Any
other repo name means GitHub Pages serves it at `amcgallian.github.io/<reponame>/` instead, and every
link on the site breaks (unstyled page, default browser link colors — that's the tell).

**This actually happened on 2026-09-01:** the repo was first created as `amcgallian/portfolio-site`,
which broke every link on the live site. Fixed by renaming the repo in place (GitHub Settings →
General → Repository name → `amcgallian.github.io`) rather than deleting/recreating — this preserves
history and GitHub auto-detects the user-site naming pattern. The local git remote was then repointed
with `git remote set-url origin https://github.com/amcgallian/amcgallian.github.io.git`. Note: unlike
the repo page itself, Pages URLs do **not** auto-redirect from the old name — `/portfolio-site/` now
404s, so that URL should never be given out anywhere (resumes, LinkedIn, etc.) — the correct link is
`https://amcgallian.github.io`. Added a root `.nojekyll` at the same time since Pages now serves from
the domain root — cheap insurance against Jekyll processing this static site unexpectedly.

Original steps, for reference if the repo ever needs to be recreated from scratch:

```bash
# 1. Create the repo at github.com/new — name: amcgallian.github.io, public, no README
# 2. From this folder:
git add -A
git commit -m "Initial portfolio site"
git branch -M main
git remote add origin https://github.com/amcgallian/amcgallian.github.io.git
git push -u origin main
# 3. In repo Settings → Pages, confirm: Deploy from a branch, main, /(root). Usually automatic.
# Live in 1-2 min at https://amcgallian.github.io
```

## After it's live

Tell Andrew — or if you're continuing his job search work, update these files in the sibling
`Job Search/` folder to point at the new URL instead of his old `sites.google.com/uchicago.edu/...`
Google Site (which is on his university Google Workspace and will likely die when alumni access
lapses):
- `../master-resume.md` (contact block)
- `../jobfeed/resume_data.py` (`CONTACT["line2"]`) — then rebuild:
  `../jobfeed/.venv/bin/python ../jobfeed/build_resumes.py`
- `../linkedin-profile.md` (Featured section + About)

## Recording the atlas (in place of hosting it)

Andrew doesn't want to pay for a server for `chicago-atlas` right now. The plan is a screen recording
instead — run it locally (`cd /Volumes/FELLOWSHIP/chicago-atlas && python server.py`,
`localhost:8000`), record ~60 seconds of the timeline scrubbing, a layer toggle, and a polygon draw,
and drop it at the top of the project's own README on GitHub, plus embed or link it from
`/projects/chicago-atlas/` on this site once you have it.

## File structure

```
index.html              — homepage, showcase section (6 of 7 projects, curated)
about.html               — bio, headshot, CV download
projects/index.html      — full project list (7), split into Flagship + Core Projects
projects/<slug>/index.html   — one page per project
research/, courses/       — same card pattern, coursework and lab positions
style.css                 — shared stylesheet, CSS custom properties for theming
assets/                   — images, PDFs (headshot.jpg, cv.pdf, posters)
```

Adding a new project = new `projects/<slug>/index.html` (copy an existing one as a template — 
`projects/corymap/index.html` is a clean, simple example) + a card block on `index.html` and
`projects/index.html` + bump the relevant `section-count` span.
