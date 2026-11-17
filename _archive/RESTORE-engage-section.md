# Restoring the original "Engage with me" section

On 2026-11-17 the Engage section on galudesign.com was changed from two
columns (**Consulting**: limited 3-month retainers, fit call, parameter grid,
"Book a fit call"; **Full-time**: five numbered role criteria, "Email about a
role" copy-email button) to a single **Advisory & Consulting** offering.

The original section is preserved, unpublished, in:

- `_archive/sections/engage-consulting-fulltime.html`: verbatim original CSS,
  HTML, and JS.
- Tag `site-archive-pre-advisory-update-2026-11-17` and branch
  `archive/pre-advisory-update-2026-11-17`: the whole site as it was.
  See `_archive/ARCHIVE-pre-advisory-update-2026-11-17.md`.

`_archive/` is not published: GitHub Pages runs Jekyll for this repo (no
`.nojekyll`), and Jekyll skips folders that start with `_`. If a `.nojekyll`
file is ever added, move `_archive/` out of the repo or it will become public.

## Option 1: swap the section back into the current index.html

Keeps every other change made since 2026-11-17.

1. **CSS.** In `index.html` `<style>`, replace everything from
   `/* ─── ENGAGE ──────────────────── */` up to (not including)
   `/* ─── FOOTER ──────────────────── */` with the ENGAGE block from part 1 of
   the archived file. (It restores `.params`, `.param*`, and `.cta.is-copied`;
   `.crit-title` and `.crit-desc` are only used by the advisory version and can go.)
   Add `.wrap .params,` back to the "Sacred rule" selector list near the top
   (after `.wrap .engage-copy,`).
2. **Responsive CSS.** In `@media (max-width: 900px)`, replace
   ```css
   .engage-col { padding: 0 0 40px; }
   .engage-copy:last-of-type { margin-bottom: 0; }
   ```
   with the 900px rules from the archived file (from `.engage-grid {` down to
   `.params { grid-template-columns: 1fr 1fr; }`; the `.engage-grid` rule is
   already there, so don't duplicate it). In `@media (max-width: 520px)`, add
   `.params { grid-template-columns: 1fr; }`.
3. **HTML.** Replace the whole `<!-- ENGAGE · Advisory & Consulting ... -->` comment and
   `<section class="wrap engage" id="engage" ...> ... </section>` with part 2.
4. **JS.** In the final `(function () { ... })();` of the main `<script>`,
   paste part 3 (the `copy-email` handler) right after the ticker
   `if (track) { ... }` block, before `})();`.
5. **Meta description** (optional): the original was
   `Andrew Galu is a founding presentation designer. Consulting that leaves teams independent; selectively open to full-time function-build roles. Okta, OpenAI, Sierra. Bay Area.`
6. Check locally (`python3 -m http.server` in the repo root, open
   `http://localhost:8000/#engage`): both columns render, "Book a fit call"
   opens the Google Calendar booking page, and "Email about a role" changes to
   "Email address copied". Then commit and push to `main`.

## Option 2: restore index.html exactly as it was

Use this if nothing else on the page has changed since, or if you're OK
redoing later edits.

```sh
git checkout main
git checkout site-archive-pre-advisory-update-2026-11-17 -- index.html
git commit -m "Restore original Engage section (consulting + full-time)"
git push origin main
```

GitHub Pages redeploys on push to `main`. Hard-refresh https://galudesign.com/
to confirm.
