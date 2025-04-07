---
id: fzy
tags:
  - command-line
  - snippets
  - software
title: 🧉 Fzf
modified: 2025-04-06T17:03:20-07:00
created: 2025-04-06T16:59:33-07:00
---

> Fzf is a general-purpose command-line fuzzy finder.
> [GitHub - junegunn/fzf: :cherry\_blossom: A command-line fuzzy finder](https://github.com/junegunn/fzf)

##  🔮 Show file preview

**Using cat:**
```sh
fzf --preview 'cat {}'
```

**Using [🦇 bat](bat%201.md):**

```sh
fzf --preview 'bat --style=numbers --color=always --line-range :500 {}'
```

## 💿 Cd into directories

```bash
cd $(find . -type d -print | fzf)
```