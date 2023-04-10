---
title: 'Which ''yarn''?'
date: Mon, 31 Aug 2020 15:51:21 +0000
draft: false
tags: ['cmdtest', 'debian', 'javascript', 'linux', 'Linux/Unix', 'yarn']
---

This has happened to me each time I setup a new Debian or Ubuntu environment. Firstly, the `yarn` command I am referring to here is the JavaScript "Yarn" package manager. The `yarn` that was installed or already installed was the one used by the [`cmdtest`](https://manpages.debian.https://manpages.debian.org/testing/cmdtest/yarn.1.en.html).

I thought I had `yarn` installed when I checked using the command `which yarn` and out printed `/usr/bin/yarn`.

```
$ which yarn
/usr/bin/yarn 
```

When I ran `yarn upgrade` I got this weird error message:

```
~/src/a-javascript-project $ yarn upgrade
00h00m00s 0/0: : ERROR: [Errno 2] No such file or directory: 'upgrade' 
```

This seemed strange. Why is `yarn` looking for a file or directory called 'upgrade'. Did I use the wrong option? Is it `upgrade` or `update`?

I checked the `yarn`'s `man` page to confirm and then saw the name and realised something is not right. It showed "yarn - scenario testing of Unix command-line tools".

At this point, it dawned on me that it's the wrong `yarn`!

This is a [known issue](https://groups.google.com/forum/#!topic/linux.debian.devel/ceNMToPakhw) in Debian and Debian-based distros, like Ubuntu.

To fix this, we can't run the command `sudo apt remove yarn` because `yarn` is not a package. It belongs to the `cmdtest` package. So, we have to remove the `cmdtest` package instead and then only install the correct `yarn`, preferably using `npm install -g yarn`.

I hope this helps if you are also facing the same problem.

–