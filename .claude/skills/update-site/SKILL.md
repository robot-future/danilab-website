---
name: update-site
description: Update and deploy the DANiLab website (Hugo + HugoBlox on AWS Amplify). Use for adding news posts, publications, datasets, team members, editing page text or images, and for building, previewing, committing and deploying to danilab.org. Also covers rollback and troubleshooting failed Amplify builds.
---

# Updating the DANiLab website

Hugo + HugoBlox "Research Group" site for the DANiLab group at the University
of Leicester. Lives at https://danilab.org, hosted on AWS Amplify.

**The deploy loop: push to `main` → Amplify auto-builds → live in ~3-5 min.**
There is nothing to click in the AWS console for a normal content update.

## Non-negotiables

1. **Never push without the user's explicit go-ahead.** Push = deploy = the
   change is public on danilab.org. Editing and committing locally is fine to
   do as part of the work; the push is the point of no return.
2. **Always build locally before pushing** (`hugo`). A build that fails locally
   fails on Amplify too. Never push a broken build.
3. **Never destructively modify an image.** Before resizing/cropping/replacing
   any image, copy the pristine original to
   `image-originals/<same-relative-path>` first. This is a standing rule.
4. **Never edit theme module files.** The HugoBlox modules live in
   `~/Library/Caches/hugo_cache/modules/`. To change theme behaviour, add a
   project override under `layouts/` instead (see "How overrides work").
5. **Don't touch anything outside this repo.**

## Environment

- **`hugo` may not be on PATH.** It is Hugo **v0.135.0 extended**. If `hugo`
  is not found, look for it at `~/bin/hugo` and use that full path for every
  command below.
- Build: `hugo --gc` (add `--minify` to mirror production).
- Local preview: `nohup hugo server > /tmp/hugo.log 2>&1 & disown`
  then http://localhost:1313
- No Node/npm. Theme is installed via **Hugo Modules** (needs Go at build time).
- Git remote uses **SSH** (`git@github.com:robot-future/danilab-website.git`),
  authenticated as `dh-leics`. Pushing works without prompting.

## The standard update loop

1. Make the edit (usually a markdown file under `content/`).
2. Build: `hugo --gc` — must succeed with no errors.
3. Verify the change landed, e.g. `grep` the built file in `public/`, or start
   the dev server and look at the page.
4. Show the user what changed. Get their go-ahead.
5. Commit with a clear message, then `git push origin main`.
6. Tell the user it will be live in ~3-5 minutes. Optionally verify after:
   `curl -sS https://danilab.org | grep -o '<title>[^<]*</title>'`

For **large or structural changes** (redesigns, new page types, layout work),
prefer a feature branch, preview locally, then merge to `main` once approved.

## Where content lives

| What | Where |
|---|---|
| Homepage (hero, research areas, funders, news, work-with-us) | `content/_index.md` |
| News posts | `content/post/<slug>/index.md` |
| Publications | `content/publication/<slug>/index.md` |
| Datasets | `content/dataset/<slug>/index.md` |
| Team page | `content/people/index.md` |
| Join the lab page | `content/contact/index.md` |
| Robots & hardware page | `content/robots-hardware/index.md` |
| Site config, baseURL | `config/_default/hugo.yaml` |
| Nav, theme, fonts, appearance | `config/_default/params.yaml` |
| All custom CSS | `assets/scss/template.scss` |
| Images used by pages | `assets/media/` (or alongside the page's index.md) |
| Pristine image backups | `image-originals/` (never served; keep in sync) |

Landing pages (`_index.md`, `people`, `contact`) are built from a `sections:`
list of **blocks** in front matter — `block: markdown`, `block: hero`,
`block: collection`. Body text goes in the block's `text: |` field, and
supports raw HTML plus Hugo shortcodes.

## Adding a news post

Create `content/post/<YY-MM-DD-slug>/index.md` (match the existing naming):

```markdown
---
title: Your headline here
date: 2026-07-05
image:
  caption: ''
  focal_point: 'Smart'
---

Opening paragraph — this becomes the card summary on the homepage.

More body text.

![](photo.jpeg)
```

- Put images in the **same folder** as `index.md` and reference them by
  filename, as above.
- **Dates must not be in the future** — Hugo excludes future-dated content from
  production builds, so the post would silently vanish. Check today's date.
- The homepage "Latest News" block shows the 3 most recent automatically.

## Adding a publication

Create `content/publication/<slug>/index.md`:

```markdown
---
title: "Full Paper Title"
authors:
  - Author One
  - Zhou Daniel Hao
date: "2026-01-15T00:00:00Z"
publishDate: "2026-01-15T00:00:00Z"
publication_types: ["2"]      # 1 = conference paper, 2 = journal article
publication: "*IEEE Transactions on Something*"   # full venue, italics
publication_short: "IEEE T-X"                     # badge on the card
abstract: ""
featured: false
doi: "10.1109/..."
url_source: "https://..."     # optional; also url_pdf, url_code, url_dataset,
                              # url_project, url_video
image:
  caption: ""
  focal_point: ""
  preview_only: false
---
```

- **Ordering is by `date`, descending.** To place a paper in a specific spot in
  the list, set its date relative to its neighbours. The card does not display
  a date, so an adjusted date is not user-visible — but add a comment in the
  file explaining why, as existing entries do.
- **No future dates** (same build-exclusion trap as posts).
- Add a teaser image as `featured.jpg` in the paper's folder. Cards without an
  image degrade gracefully.
- Datasets work the same way but live in `content/dataset/` and appear under a
  separate "Datasets" heading on the publications page.

## Editing the team page

`content/people/index.md` — one grid of `person-card` divs, all members
together (deliberately not grouped by role). Each card is:

```html
<div class="col-6 col-sm-4 col-md-3 mb-4">
<div class="person-card">

{{< figure src="firstname-lastname.jpg" alt="Name" class="team-photo" lightbox="false" >}}

**[Name](https://their-own-page)**

<div class="person-role">PhD Candidate</div>

Their research topic (Funder)

</div>
</div>
```

Each person's name links to **their own** page (personal site / Scholar), not a
project page. Photos go in `assets/media/`. Keep blank lines around markdown
inside HTML divs — Hugo needs them to render the markdown.

## Images

- Optimise before committing: `sips -s format jpeg -Z 1400 -s formatOptions 85 in.jpg --out out.jpg`
  (`-Z` = max dimension; omit it to keep native size — never upscale).
- **Back up the pristine original to `image-originals/<same-relative-path>`
  before any destructive change.** This is tracked in git on purpose.
- Hugo generates responsive WebP variants automatically at build time.
- The social preview image is `assets/media/sharing.png` (used as `og:image`).

## Custom styling

All custom CSS goes in **`assets/scss/template.scss`** (a project override
imported after the theme). Available variables: `$sta-primary`,
`$sta-background`, plus project ones defined at the top of that file:
`$danilab-text`, `$danilab-muted`, `$danilab-card-bg`.

Bootstrap 5 breakpoints are available via
`@include media-breakpoint-up(md) { ... }`. Note: some theme utility classes
(e.g. `text-md-start`) are `!important` and will not override — write a scoped
custom rule instead.

## How overrides work

To change theme rendering, mirror the module's path under `layouts/`:
- Blocks: `layouts/partials/blocks/<blockname>.html`
- Views (how a collection item renders): `layouts/partials/views/<view>.html`
- Section list pages: `layouts/section/<section>.html`

Existing overrides in this repo: `blocks/hero.html`, `views/pubcard.html`,
`views/newscard.html`, `section/publication.html`, and
`partials/hooks/footer-start/logo.html`.

## Deployment

- **Build spec:** `amplify.yml` in the repo root. It installs Go and Hugo
  Extended **into `$HOME/tools`** — the Amplify container is **non-root**, so
  writing to `/usr/local` fails with "Cannot mkdir: Permission denied". Don't
  "fix" it back to `/usr/local`.
- **Required Amplify env vars** (set in the console, App settings →
  Environment variables): `HUGO_VERSION = 0.135.0`, `GO_VERSION = 1.23.4`.
  If a build fails on the very first curl, these are usually missing.
- `baseURL` is `https://danilab.org/` in `config/_default/hugo.yaml`, so the
  build needs no `-b` flag.
- `netlify.toml` is a leftover from the old host. Amplify ignores it.
- There is **no GitHub Actions deploy**. The template's GitHub Pages workflow
  (`publish.yaml`) was removed because Pages is not used and it failed on every
  push. Don't re-add it; Amplify is the only deploy path.

### If an Amplify build fails
Ask the user for the **last ~15 lines around the first `[ERROR]`** — not the
whole log, it's enormous. Then fix, commit, push; the push retriggers a build.

### Rollback
Two options, both fast:
1. **Amplify console** → app → branch → pick a previous deployment →
   **Redeploy this version**. No code changes needed.
2. `git revert <sha>` and push.

## Verifying it's live

```bash
curl -sS https://danilab.org | grep -o '<title>[^<]*</title>'   # site is up
dig +short danilab.org                                          # DNS
```

## Known context

- The site was migrated from WordPress; pre-2026 publications are still being
  migrated, and the publications page carries a notice saying so.
- DNS for danilab.org is delegated to Route 53; Amplify manages the records and
  the TLS certificate.

> **Note:** This repository is public. Keep infrastructure specifics, account
> details and anything security-relevant **out of this file** — put them in
> `.claude/NOTES.local.md`, which is gitignored. Read that file too if it
> exists; it holds private operational notes for this site.
