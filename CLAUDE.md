# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

Personal research website for **Shikhar Shiromani**. Jekyll + the
[al-folio](https://github.com/alshedivat/al-folio) v1.x starter, deployed to GitHub Pages
by GitHub Actions.

## Commands

```bash
bundle install                     # Ruby 3.3+; every al_* / jekyll-* gem is version-pinned
bundle exec jekyll serve           # http://localhost:4000
bin/cibuild                        # what CI effectively runs: bundle exec jekyll build
bin/al-folio <subcommand>          # al_folio_upgrade gem CLI (theme upgrade / doctor)
bin/setup-python-deps              # jupyter + nbconvert, only for jekyll-jupyter-notebook

npm ci && npm run lint:prettier    # the Prettier action runs this on every push and PR
npm run format                     # prettier . --write — run before pushing

# Reproduce the two committing Actions locally (both need `pip install -r requirements.txt`)
rendercv render _data/cv.yml --settings assets/rendercv/settings.yaml
python bin/update_scholar_citations.py
```

There are no tests. `prettier . --check` is the only lint gate, and it is a separate workflow
from the deploy, so a formatting failure does not block the site — but it does redden the
commit. `.prettierignore` already excludes `_data/citations.yml` (script-generated).

### Local builds need real setup

The machine's default Ruby is 2.6 and the Gemfile needs 3.3+. `imagemagick.enabled: true` in
`_config.yml` also needs `convert` on PATH, or the responsive-image step fails. `Gemfile.lock`
is gitignored, so `bundle install` resolves fresh every time. If a local preview is not worth
that setup, push and let the `Deploy site` Action build — that is the authoritative build.

## Architecture

al-folio v1.x is a **thin starter**. Layouts, includes, Sass and Liquid tags live in the
`al_*` gems (`theme: al_folio_core` in `_config.yml`), not in this repo — which is why
`_layouts/`, `_includes/`, `_sass/` and `assets/tailwind/` do not exist here. If a fix seems
to need one of those, it almost certainly belongs in `_config.yml` or in content instead.
Shadowing a gem file locally works but means maintaining it forever, so treat it as a last
resort. Feature switches live under `al_folio:` and `enable_*` in `_config.yml`; the style
engine is Tailwind 4 with preflight off.

`baseurl` is blank because this is a user site on a custom domain. Do not set it, and do not
pass `--baseurl` — upstream al-folio docs say `/al-folio`, which is correct for _their_ demo
repo and wrong here.

### Build pipeline and two traps

`Deploy site` runs `jekyll build` → `purgecss -c purgecss.config.js` → push `_site` to the
`gh-pages` branch. Both post-processing steps have already caused real breakage, and both
fixes are load-bearing:

- **`jekyll-minifier.compress_css: false` must stay false.** cssminify2 mangles Tailwind v4
  spacing tokens inside `calc()`, turning `var(--spacing)` into `var( -  - spacing)` and
  breaking every spacing utility (a broken `.fixed-top` navbar, for one). CSS is already
  minified upstream. JS minification is delegated to jekyll-terser instead.
- **PurgeCSS only scans static HTML.** Any class injected at runtime must be added to
  `safelist` in `purgecss.config.js`, or its rules are stripped from production only and the
  page looks fine locally. medium-zoom's overlay classes are already listed for this reason.

## Actions

| Workflow               | Trigger                                                  | Effect                                                              |
| ---------------------- | -------------------------------------------------------- | ------------------------------------------------------------------- |
| `deploy.yml`           | push to `main` touching content/assets/config            | builds and pushes `_site` to `gh-pages`                             |
| `prettier.yml`         | every push and PR                                        | `prettier --check`; on failure uploads an HTML diff                 |
| `render-cv.yml`        | push touching `_data/cv.yml` or `assets/rendercv/*.yaml` | regenerates the CV PDF and **commits it back**                      |
| `update-citations.yml` | cron Mon/Wed/Fri                                         | rewrites `_data/citations.yml` from Scholar and **commits it back** |

The two committing workflows need Settings → Actions → Workflow permissions set to
**Read and write**. `update-citations.yml` is capped at a 90-second timeout and is allowed to
fail quietly — Scholar rate-limits, and a failed run just leaves the old counts in place.
README-only changes do not trigger a deploy; `CLAUDE.md` is excluded from the Jekyll build.

## Where things live

| Change                                     | File                                                     |
| ------------------------------------------ | -------------------------------------------------------- |
| Bio / landing page                         | `_pages/about.md`                                        |
| Publications                               | `_bibliography/papers.bib`                               |
| Reviewing, awards, mentorship, fellowships | `_pages/service.md`                                      |
| CV content (drives the generated CV PDF)   | `_data/cv.yml`                                           |
| News items                                 | `_news/YYYY-MM-DD-slug.md`, one per item, `inline: true` |
| Socials, Scholar ID, CV link               | `_data/socials.yml`                                      |
| Venue colors and links for `abbr` badges   | `_data/venues.yml`                                       |

`_posts/` does not exist yet, so the `/notes/` blog page (`_pages/blog.md`) is empty and
hidden from the navbar. Set `nav: true` there once the first post lands.

## Rules that matter

**Never invent or upgrade a publication venue.** Every entry in `papers.bib` was
cross-verified against Gmail acceptance emails, PMLR, Crossref/IEEE and the venue sites.
Google Scholar had six of the ten wrong. Specifically:

- Linear Predictability is a **SELVA @ ACL 2026 oral (1 of 4)**, not a preprint.
- Where Reliability Lives is the **Mechanistic Interpretability Workshop at ICML 2026**, not ICLR.
- ProMoral-Bench is **NeurIPS 2025**, not 2026.
- COMPASS was accepted at **five** AAAI-26 workshops; the oral was LaMAS.
- ChameleonBench is archival: **PMLR Vol. 304, pp. 1006–1021**.
- The 2022 skin-lesion paper is **ICAC3N**, not ICACCS.

Work still under review keeps `abbr = {Preprint}` and no `booktitle`. Today that is
A False Average (BlackboxNLP 2026), SAGE (NeurIPS 2026), and Hypocrisy Gap. Promote an
entry only when an acceptance actually lands.

Of the recent AI-safety work, only ChameleonBench (PMLR) and SELVA are archival; the rest are
non-archival workshops, so cite those by workshop plus date rather than implying proceedings.
The three older IEEE papers (ICCSS 2025, ICIDCA 2023, ICAC3N 2022) are archival proceedings.

**Do not add self-reported metrics** (citation counts, h-index) to page content. The
`Update citations` Action populates `_data/citations.yml` from Scholar automatically.

### Adding a paper

```bibtex
@inproceedings{key2026,
  abbr        = {ICML-W},      % badge in the left margin; color from _data/venues.yml
  bibtex_show = {true},        % adds a "Bib" button
  selected    = {true},        % also show on the landing page
  arxiv       = {2601.00000},  % adds an arXiv button
  award       = {Oral},        % highlighted award line
  additional_info = {...},     % free-text line, e.g. "Under review at NeurIPS 2026."
  abstract    = {...},
  title       = {...},
  author      = {Last, First and Other, Person},
  booktitle   = {Workshop Name at VENUE 2026, City},
  year        = {2026},
  month       = {July}
}
```

Any key listed in `filtered_bibtex_keywords` (`_config.yml`) is consumed by the theme and
hidden from the rendered BibTeX. Seven entries are currently `selected` — keep that list
short, it is the landing page.

## Still to fill in

`YOURUSERNAME` in `_data/socials.yml` and `_data/cv.yml`; `url:` in `_config.yml`; the `CNAME`
file (still `yourdomain.com`); and `assets/img/prof_pic.jpg` is a placeholder monogram, not a
photo. `giscus.repo` is empty, so post comments are inert until it is set.
