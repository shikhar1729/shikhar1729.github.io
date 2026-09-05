# CLAUDE.md

Personal research website for **Shikhar Shiromani**. Jekyll + the
[al-folio](https://github.com/alshedivat/al-folio) v1.x starter, deployed to GitHub Pages
by GitHub Actions.

## Run it

```bash
bundle install                # Ruby 3.3+; the al_* gems are pinned in the Gemfile
bundle exec jekyll serve      # http://localhost:4000
```

`baseurl` is blank in `_config.yml` because this is a user site on a custom domain. Do not
set it, and do not pass `--baseurl` — upstream al-folio docs say `/al-folio`, which is
correct for *their* demo repo and wrong here.

## Where things live

| Change | File |
|---|---|
| Bio / landing page | `_pages/about.md` |
| Publications | `_bibliography/papers.bib` |
| Reviewing, awards, mentorship | `_pages/service.md` |
| CV content (and the generated CV PDF) | `_data/cv.yml` |
| News items | `_news/YYYY-MM-DD-slug.md`, one per item |
| Socials, Scholar ID, CV link | `_data/socials.yml` |

al-folio v1.x is a **thin starter**. Layouts, includes, Sass and Liquid tags live in the
`al_*` gems, not in this repo. If a fix seems to need `_layouts/`, `_includes/`, `_sass/`
or `assets/tailwind/`, it almost certainly belongs in config or content instead. Shadowing
a gem file locally works but means maintaining it forever, so treat it as a last resort.

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

Only ChameleonBench (PMLR) and SELVA are archival. Everything else is a non-archival
workshop, so cite by workshop plus date rather than implying proceedings.

**Do not add self-reported metrics** (citation counts, h-index) to page content. The
`Update citations` Action populates `_data/citations.yml` from Scholar automatically.

## Adding a paper

```bibtex
@inproceedings{key2026,
  abbr        = {ICML-W},      % badge in the left margin
  bibtex_show = {true},        % adds a "Bib" button
  selected    = {true},        % also show on the landing page
  arxiv       = {2601.00000},  % adds an arXiv button
  award       = {Oral},        % highlighted award line
  abstract    = {...},
  title       = {...},
  author      = {Last, First and Other, Person},
  booktitle   = {Workshop Name at VENUE 2026, City},
  year        = {2026},
  month       = {July}
}
```

Seven entries are currently `selected`. Keep that list short — it is the landing page.

## Actions

- `deploy.yml` — builds and pushes `_site` to the `gh-pages` branch on every push to `main`.
- `render-cv.yml` — regenerates the CV PDF from `_data/cv.yml` and commits it back.
- `update-citations.yml` — refreshes Scholar citation counts.

Both CV render and citation update commit to the repo, so Settings → Actions → Workflow
permissions must be **Read and write**.

## Still to fill in

`YOURUSERNAME` in `_data/socials.yml` and `_data/cv.yml`; `url` in `_config.yml`; the
`CNAME` file; and `assets/img/prof_pic.jpg` is a placeholder monogram, not a photo.
