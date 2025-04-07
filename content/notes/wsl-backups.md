---
id: wsl-backups
tags:
  - wsl
  - linux
  - development
title: 💻 WSL Backups
modified: 2025-04-06T17:09:09-07:00
created: 2025-04-06T16:59:33-07:00
---

I have accidentally messed up my WSL installations a couple of times by just playing around with things and tinkering with the system files. I like being able to do this, even if I do not really know how, and sometimes make mistakes--it is a beneficial learning experience for me each time. So rather than leaving things as they are and not playing around with things that I should not, I choose to make frequent backups.

## 🚒 Making Backups

I back up my WSL installations using a `tarball` created by the `WSL` executable supplied by Microsoft, using a command much like the one listed below.

```bash
WSL --export Ubuntu C:\Documents\WSL\Ubuntu-WSL.tar
```

Note that I use a dedicated folder on an alternate hard drive, as I have a few WSL instances that I want to backup and some of them are quite large. I also append the date to the compressed file.

## ⛑ Restoring From Backup

You can restore a WSL backup with a command like the following:

```bash
WSL --import Ubuntu C:\Documents\WSL\Ubuntu-WSL.tar

```
