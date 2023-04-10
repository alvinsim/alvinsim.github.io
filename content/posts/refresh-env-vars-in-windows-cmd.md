---
title: 'Refresh Environment Variables in Windows Command Prompt'
date: Sat, 18 Aug 2018 12:24:30 +0000
draft: false
tags: ['MS WIndows']
---

Have you ever added an environment variable in Windows and having to close and re-open the command prompt just to use it? Or worse, having to reboot Windows.

I just found this cool command when I used [Chocolatey](https://www.chocolatey.org/) to install [maven](https://maven.apache.org/). Right at the end of the installation, Chocolatey prompt me to run the `refreshenv` command to have the environment variable change(s) take effect without re-opening the command prompt.

```
alvin@ALVINSIM-HP C:\Users\alvin\
> refreshenv
Refreshing environment variables from registry for cmd.exe. Please wait...Finished.. 
```

For those who are familiar with Unix, the `refreshenv` command behaves the same as the `source` command. For example, if you have made some changes to the `.bashrc` file, you would run the command `source ~/.bashrc`.

After digging further, I found out that this command is part of Chocolatey. It is located at `C:\ProgramData\chocolatey\bin`, or which ever path you installed Chocolatey.

```
alvin@ALVINSIM-HP C:\ProgramData\chocolatey\bin
> dir refreshenv.cmd
 Volume in drive C is Windows
 Volume Serial Number is XX9X-97XX

 Directory of C:\ProgramData\chocolatey\bin

05/11/2018  09:32 AM             2,283 RefreshEnv.cmd
               1 File(s)          2,283 bytes
               0 Dir(s)  54,360,322,048 bytes free 
```

If you have never heard of Chocolatey, I wrote about it briefly at [another post](http://www.alvinsim.com/things-i-do-after-i-install-windows/). It is basically a package manager for Windows. I use it to find, install and update applications on my Windows machine. This is same with the `apt` or `yum` command in some Linux distros, or `brew` from Homebrew if you are on MacOS.

–