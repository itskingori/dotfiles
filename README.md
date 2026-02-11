# dotfiles

My personal dotfiles, managed with [chezmoi][1].

## How To See What's Managed

Run:

```sh
chezmoi managed
```

This prints the full list of destination paths that will be present in `$HOME` after applying.

> [!NOTE]
> This repository uses chezmoi source-state naming (`dot_` and `private_` prefixes). chezmoi maps these back to the real destination paths when applying.

## Handy Commands

```sh
chezmoi managed
chezmoi diff
chezmoi apply -v
chezmoi add ~/.config/zed/settings.json
chezmoi source-path ~/.config/zed/settings.json
```

[1]: https://www.chezmoi.io
