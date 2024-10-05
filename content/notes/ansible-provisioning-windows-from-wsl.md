---
id: ansible-provisioning-windows-from-wsl
aliases:
  - 🪟 Provisioning Windows from WSL
tags:
  - development
  - ansible
title: 🪟 Provisioning Windows from WSL
---

I found this to be very difficult since most tutorials online just install ansible in WSL, and do not include provisioning the host Windows OS through WSL. Eventually I found this post: [https://landy.dev/2020/12/01/managing-windows-hosts-with-ansible/](https://landy.dev/2020/12/01/managing-windows-hosts-with-ansible/) which shows how to get ansible working through SSH, which is much easier than using WinRM.

Once I got SSH installed and setup to use `ed25519` keys (see: [SSH](https://www.notion.so/SSH-b2bd717bc003422a890660ac57cb95a2?pvs=21)) things were quite simple.

I created an entry in my `ssh` config for accessing the Windows host, and used that in my `inventory.yml` file:

```yaml
---
all:
  hosts:
    my_windows_server:
      ansible_shell_type: cmd
      ansible_host: win
      ansible_user: erick
```

Then I was able to run a test command using:

```bash
ansible -i inventory.yml -m win_ping my_windows_server
```

Which produced the following output:

```
my_windows_server | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```
