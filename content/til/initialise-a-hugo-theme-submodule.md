---
title: "Initialise a Hugo theme submodule"
date: 2026-11-20
tags: ["git", "hugo"]
draft: false
---

Check whether the theme is actually on disk:
```bash
git submodule status
```

A `-` before the hash means the submodule is not initialised — the theme folder is empty and `hugo server` fails to find the theme. Bit me on countingbeans after the theme was added from another machine.

Fill the folder in:
```bash
git submodule update --init themes/hugo-bearblog
```

Swap in whichever path the status output shows. Freshly cloned the whole repo? Grab everything in one go:
```bash
git submodule update --init --recursive
```

One-time per clone — a later `git pull` does not empty it again. Confirm with `hugo server`; the site builds once the theme files are present.
