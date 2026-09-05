# shikhar1729.github.io

Personal research website. Built with [Jekyll](https://jekyllrb.com/) and the
[al-folio](https://github.com/alshedivat/al-folio) theme, deployed to GitHub Pages
by GitHub Actions.

Live at **https://shikhar1729.github.io**.

---

## How deployment works

Push to `main`. The `Deploy site` Action builds the site and pushes `_site` to the
`gh-pages` branch, which GitHub Pages serves. Nothing else to run.

Two repo settings make that work, and they are already set:

- **Settings → Pages** → Source: _Deploy from a branch_, branch `gh-pages`, folder `/ (root)`.
- **Settings → Actions → General** → Workflow permissions: **Read and write**. The deploy,
  CV-render, and citation Actions all commit back to the repo.

### Moving to a custom domain later

1. Create a `CNAME` file containing the bare domain — no `https://`, no trailing slash.
2. Set `url:` in `_config.yml` to `https://thatdomain`. Leave `baseurl:` blank.
3. At your registrar, point the apex domain at GitHub's four Pages IPs:

```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
CNAME www  shikhar1729.github.io.
```

4. In **Settings → Pages**, enter the domain and tick **Enforce HTTPS** once the certificate
   provisions (a few minutes to an hour).

GitHub then redirects `shikhar1729.github.io` to the new domain, so existing links keep working.

---

## Editing content

| What                       | Where                                                                                                                                          |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| Bio and landing page       | `_pages/about.md`                                                                                                                              |
| Publications               | `_bibliography/papers.bib` — set `selected={true}` to surface a paper on the landing page                                                      |
| CV (and the CV PDF)        | `_data/cv.yml` — the `Render a CV` Action regenerates `assets/rendercv/rendercv_output/Shikhar_Shiromani_CV.pdf` on every push that touches it |
| News items                 | `_news/*.md` — one file per item, filename date sorts them                                                                                     |
| Service, reviewing, awards | `_pages/service.md`                                                                                                                            |
| Blog posts                 | `_posts/*.md`. The `notes` page is at `/notes/` but hidden from the navbar; set `nav: true` in `_pages/blog.md` to show it                     |
| Site title, socials, nav   | `_config.yml`, `_data/socials.yml`                                                                                                             |

### Adding a paper

Append a BibTeX entry to `_bibliography/papers.bib`. Useful al-folio fields beyond standard BibTeX:

```bibtex
@article{key2026,
  abbr        = {ICLR},        % badge shown on the left
  bibtex_show = {true},        % adds a "Bib" button
  selected    = {true},        % show on the landing page
  arxiv       = {2601.00000},  % adds an arXiv button
  award       = {Oral},        % highlighted award line
  abstract    = {...},         % expandable abstract
  code        = {https://...}, % adds a Code button
  title       = {...},
  author      = {Last, First and Other, Person},
  year        = {2026}
}
```

---

## Running locally (optional)

```bash
bundle install
bundle exec jekyll serve
# http://localhost:4000
```

Requires Ruby 3.3+. You do not need this to publish; the GitHub Action builds the site for you.
