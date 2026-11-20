---
title: Fix duplicate Recent articles section after Blowfish update
date: 2026-11-20
tags: [hugo, blowfish, layouts, submodule]
draft: false
---

Homepage showed two identical Recent articles sections after a theme update.

Problem
-------

stationerygamer.com. Blowfish theme as a git submodule, deployed via GitHub
to Cloudflare Pages. Updated the submodule on 20 Nov 2026 and the homepage
rendered `recent-articles/main.html` twice.

Cause: I had copied `layouts/partials/home/profile.html` from the theme
into my own `layouts/partials/home/` folder ages ago. That froze my copy
against theme updates. Old Blowfish ended `profile.html` with its own
`<section>{{ partial "recent-articles/main.html" . }}</section>` block.
A later Blowfish version moved that block out of the partial and into the
theme's `layouts/index.html`, which calls it after whichever homepage
partial runs. Frozen override plus updated theme = two Recent sections.

Environment
-----------

- Hugo, Blowfish theme via git submodule
- Site repo: `~/Sites/stationerygamer`
- Deploy: push to main, Cloudflare Pages builds

Fix
---

Diffed my override against the theme's current version of the same file.
Mine was a stale stock copy with no customisations, so deletion was safe.

```bash
cd ~/Sites/stationerygamer
diff layouts/partials/home/profile.html themes/blowfish/layouts/partials/home/profile.html
git rm layouts/partials/home/profile.html
git commit -m "Remove stale profile.html override; duplicate Recent section"
git push origin main
