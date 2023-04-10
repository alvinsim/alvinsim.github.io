---
title: '''git status'' in Your Prompt'
date: Tue, 25 Jun 2019 12:35:07 +0000
draft: false
tags: ['bash', 'git', 'Git', 'linux', 'unitx', 'zsh']
---

Did you know: You can have a visual representation of the `git status` command output in your shell prompt? This is especially convenient for people who use the `git` command-line interface (_CLI_). Unfortunately, this doesn't work with the Windows command prompt or `cmd`. But there are a few workarounds.

`git-prompt.sh`
===============

> Disclaimer: For this part of the article, I will show the how-tos by using Debian (on Windows Subsystem for Linux or WSL) and FreeBSD as examples. These are the Unix-like systems that I have access to currently. For other systems or Linux distros, the steps should be the same except for the location or name of the `git-prompt.sh` file.

When `git` is installed in a Unix-like system, it usually comes with the script file `git-prompt.sh`. The location and file name of this file may differ depending on the type of system or distro you use.

Locating the Script File
------------------------

In FreeBSD, this shell script is located in `/usr/local/share/git-core/contrib/completion/`.

It is a bit different for Debian and/or Debian-based distros. The script file you should look for is `git-sh-prompt`. I believe it is similar to `git-prompt.sh` only with a different name. This file can be found in `/usr/lib/git-core/`.

Setting It Up
-------------

It is documented very clearly in the script file on how to use it and the instruction is for both `bash` and `zsh` shells. The instruction also states the different flags you can toggle depending on the information you want displayed in the shell prompt.

Firstly, copy this script file to your home directory and rename it to `.git-prompt.sh`.

```
# FreeBSD
$ cp /usr/local/share/git-core/contrib/completion/git-prompt.sh ~/.git-prompt.sh

# Debian
$ cp /usr/lib/git-core/git-sh-prompt ~/.git-prompt.sh
```

Next, you'll need to configure your shell, `bash` or `zsh`, to `source` the `~/.git-prompt.sh` file. To do that, add the code snippet below to either the `~/.bashrc` or `~/.zshrc` file.

```
source ~/.git-prompt.sh
```

This step is different for FreeBSD users because [it doesn't have neither a `~/.bashrc` nor a global `bashrc` file](https://serverfault.com/questions/174251/system-wide-bashrc-on-freebsd). Instead, you can do the same with the `~/.profile` file.

The next fun thing to do is to configure the information you want to show in your shell prompt. The flags available are:

*   `GIT_PS1_SHOWDIRTYSTATE`
*   `GIT_PS1_SHOWSTASHSTATE`
*   `GIT_PS1_SHOWUNTRACKEDFILES`
*   `GIT_PS1_SHOWUPSTREAM`
*   `GIT_PS1_STATESEPARATOR`
*   `GIT_PS1_DESCRIBE_STYLE`
*   `GIT_PS1_HIDE_IF_PWD_IGNORED`
*   `GIT_PS1_SHOWCOLORHINTS`

I will not go into detail what each flag means or the different values to enable them because it is clearly documented in the `git-prompt.sh` script file. Have a read and play with the flags to see what suits you.

As a reference, you can refer to the code snippet below on the flags I have configured for my setup.

```
export GIT_PS1_SHOWDIRTYSTATE=1
export GIT_PS1_SHOWSTASHSTATE=1
export GIT_PS1_SHOWUPSTREAM="auto"
export GIT_PS1_SHOWCOLORHINTS=1
export GIT_PS1_HIDE_IF_PWD_IGNORED=1
export GIT_PS1_SHOWUNTRACKEDFILES=1
```

Finally, with all of that done, we have to update `$PS1` to show the necessary information from `git status` based on the flags we have enabled in the step above.

There are two ways to do this. Below is an example to do it either ways. Add either one of the code below to your `~/.bashrc`, `~/.zshrc` or `/.profile` file.

```
# Method 1
export PS1='\u@\h \w$(__git_ps1 " (%s)") \$'

# Method 2
export PROMPT_COMMAND='__git_ps1 "=\u@\h:\w" "\\\$ "'
```

Save your changes and run `source ~/.bashrc` (or `/.zshrc` or `/.profile`). Go to one of your local git repositories and you'll see something like below.

```
# Examples of 'git status' output in the shell prompt
# ===================================================
#
# Current branch is on 'master' and is sync with upstream or 'origin/master'
alvinsim@beastie:~$ ~/src/dotfiles (master=) $

# Current branch is on 'master' and one or more new/untracked files has been added
alvinsim@beastie:~$ ~/src/dotfiles (master %=) $

# Current branch is on 'master' and one or more files are modified
alvinsim@beastie:~$ ~/src/dotfiles (master *=) $

# Current branch is on 'master' and one or more files are staged for commit
alvinsim@beastie:~$ ~/src/dotfiles (master +=) $

# Current branch 'master' is one or more commits ahead of 'origin/master' or upstream
alvinsim@beastie:~$ ~/src/dotfiles (master>) $

# Current branch 'master' is one or more commits behind of 'origin/master' or upstream
alvinsim@beastie:~$ ~/src/dotfiles (master<) $
```

You can refer to the full code snippet below. You should have something similar.

```
# change value of PS1 to show git status of a git repo
source ~/.git-prompt.sh
export GIT_PS1_SHOWDIRTYSTATE=1
export GIT_PS1_SHOWSTASHSTATE=1
export GIT_PS1_SHOWUPSTREAM="auto"
export GIT_PS1_SHOWCOLORHINTS=1
export GIT_PS1_HIDE_IF_PWD_IGNORED=1
export GIT_PS1_SHOWUNTRACKEDFILES=1
#export PS1='\u@\h \w$(__git_ps1 " (%s)") \$ '
export PROMPT_COMMAND='__git_ps1 "\u@\h:\w" "\\\$ "'
```

Without `git-prompt.sh`
=======================

If you are not able to locate the `git-prompt.sh` script file, or it didn't come as part of the `git` installation, you can download it from git's [Github repository](https://github.com/git/git/tree/master/contrib/completion).

On Windows?
===========

As far as I know, there are two ways to achieve this ― Git Bash and PowerShell.

Git Bash
--------

![img](/images/git-bash.png)

Download the `git` setup file for Windows from [https://git-scm.com](https://git-scm.com) or [https://gitforwindows.org](https://gitforwindows.org) and run it. Personally, I prefer to use [Chocolatey](https://chocolatey.org), a package manager for Windows, to install `git` by running the command `choco install git -y`.

`git` for Windows comes with something extra called Git BASH. It is a BASH emulator where you can run the `git` command just like you would on a Unix-like system. You'll also have all the common Unix commands at your disposal. Yeah, it is something similar to [Cygwin](https://www.cygwin.com).

In Git BASH, the `git-prompt.sh` file is located in `/mingw64/share/git/completion/`.

PowerShell
----------

For those who do not prefer to use BASH, another option is to use Windows PowerShell. There is a PowerShell module called [posh-git](https://github.com/dahlbyk/posh-git). You can follow the installation instructions as stated in the `README.md` file. I am sorry that I can't provide a step-by-step guide here because I am not familiar with PowerShell and the instructions didn't work for me.

`__git_ps1: command not found`
==============================

If for some unknown reason you see the message `__git_ps1: command not found`, this basically means that the shell is not a login shell. You can refer to [this answer at Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/38175/difference-between-login-shell-and-non-login-shell#46856) for more clarity.

I encountered this once in my FreeBSD system when using [tmux](https://github.com/tmux/tmux/wiki). The `bash` shell was not started as a login shell. Thus, the shell ignored the `~/.profile` file.

Wrapping Up
===========

I hope that you find this article useful especially if you use `git` in the terminal a lot in a Unix-like system or some kind of emulator. If you have a simple guide on how to set this up for PowerShell and don't mind sharing, I will link it here.

–
