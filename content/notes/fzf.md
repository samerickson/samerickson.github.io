w---
id: fzy
tags:
  - command-line
  - snippets
  - software
title: 🧉 Fzf
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