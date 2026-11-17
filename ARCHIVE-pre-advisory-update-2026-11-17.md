# Site archive: pre-advisory update (2026-11-17)

This is a snapshot of **galudesign.com exactly as it was live in production** on
2026-11-17, before the "Engage with me" section was repositioned from
consulting retainers + full-time opportunities to a single advisory offering.

| What | Value |
| --- | --- |
| Repository | `galudesign/galudesign` (GitHub Pages, branch `main`, folder `/`, custom domain `galudesign.com`) |
| Production commit archived | `475b1c25551ec7202a2ab56f66cdd6f0fc01d053` ("Reorder proof-bar clients to Okta · OpenAI · Sierra") |
| Annotated tag | `site-archive-pre-advisory-update-2026-11-17` (points at the commit above) |
| Backup branch | `archive/pre-advisory-update-2026-11-17` (the commit above + this document) |
| Self-contained bundle | GitHub Release `site-archive-pre-advisory-update-2026-11-17`, asset `galudesign-archive-pre-advisory-2026-11-17.tar.gz` (full site files, no git history needed) |
| Bundle SHA-256 | `ec24c72c66ae397ee3dfa76d47d9155ffd0bc834b0fcb68a19a3faec752b59ca` |

## What this version contains

- `index.html`: the live page (with GA4 `G-3C5DYBDV8E`), including the original
  "Engage with me" section: **Consulting** column (limited 3-month retainers,
  fit call, Capacity / Engagement / Model / Fit parameter grid, "Book a fit call"
  Google Calendar appointment link) and **Full-time** column (five numbered
  criteria, "Email about a role" copy-email button).
- `testing/`: the staging copy served at galudesign.com/testing/ (no analytics).
- `archive/live-2026-09-22/`: an older archive.
- `portfolio-samples/`, `favicon.png`, `CNAME` (`galudesign.com`).

Deployment: GitHub Pages "legacy" build from `main` `/`. There is no `.nojekyll`
and no `_config.yml` or workflow, so Pages runs default Jekyll and copies the
HTML files as-is.

## How to restore production to this version

Option A: revert main to this snapshot with a new commit (keeps history, safest):

```sh
git clone https://github.com/galudesign/galudesign.git && cd galudesign
git checkout main
git checkout site-archive-pre-advisory-update-2026-11-17 -- .
# remove any files added after the snapshot (shown by:)
git diff --name-status site-archive-pre-advisory-update-2026-11-17 --diff-filter=A
git commit -m "Restore site to site-archive-pre-advisory-update-2026-11-17"
git push origin main
```

Option B: hard reset main to the tag (rewrites main's history; only if you want
main to be exactly this commit):

```sh
git checkout main
git reset --hard site-archive-pre-advisory-update-2026-11-17
git push --force-with-lease origin main
```

Option C: without git history (from the release bundle):

```sh
gh release download site-archive-pre-advisory-update-2026-11-17 -R galudesign/galudesign \
  -p galudesign-archive-pre-advisory-2026-11-17.tar.gz
sha256sum galudesign-archive-pre-advisory-2026-11-17.tar.gz   # compare with the value above
tar xzf galudesign-archive-pre-advisory-2026-11-17.tar.gz
# copy the contents of galudesign-site-pre-advisory-2026-11-17/ into the repo root
# (or upload them to any static host), commit, and push to main
```

### Redeploying

GitHub Pages rebuilds automatically on every push to `main`. After pushing:

1. Watch the build: `gh api repos/galudesign/galudesign/pages/builds/latest`
   (status should become `built`), or the repo's Actions / Pages settings.
2. Hard-refresh https://galudesign.com/ and confirm the Engage section shows
   the Consulting and Full-time columns.
3. Pages settings must stay: source branch `main`, folder `/`, custom domain
   `galudesign.com` (the `CNAME` file in this snapshot keeps the domain).

Keep this tag, branch, and release as the permanent rollback reference.
