# shikharshiromani.com

Personal research website. Built with [Jekyll](https://jekyllrb.com/) and the
[al-folio](https://github.com/alshedivat/al-folio) theme, deployed to GitHub Pages
by GitHub Actions.

---

## Before your first push: change these five things

| # | File | Line | Change to |
|---|------|------|-----------|
| 1 | `_config.yml` | `url:` | `https://yourdomain.com` (or `https://YOURUSERNAME.github.io` if you skip the custom domain) |
| 2 | `_config.yml` | `baseurl:` | Leave **blank** for a custom domain or a `<user>.github.io` repo. Only set it (e.g. `/website`) if the site lives in a project repo without a custom domain. |
| 3 | `CNAME` | whole file | Your domain, no `https://`, no trailing slash. **Delete this file entirely if you are not using a custom domain.** |
| 4 | `_data/socials.yml` | `github_username:` | Your GitHub username |
| 5 | `_data/cv.yml` | `social_networks` → GitHub `username:` | Your GitHub username |

Then replace `assets/img/prof_pic.jpg` with a real photo (square, ~600x600 or larger).

---

## Deploying

1. Create a repo named **`YOURUSERNAME.github.io`** (for a personal site) and push this directory to `main`.
2. Repo → **Settings → Pages** → set **Source** to **Deploy from a branch**, branch **`gh-pages`**, folder `/ (root)`.
   The `Deploy site` Action builds to the `gh-pages` branch on every push to `main`.
3. Repo → **Settings → Actions → General** → **Workflow permissions** → **Read and write permissions**.
   The deploy and CV-render actions both commit back to the repo.
4. Wait for the first Action run to go green, then check `https://YOURUSERNAME.github.io`.

### Custom domain

At your registrar, point the apex domain at GitHub's four Pages IPs:

```
A    @    185.199.108.153
A    @    185.199.109.153
A    @    185.199.110.153
A    @    185.199.111.153
CNAME www  YOURUSERNAME.github.io.
```

Then in **Settings → Pages**, enter the domain and tick **Enforce HTTPS** once the certificate provisions (a few minutes to an hour).

---

## Editing content

| What | Where |
|------|-------|
| Bio and landing page | `_pages/about.md` |
| Publications | `_bibliography/papers.bib` — set `selected={true}` to surface a paper on the landing page |
| CV (and the CV PDF) | `_data/cv.yml` — the `Render a CV` Action regenerates `assets/rendercv/rendercv_output/Shikhar_Shiromani_CV.pdf` on every push that touches it |
| News items | `_news/*.md` — one file per item, filename date sorts them |
| Service, reviewing, awards | `_pages/service.md` |
| Blog posts | `_posts/*.md`. The `notes` page is at `/notes/` but hidden from the navbar; set `nav: true` in `_pages/blog.md` to show it |
| Site title, socials, nav | `_config.yml`, `_data/socials.yml` |

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
