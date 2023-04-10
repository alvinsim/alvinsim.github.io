---
title: 'SSH Keys Suddenly Refused to Connect'
date: Sun, 29 Nov 2020 11:16:44 +0000
draft: false
tags: ['Git', 'git', 'github', 'gitlab', 'ssh', 'ssh-keys']
---

Strangely, my Debian system (_running on WSL_) suddenly refused to connect to both Gitlab and GitHub using my SSH keys. Everything was fine when I last used it a couple of weeks ago. But now running the command `ssh -Tv git@github.com` returns a "Connection timed out" error.

![img](/images/ssh-github-fail.png)

And I didn't see the same issue using the same SSH keys on a Ubuntu system (_also running on WSL_) and Git Bash on Windows. So, there is no issues with my SSH keys.

I was very close to re-building my Debian system until I saw [this Stack Overflow answer](https://stackoverflow.com/a/52817036/265416). According to this Stack Overflow answer, which also has a link to one of GitHub's [Troubleshooting SSH](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/using-ssh-over-the-https-port) article, most probably the firewall has refused the SSH connection.

> Sometimes, firewalls refuse to allow SSH connections entirely. If using HTTPS cloning with credential caching is not an option, you can attempt to clone using an SSH connection made over the HTTPS port. Most firewall rules should allow this, but proxy servers may interfere

A quick workaround is to change the `hostname` and port i.e. use port `443` and `hostname` `ssh.github.com` instead. To quickly test this, we can use the `ssh` command below.

![img](/images/ssh-github-success.png)

The final touch would be to add the hostname and port to the `~/.ssh/config` file.

```
Host github.com
  Hostname ssh.github.com
    Port 443

Host gitlab.com
  Hostname altssh.gitlab.com
    Port 443
```

With this in my SSH configuration file, I can now connect happily to GitHub and Gitlab.

![img](/images/ssh-github-success-02.png)
