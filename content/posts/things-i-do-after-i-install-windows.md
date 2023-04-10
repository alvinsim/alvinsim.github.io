---
title: 'Things I Do After I Install Windows'
date: Mon, 29 Feb 2016 17:35:55 +0000
draft: false
tags: ['chocolatey', 'duckduckgo', 'MS WIndows', 'opera', 'windows']
---

1\. Connect to a (trusted) network
----------------------------------

After the Windows installation completes successfully, I'd connect it to the Internet. This is so that I can update Windows with the latest security patches, and download the necessary applications.

2\. Windows Update
------------------

It is always important to always keep your Windows (or any other OS you use) up-to-date with the latest security patches and updates.

3\. Check Windows Settings
--------------------------

For Windows prior to Windows 10, I would configure Windows Update to notify only and not download. But in Windows 10, this setting is no longer there. Windows 10 will automatically download and install latest updates. The options you can configure for Windows 10 Windows Update are

*   Automatically restart Windows after updates are installed or delay it.
*   Update other Microsoft products i.e. Microsoft Office.
*   Peer-to-peer downloads for updates. Specifically for Windows 10, check the "Privacy" settings. Go through all the items and turn them off, or just allow access for certain apps.

4\. Turn-on Windows Defender
----------------------------

For me Windows Defender is suffice. To turn it on, launch Windows Defender and click on the big red "Turn On" button.

5\. Install Chocolatey
----------------------

This is a must have in all my Windows machine. It is a package management for Windows similar to `apt-get install [package_name]` for Debian-based distros or `yum install [package_name]`.

I use Chocolatey because

1.  It saves me time installing softwares on a fresh Windows.
2.  It automatically resolves package dependencies i.e. Chocolatey will automatically install any of the package's pre-requisite packages before continuing.
3.  The packages are safe because each package's version are approved by moderators.

The only downside I experienced is sometimes latest version of packages might take awhile to be approved. But, you can still install them by appending the `--version` flag in the command e.g. `choco install skype --version=7.18.0.111`.

To install Chocolatey, open an **_administrative_** command prompt and paste the following command:

`@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin`

Now you can start to install packages. To install a package, open an **_administrative_** command prompt and type `choco install [package_name]` e.g. `choco install skype`.

Chocolatey allows you to install more than one package in a single command e.g. `choco install skype opera conemu`.

If you do not know the name of the package, you can use the command `choco list [package_name]` and it will output packages related to the one you entered. Or you can also search for the package at the [Chocolatey website](https://chocolatey.org/).

With Chocolatey, you can keep packages updated with the latest (approved) version (_only if they were installed using the `choco install` command_) by using the command `choco upgrade all`. Or you can specify certain packages to update `choco upgrade skype`.

6\. Install must-have applications (via Chocolatey)
---------------------------------------------------

After installing Chocolatey, I'll open an **_administrative_** command prompt and use the following command.

`choco install ccleaner 7zip adobereader libreoffice vim teracopy winscp wget putty emacs opera curl skype pidgin evernote git hg calibre f.lux imgburn onedrive paint.net spotify keepass pushbullet conemu sublimetext3 sublimetext3.packagecontrol youtube-dl ffmpeg vim -y`

7\. Checkout my dotfiles from my Bitbucket Repo
-----------------------------------------------

I will then proceed to checkout my `dotfiles` repo from [my Bitbucket repo](https://bitbucket.org/alvinsim/dotfiles).

It mainly contains my emacs and vim configuration.

8\. Configure Web Browsers
--------------------------

I use Opera as my default browser, but this applies to all other browsers as well.

Below are the settings I would change.

*   Set DuckDuckGo as the default home page - [\[https://duckduckgo.com\]](https://duckduckgo.com).
    
*   Set DuckDuckGo as the browser's default search engine (_Install the DuckDuckGo extension or plug-in if available_).
    
*   Clear cookies when I close the browser.
    
*   Set browser plug-ins to only enable when they are clicked, such as flash.
    
*   Do not allow the browser to track my physical location.
    
*   Set the browser to ask for permission when sites want to use the microphone and camera.
    
*   Set the browser to send a `do-not-track` request in the browsing traffic.
    
*   Do not save passwords.
    

\--

_\[**UPDATE** - 7 Oct, 2016\] Removed image because of its [Creative Commons License](https://creativecommons.org/licenses/by-nc-sa/2.0/)._