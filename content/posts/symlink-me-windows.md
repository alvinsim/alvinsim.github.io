---
title: 'Symlink Me, Windows!'
date: Fri, 08 Jun 2018 17:01:39 +0000
draft: false
tags: ['mklink', 'MS WIndows', 'symbolic-links', 'windows']
---

Microsoft Windows has this feature called [symbolic links](https://en.wikipedia.org/wiki/Symbolic_link) since Windows Vista. But, I am guessing not many are aware of this feature, nor did I. It wasn't until I had a need for it and tried searching if there were any 3rd party applications which provided this feature. And I found [this How-To Geek article](https://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/). Eventually, I found [other articles](https://duckduckgo.com/?q=windows+symlink) on this subject.

What are symbolic links?
========================

Symbolic links are pointers referencing to another file or directory at a different location. Or, you can call them virtual file or directory. You can open a symbolic link file and the referenced file actually opens. You can, in a command prompt, `cd` to a symbolic link directory and you will be "transported" to the referenced directory.

But, didn't Windows already have shortcuts?
===========================================

Yes, but symbolic links are way better. The Windows shortcut is just a `.lnk` file which tells Windows the file or directory it is referencing to. Double-click on the shortcut in the Windows Explorer, Windows will open the file with its associated software, or go to that directory in Windows Explorer.

But, there are some things which cannot be done with a Windows shortcut.

Firstly, in the command prompt, when you have a Windows shortcut pointing to a directory, you cannot actually use the `cd` command to change to that directory by calling the shortcut. Because Windows only sees it as an ordinary file.

Example: In my directory, I have the following files and directories.

```
C:\Users\alvin\Dropbox>dir
 Volume in drive C is Windows
 Volume Serial Number is SSSS-XXXX

 Directory of C:\Users\alvin\Dropbox

12/05/2016  10:45 AM    <DIR>          .
12/05/2016  10:45 AM    <DIR>          ..
11/26/2016  01:20 PM    <DIR>          blogs
04/24/2016  09:27 AM    <DIR>          book
02/04/2016  05:08 PM           836,507 Bookmarks
04/24/2016  09:26 AM    <DIR>          Camera Uploads
02/05/2016  10:45 AM             1,187 haha.txt.lnk
01/26/2016  01:20 PM    <DIR>          home
04/24/2016  12:00 AM    <DIR>          Public
02/05/2016  10:42 AM               947 Shortcuts.lnk
07/28/2009  03:36 PM               240 This is your Dropbox.txt
09/14/2016  11:10 PM    <DIR>          work
             6 File(s)      1,752,496 bytes
             8 Dir(s)  660,582,707,200 bytes free 
```

`Shortcuts.lnk` is a shortcut to another directory. But I cannot run `cd Shortcuts.lnk` in the command prompt. Instead, in the command prompt, you can type `Shortcuts.lnk` and a Windows Explorer will open.

Secondly, following to that point, syncing a Windows shortcut will only sync the `.lnk` file and not the referenced file or directory.

How to create a symbolic link?
==============================

In Unix systems, symbolic links are created using the `ln -s` command. But, of course, the same cannot be applied to Windows.

The way to do it in Windows is to use the command prompt, but with administrator privileges. Very unfortunate that this is the only way and there are no options in the right-click context menu either. There are third-party softwares though, which you can use. But, I won't discuss that in this post.

Open a command prompt and run it as administrator. Then type `mklink /?`. This will display the usage and option when using this command.

```
C:\Users\alvin\Dropbox>mklink /?
Creates a symbolic link.

MKLINK [[/D] | [/H] | [/J]] Link Target

        /D      Creates a directory symbolic link.  Default is a file
                symbolic link.
        /H      Creates a hard link instead of a symbolic link.
        /J      Creates a Directory Junction.
        Link    Specifies the new symbolic link name.
        Target  Specifies the path (relative or absolute) that the new link
                refers to. 
```

What type of links can I create with `mklink`?
==============================================

There are three types of links you can create with the `mklink` command.

*   **hard link:** can only be used for files and not directories.
*   **junction:** also called a soft link, is similar to a hard link, except that it can reference directories on different volumes on the computer.
*   **symbolic link:** Similar to junction and can be viewed as an upgrade of junction.

How does this benefit me as a normal Windows user?
==================================================

Using It For Syncing Files
--------------------------

One benefit of using symbolic links is when you use a file syncing or backup application, like Dropbox. Use the `mklink` command to create a symbolic link inside the Dropbox directory, and your files will be synced across all of your devices. There is no need to copy the directories or files to the Dropbox directory.

Using It For Java Projects
--------------------------

Another one of my use cases for symbolic links is when you build or run your Java project in Windows and you encounter the nasty error message "_CreateProcess error=206, The filename or extension is too long_". This is a limitation in Windows when executing a file with a long file name.

In my case, it happened at one of my previous work place when running [ant](https://ant.apache.org/) scripts to build the Java project. The `ant` script failed due to this error message because this project was referencing quite a number of Java library files, or what we call [jar](https://en.wikipedia.org/wiki/JAR_(file_format)) files, in the `-cp` or `-classpath` option. The more library or `jar` your project refers to, the longer the executing file name.

So, I created a symbolic link to `C:\`. And, this made the `classpath` shorter.

Of course, the other option is to create an uber jar file and have your `classpath` point to it only.

Deleting Symbolic Links
=======================

To delete symbolic links, you can do it as how you would delete a normal file i.e. right-click the symbolic link and click on `Delete`. Or in the command prompt, use the `del` command. But, when using the `del` command in the command prompt, it will remove files in the directory (not sub-directories), as well. This won't happen though if you delete it from Windows Explorer. This doesn't happen in Unix systems though. Looks more like a bug to me. Do keep this in mind!

Conclusion
==========

I do hope that this article has given you a better understanding of symbolic links in general. And you would start to use them to improve your work-flow and increase your productivity.

–