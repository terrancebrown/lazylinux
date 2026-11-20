---
title: "Update Hugo theme submodules"
date: 2026-11-20
tags: ["git", "hugo"]
draft: false
---

Check the current pin:
```bash
git submodule status
```

A `+` before the hash means the local copy differs from the recorded pin.

Pull the latest commit for one theme:
```bash
git submodule update --remote themes/PaperMod
```

Or all themes at once:
```bash
git submodule update --remote
```

Then commit the pointer change, or the site keeps building against the old version:
```bash
git add themes/PaperMod
git commit -m "Update PaperMod submodule"
git push
```

Push to main triggers the Cloudflare Pages rebuild automatically, provided the build is set to fetch submodules.

Run `hugo server` before pushing; a big theme jump can break layouts quietly.
