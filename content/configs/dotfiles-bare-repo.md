---
title: "Dotfiles: bare repo, $HOME as working tree"
date: 2026-11-20
tags: ["dotfiles", "git", "zsh"]
draft: false
---

Dotfiles live in a bare git repo at `~/.dotfiles`. No symlinks, no stow, no manager. `$HOME` is the working tree; tracked files stay where they belong.

Everything runs through an alias, defined in `.zshrc` on every machine:

```bash
alias dotfiles='git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
```

Works in interactive shells only — scripts and cron jobs need the full form spelt out:

```bash
git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME <command>
```

Everyday use:

```bash
cd ~
dotfiles status
dotfiles add path/to/file
dotfiles commit -m "message"
dotfiles push
```

New file not appearing in `status`? Intentional: `status.showUntrackedFiles no` keeps `~` from flooding git. Be explicit with `add`.

Setup on a new machine:

```bash
git clone --bare <remote-url> $HOME/.dotfiles
alias dotfiles='git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
dotfiles checkout
dotfiles config --local status.showUntrackedFiles no
```

If `checkout` refuses because existing files would be overwritten (default `.bashrc` and the like), move those aside first and re-run.

Gotchas:

- `add -A` can hang — it scans all of `$HOME` (Videos, Downloads, `.cache`, containers). Prefer `add -u` or explicit paths.
- Tracked a secret by accident — `dotfiles rm --cached <file>` untracks without deleting.
- Merge conflicts on pull — resolve as usual: edit, `dotfiles add <file>`, `dotfiles commit`.
- Push rejected with "remote contains work you do not have" — `dotfiles pull --no-rebase` first, then push.
- Pull says "divergent branches" — same fix: `pull --no-rebase` merges, then `push`. Or set a standing answer with `dotfiles config --local pull.rebase false`.

What's tracked:

- `.zshrc` — shell config, carries the `dotfiles` alias itself
- `.config/micro` — micro editor settings
- `README.md` — full command reference for this setup

Full command reference lives in the repo README: https://github.com/terrancebrown/dotfiles
