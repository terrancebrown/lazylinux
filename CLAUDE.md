Repo: ~/Sites/lazylinux (branch: main)
Theme: PaperMod
Hugo version: 0.161.1+extended+withdeploy
Deployment: Cloudflare Pages via GitHub push to main. Build command: hugo --minify. HUGO_VERSION env var is set to 0.161.1.
Editor: VSCodium (primary), micro in terminal.

Content structure:
- All posts are flat .md files organised into topic sections
- Sections: content/til/ (Today I Learned), content/configs/ (config references)
- No date prefix on slugs
- Front matter is YAML (--- delimiters)
- Archetype scaffolds: date, draft, title only — additional fields added manually
- New post commands:
  hugo new content/til/slug.md
  hugo new content/configs/slug.md

Front matter convention (based on existing posts):
```yaml
title: "Post Title"
date: YYYY-MM-DD
tags: ["tag"]
draft: false
```

Posts are short and reference-focused. TILs are quick single-topic notes; configs are annotated config file snippets. The owner runs macOS, Bazzite, Fedora Workstation, and Debian XFCE. Writes in South African English (en-GB spelling).
