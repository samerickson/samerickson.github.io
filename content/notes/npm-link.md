---
id: npm-link
title: 📦 NPM | Link
tags:
  - npm
---

NPM link allows you to override where [📦 NPM](npm.md) gets a package from.

- [npm-link | npm Docs](https://docs.npmjs.com/cli/v8/commands/npm-link)\*

## Steps

> [!WARNING] Warning
> `npm link` requires the versions of node to match.

1. Navigate to the locally cloned repository for a dependency you want to add
2. Note the name of the package in the `package.json`
3. Enter the command `npm link`
4. Navigate to the host application repository
5. Enter the command `npm link <name-of-package>`

At this point you will notice that the package that you linked will not be listed in the dependencies for the host app, but the package will appear as a `symlink` within that projects `node_modules`.
