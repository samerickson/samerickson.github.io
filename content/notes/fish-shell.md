---
id: fish-shell
tags:
  - shell
  - fish-shell
title: 🐟 Fish (Shell)
---

## Setting Environment Variables

~ [fish\_add\_path - add to the path — fish-shell 3.7.1 documentation](https://fishshell.com/docs/current/cmds/fish_add_path.html)

```sh
# Appending
fish_add_path -a <path-to-append>

# Prepending
fish_add_path -p <path-to-prepend>
```

### In fish.config

Use the universal flag (used to add to path if not already present):

```sh
fish_add_path -u <path-to-prepend>
```