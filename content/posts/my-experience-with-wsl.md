---
title: 'My Experience with Windows Subsystem for Linux (WSL)'
date: Sat, 15 Sep 2018 13:07:12 +0000
draft: false
tags: ['debian', 'emacs', 'linux', 'MS WIndows', 'nodejs', 'npm', 'windows', 'wsl']
---

One day on my way back home, I was listening to one of [Hanselminutes's](https://www.hanselminutes.com/) podcast episodes titled ["Inside Linux on Windows with WSL and Tara Raj"](https://www.hanselminutes.com/646/inside-linux-on-windows-with-wsl-and-tara-raj).

This reminded me of the first time I tried it when [Microsoft first announced it](https://techcrunch.com/2016/03/30/be-very-afraid-hell-has-frozen-over-bash-is-coming-to-windows-10/) back in 2016. Then, it was called "Bash on Windows" and Microsoft collaborated with [Canonical](https://www.canonical.com/), the company behind [Ubuntu](https://www.ubuntu.com/).

Personally, I didn't use it much. It was just another shiny new toy and I didn't have a use for it then. I removed it from my Windows a couple of weeks after.

After listening to the podcast episode, I thought I should give it another go and maybe I can set it up as my development environment. It would be great rather than connecting remotely via [SSH](https://en.wikipedia.org/wiki/Secure_Shell) to my [FreeBSD](https://www.freebsd.org/) [Virtual Box](https://www.virtualbox.org/) Virtual Machine (_VM_). Don't get me wrong, I like FreeBSD and I started playing with it since version 9 (_current version as of this writing is version 11_). It's my favourite Unix systems thus far. But there is a down side when you use VMs. You will need to allocate a portion of your resources (_memory, no. of CPUs, graphics, etc_) and this impacts your main OS' performance. With WSL, you do not incur the overhead of using a VIM.

Introduction to WSL
===================

My take on WSL after listening to the podcast episode is this: it is like a bridge between the Linux system and Windows. The Linux system which you install, doesn't have a Linux kernel. According to [this Microsoft blog post titled "Windows Subsystem for Linux Overview"](https://blogs.msdn.microsoft.com/wsl/2016/04/22/windows-subsystem-for-linux-overview/), there are two drivers in WSL, `lxcore.sys` and `lxss.sys`, and their job is to translate the Linux system calls to Windows.

Ever heard of [Wine](https://www.winehq.org/) (_Wine is Not an Emulator_)? It is a package you install in Linux/Unix systems, which then allows you to install Windows application, such as Microsoft Office, Adobe Photoshop, games, etc. So, WSL is similar in that sense where you can install Linux/Unix packages on Windows.

And conceptually, you can say it is same with [Cygwin](https://cygwin.com/). But, Cygwin doesn't actually run Linux/Unix binaries. If you notice the Cygwin packages you install, are re-compiled and packaged in `.exe` and `.dll` files. [This answer](https://askubuntu.com/a/814004/969) on [ask ubuntu](https://askubuntu.com) sums it very clearly. Refer to the snippet of the answer below.

> Cygwin is a great tool if you want to live entirely in Windows and want to drive/automate Windows tasks with bash scripts. However, Cygwin is unable to run unmodified Linux binaries.
>
> That's where WSL steps in:
>
> The Windows Subsystem for Linux (WSL), is a new layer of the Windows kernel which aims to provide a high degree of compatibility with the Linux kernel ABI. This allows native, unmodified, Linux ELF64 binaries to run on WSL.

Once I got home, I started my exploration with WSL and also figure out if it is possible to use it as a development environment. Well, installation was easy. It was the installation of packages where I hit some roadblocks, specifically with [Node.js](https://nodejs.org/en/) and [Emacs](https://www.gnu.org/software/emacs/). It took me around 2 - 3 days to get it to a state where I am OK with. But, I have done anything yet. So, I do not know what other things might break.

Installation
============

WSL is supported in Windows 10, Windows Server 2019 and later. Before we start, we have to enable WSL in your Windows. Do note, that this step will cause Windows to reboot without any warning.

To enable WSL, we need to open [PowerShell](https://en.wikipedia.org/wiki/PowerShell) and run it with administrator privileges. In PowerShell, run the command `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`. Once done, Windows will reboot immediately without prompting.

After Windows have re-booted, we can begin installing Linux. Open "Microsoft Store" and search for "Linux". You will see something similar to the screen shot below.

![Microsoft Store with different Linux distros to choose from](/images/microsoft-store-wls.png)

Currently your options are [Debian](https://www.debian.org/), [Kali Linux](https://www.kali.org/), [Suse (Enterprise and OpenSuse)](https://www.suse.com/) and [Ubuntu (versions 16.04 and 18.04)](https://www.ubuntu.com/). To install, click any Linux distro you want and then hit the "Install" button. For me, I went with Debian.

Once that is successfully downloaded and installed, you can launch it from the Microsoft Store by clicking on the "Launch" button or look for it at your Window's Start Menu. Alternatively, you can launch it from the command prompt by typing the name of the distro e.g. `debian`, or `ubuntu`. I am not sure about Kali Linux and Suse though.

Now there is one more step to complete the installation and Microsoft calls this the initialisation step. To do this, just launch the Linux distro and a command prompt will appear to complete the installation. Once everything is completed, you'll be prompted to enter a user name and password like below.

```
Installing, this may take a few minutes...
Installation successful!
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username:
```

You can put in any username and it is not related to your Windows' username. To use your Linux distro, there is no login required. So, the password is mainly used when you need to run commands with `sudo`.

For more information on the installation, you can refer [here](https://docs.microsoft.com/en-us/windows/wsl/initialize-distro).

Post-installation
-----------------

### System Update

Before you start messing around in your Linux distro, it is always good to keep your system updated.

For Debian-based distros like Debian, Ubuntu and Kali Linux, you can run the two commands below, one after the other.

```
$ sudo apt update
$ sudo apt upgrade
```

Once that is done, you are good to go.

To install packages for Debian-based Linux distros, you can use the `apt install` command e.g. `sudo apt install firefox`. To know in more detail how to use the `apt` command, you can type `apt -help` at the prompt. This will show a list of commands to use.

### Opening a GUI Application

If you haven't notice, there is no graphical user interface (_GUI_). All interactions are through the [Bash Shell](https://en.wikipedia.org/wiki/Bash_(Unix_shell)). It is still possible to open a GUI application like a web browser.

You will need to install [X Server](https://en.wikipedia.org/wiki/X.Org_Server) in Windows. There are a few you can choose from such as [MobaXterm](https://mobaxterm.mobatek.net/), [Xming](https://sourceforge.net/projects/xming/) and [Cygwin](https://cygwin.com/). Initially I chose to use Cygwin because I already have that installed. But I setting it up was too painful and it didn't work. So, I installed MobaXterm instead. If you use [Chocolatey](https://chocolatey.org), you can run the command `choco install mobaxterm`. Otherwise, download and install from [their website](https://mobaxterm.mobatek.net/).

![MobaXterm for X Server](/images/wsl-mobaxterm.png)

After installing X Server on Windows, your Linux distro needs to know where to direct the display to. And we don't really want to set this manually each time we use our Linux distro, do we? You will have to run the below command to have it set to you `.profile`.

```
$ echo 'export DISPLAY=localhost:0.0' >> ~/.profile
$ source ~/.profile
```

Now, you can test it with any GUI application you have installed. Below you can see a screenshot of the Firefox webs browser which I installed in my Debian system.

![Firefox installed on Debian running on WSL](/images/wsl-firefox.png)

Pain-in-the-ass Moments
-----------------------

### Emacs

I encountered a number of issues whilst setting up emacs.

1.  "Client failed to connect to the DBUS Daemon:"

    First launch of emacs, I was greeted with the below error messages.

    ```
    (emacs:291): GConf-WARNING **: Client failed to connect to the D-BUS daemon:
    /usr/bin/dbus-launch terminated abnormally without any error message

    (emacs:291): GConf-WARNING **: Client failed to connect to the D-BUS daemon:
    /usr/bin/dbus-launch terminated abnormally without any error message

    (emacs:291): GConf-WARNING **: Client failed to connect to the D-BUS daemon:
    /usr/bin/dbus-launch terminated abnormally without any error message

    (emacs:291): GConf-WARNING **: Client failed to connect to the D-BUS daemon:
    /usr/bin/dbus-launch terminated abnormally without any error message

    (emacs:291): GConf-WARNING **: Client failed to connect to the D-BUS daemon:
    /usr/bin/dbus-launch terminated abnormally without any error message

    (emacs:291): GConf-WARNING **: Client failed to connect to the D-BUS daemon:
    /usr/bin/dbus-launch terminated abnormally without any error message
    ```

    After some searching, I came across an article which mentioned to install the `dbus-x11` package. Installing it actually fixed that. Phew!

2.  I Installed The Wrong Version of Emacs

    With emacs up and running, I ran `git clone` to download my emacs' config file from [my Github "dotfiles"](https://github.com/alvinsim/dotfiles) repository and copied it to `~/.emacs.d/`. I opened that file in emacs and evaluated it (`M-x eval-buffer`). This time, it coughed out "Package 'emacs-25' is unavailable". Now, this is really odd because I thought I have the updated version (_current release version as of this writing is 26_). I confirmed my emacs version once and noticed it was version 24. When I installed emacs, I ran `sudo apt install emacs`. I checked Debian's site and noticed that the latest emacs version it supports is version 25. To install it, I should run `sudo apt install emacs25` instead.

    DANG IT!

    I removed that emacs version and installed version 25. And now everything seems to be OK. _Fingers crossed_.

3.  Org Mode Package Conflict?

    To make sure there is no further issues with my emacs config file, I closed emacs, removed all the loaded packages in `~/.emacs.d/elpa` and opened emacs again.

    This time, I get an error with org mode with the error message "Symbol’s function definition is void: org-link-types". It seems like a known issue with emacs version 25.1.1. You can refer to this [issue reported in github](https://github.com/syl20bnr/spacemacs/issues/8334).

    Basically this error is because of va conflict with the built-in org package in emacs and the org-plus-contrib package I installed separately.

    To fix this, I removed the built-in `org` directory, which you can find at `/usr/share/emacs/25.1/lisp/org`.

    I then restarted emacs and _cross-fingers_ everything is OK for now.

    ![Finally emacs running with no errors](/images/wsl-emacs25.png)


### Node.js

As usual, I installed [Node.js](https://nodejs.org) using the command `sudo apt install nodejs`. There were no issues with Node.js, but you might have this issue with npm when you already have a version of installed in your Windows. Running `npm`, you will be greeted with the error below. This is a known issue and you can have a read [here](https://github.com/Microsoft/WSL/issues/1512).

```
$ npm
: not foundram Files/nodejs/npm: 3: /mnt/c/Program Files/nodejs/npm:
: not foundram Files/nodejs/npm: 5: /mnt/c/Program Files/nodejs/npm:
/mnt/c/Program Files/nodejs/npm: 6: /mnt/c/Program Files/nodejs/npm: Syntax error: word unexpected (expecting "in")
```

To properly install Node.js, run the below command.

```
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt install -y nodejs
```

Conclusion
==========

It was time consuming and very painful setting up Debian or generally any Linux distro on WSL. It is so much easier setting up a fresh install of Debian or FreeBSD on a VM. I do want to give WSL the benefit of the doubt, but it is out of beta and I wasn't expecting all of this.

To be frank, I screwed up my first set-up and had to re-install everything from scratch. On my first attempt while hitting the D-BUS issue with emacs, I read some comments that mentioned to build emacs from source with the `--without-dbus` option. That worked but other issues cropped up.

Another issue I had on my first try was Xming for X Server and things look kind of weird.

In total, I think it took me around 2 - 3 days. If later things really don't work out, I will drop this and go back to my FreeBSD VM.

Anyway, if you are new to Linux/Unix and you are looking for something to play with, this would be a good platform for you to mess around.

Let me know your experience with WSL. It would be great to know issues which other people face and maybe we can provide a helping hand.

– _Alvin Sim_
