---
title: "Rename a git branch"
date: 2026-03-21
tags: ["git"]
draft: false
---

Rename the current branch:
```bash
git branch -m new-name
```

Rename a specific branch:
```bash
git branch -m old-name new-name
```

Useful when git initialises with `master` and you want `main`.