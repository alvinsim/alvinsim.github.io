---
title: 'It''s a Chocolatey Time'
date: Sun, 14 Jun 2020 13:56:03 +0000
draft: false
tags: ['Others']
---

![img](/images/chocolatey-logo.png)

[Chocolatey](https://chocolatey.org) is a software or package management on Windows, similar to the `apt` command on Debian or Debian-based distributions. It'd be great if Windows has something similar built-in. This does make managing software so much easier.

I have used Chocolatey for many years, since 2016 or earlier, and it is always one of the first things I install on a new Windows system.

One of the main advantages of using Chocolatey and because it is a command-line-interface (_CLI_) power tool, is installations and upgrading of software can be automated. This means that you can now write a single `choco install`, `choco uninstall` or `choco upgrade` command in a Windows `.BAT` file and just sit back and wait for Chocolatey to do its thing. Or unfortunately, if you are not a CLI person, you can choose to install the [chocolateGUI](https://github.com/chocolatey/ChocolateyGUI) and use that instead.

Install Chocolatey
==================

To get started with Chocolatey, you'd first have to install it. Before starting, most importantly you'd need to make sure you have Administrator access to the Windows machine. If unfortunately, you don't, you can refer [here](https://chocolatey.org/docs/installation#non-administrative-install) for the non-administrative installation steps.

You can refer to the installation steps in the Chocolatey [installation page](https://chocolatey.org/install). Basically, you will have to open PowerShell as an Administrator (`Win+x` _and select "Windows PowerShell (Admin)"_) and paste the below command into the shell and run it.

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

If for some reason you encounter an error during this step, you can refer back to the installation page.

After the installation has completed, you can run the command `choco` and it should output the Chocolatey version installed plus the Chocolatey command for the help menu, like below.

![img](/images/choco.gif)

By default, Chocolatey is installed in `%PROGRAMDATA%` (_you can run `echo %PROGRAMDATA%` in the command prompt and see what path it is set to_) and the software that you install using Chocolatey are installed in `%PROGRAMDATA%\chocolatey\lib`.

Let the fun begin!
==================

To begin using Chocolatey, You can choose either to use the "Command Prompt" or PowerShell and either one has to be run as Administrator.

`choco list`
------------

There are two ways to search for software on Chocolatey – using the `choco list` command or via the Chocolatey website. For example, if I were to search for "sqlitebrowser", I'd run the command `choco list sqlitebrowser`. The output will be a list of software from the Chocolatey "repository" that is related to the word "sqlitebrowser". And you can do the same at the Chocolatey website by clicking on the "Search" at the top-right and type "sqlitebrowser".

![img](/images/choco-list-sqlitebrowser.gif)

`choco install`
---------------

Once you have found the software or list of software to install, you can then run the `choco install` command. This command is expecting one or more names of software to install.

Following the example above, if we want to install sqlitebrowser, we'd run the command `choco install sqlitebrowser`. After Chocolatey is done with the pre-installation steps, you'll then be prompted to enter "Y" ("Yes"), "A" ("All - yes to all"), "N" ("No") or "P" ("Print"). If you want Chocolatey to proceed with the installation without prompting, you can instead run the command `choco install sqlitebrowser -y`.

![img](/images/choco-install-sqlitebrowser-y.gif)

One thing to note: When the installation depends on another software but it is not already installed in your Windows machine, Chocolatey will install all that is required. For a list of dependencies that software requires, you can see them on the Chocolatey website.

`choco upgrade`
---------------

The `choco upgrade` command can be used to upgrade a specific software or all software installed by Chocolatey.

To only upgrade, for example, sqlitebrowser, we can run the command `choco upgrade sqlitebrowser` or `choco upgrade sqlitebrowser -y` to skip the prompt similar to the `choco install` command.

![img](/images/choco-upgrade-sqlitebrowser.gif)

To upgrade all software installed using Chocolatey, we can run the command `choco upgrade all -y`.

If for some reason you want to skip the upgrade for specific software, you can choose to either:

*   Delete the software from the Chocolatey `bin` directory (`%PROGRAMDATA%\chocolatey\bin`).
*   Run the command `choco pin -n=SOFTWARE_NAME`, e.g. `choco pin -n=vlc`.
*   Or if you decide to only skip the upgrade for certain software for this time, you can run this example command `choco upgrade all --except="vlc,youtube-dl -y"`.

`choco uninstall`
-----------------

To uninstall software, you can use the command `choco uninstall` and pass in the software name and also the `-y` option if you want to skip the prompt.

![img](/images/choco-uninstall-sqlitebrowser.gif)

`refreshenv`
------------

`refreshenv` is a very useful command and I do not see why something similar couldn't be baked into Windows.

This command is usually used when you install or uninstall software and it has made changes to the Windows environment variables.

In normal circumstances, you have to open a new Command Prompt or PowerShell window to see the updated Windows environment variables. But, by running `refreshenv`, it refreshes the environment variables in the current command prompt or PowerShell window.

Using it is similar to the `source` command in Unix systems.

![img](/images/choco-refreshenv.gif)

Remove Chocolatey
-----------------

If for some reason you no longer want to use Chocolatey anymore, you can delete the "chocolatey" folder in the `%PROGRAMDATA%` or wherever `%ChocolateyInstall%` is pointing to.

According to the [Uninstalling Chocolatey page](https://chocolatey.org/docs/uninstallation), it is also best to make a copy of the `lib` and `bin` sub-folders just in case something not right happens. I'd say, best to back up the `chocolatey` directory instead.

Alternative to Chocolatey
=========================

Scoop
-----

I happened to stumble upon [Scoop](https://scoop.sh/) that does the same as Chocolatey. I didn't give it a try but I noticed that more software projects are listing Scoop as part of their installation instructions in their documents.

You can see a list of supported software at [their GitHub repository](https://github.com/ScoopInstaller/Main/tree/master/bucket).

Do share your experience in the comments below if you are using it or have used it before.

Windows Package Manager
-----------------------

And here is another alternative and surprisingly it is from Microsoft – [Windows Package Manager](https://docs.microsoft.com/en-us/windows/package-manager/).

To install, you'll need to grab ["Windows App Installer"](https://www.microsoft.com/en-au/p/app-installer/9nblggh4nns1?ocid=9nblggh4nns1_ORSEARCH_Bing&rtc=2&activetab=pivot:overviewtab) from the Microsoft Store. Your Windows will need to be at least Windows 10 version 14393.0 or higher.

Do note that this is still in preview. If you decide to install, do expect bugs, and most importantly, changes when updated preview versions are continuously rolled out.

You can see a list of supported software or packages in Microsoft's [winget-pkgs](https://github.com/microsoft/winget-pkgs) GitHub repository.

Conclusion
==========

Chocolatey has matured now and I rarely come across any issues. If one does happen, you can head up to the software's page in the Chocolatey website and see in the comments section if it is a known issue, otherwise, post a question and ask the software's maintainer.

I would definitely recommend Windows users to use Chocolatey, especially when you need to set up a new Windows machine. It has truly improved the experience of software management in Windows. The two advantages of using Chocolatey from my point-of-view are

1.  It is a CLI tool. So this helps a lot when you want to automate your software management.
2.  It handles software dependencies.

If this is new to you, do give this a try and let me know your thoughts.

–
