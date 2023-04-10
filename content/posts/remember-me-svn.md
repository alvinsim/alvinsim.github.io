---
title: 'Remember Me, Subversion'
date: Wed, 22 Mar 2017 16:17:11 +0000
draft: false
tags: ['authentication', 'hack', 'subversion', 'subversion', 'tortoisesvn', 'windows']
---

Every three months, my workplace's network domain will prompt to change our password. And this tri-monthly exercise would affect all the other intranet sites and systems, namely [Subversion](https://en.wikipedia.org/wiki/Apache_Subversion) (SVN). Now, this is not a major problem because the organisation uses [single sign-on](https://en.wikipedia.org/wiki/Single_sign-on) via [LDAP](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol) or [Active Directory](https://en.wikipedia.org/wiki/Active_Directory) i.e. you can access the other intanet sites or systems with the same User ID and password.

But recently, I noticed SVN doesn't remember me, even when I clicked on the "Save authentication" check box at the [TortoiseSVN](https://en.wikipedia.org/wiki/TortoiseSVN)'s authentication window.

![img](http://www.alvinsim.com/wp-content/uploads/2017/03/tortoisesvn-auth.png)

As I later found out, this is no fault of TortoiseSVN, although I am using an older version of it - `TortoiseSVN 1.6.16, Build 21511 - 64 Bit , 2011/06/01 19:00:35`. This is because saving my authentication credentials via [IntelliJ IDEA](https://en.wikipedia.org/wiki/IntelliJ_IDEA) doesn't work too.

Frustrated, I searched the interwebs and found [the same question asked in Stack Overflow](http://stackoverflow.com/questions/5048718/tortoisesvn-not-saving-authentication-details#5769231).

There are several possible solutions that might worked, but I only tried one, which is the one below.

### Remove the `Subversion\auth` folder

*   Depending on the version of Windows you are using, this folder might reside in `%APPDATA%\Subversion\auth` if you are using Windows XP; or `%APPDATA%\Roaming\Subversion\auth` for Windows 7 and later.
*   Using Windows Explorer, go to the `subversion` folder, click on the `auth` folder and hit the `DEL` button.
*   If you are using the `CMD` prompt, just use the command `rmdir /S /Q %APPDATA%\Subversion\auth` or `rmdir /S /Q %APPDATA%\Roaming\Subversion\auth`, depending on your Windows version.

This is ad-hoc solution. I have also tried [this other answer](http://stackoverflow.com/a/16286870) and hope it works without removing the `Subversion\auth` folder.

–