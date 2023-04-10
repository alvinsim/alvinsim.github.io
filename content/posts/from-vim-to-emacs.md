---
title: 'From Vim To Emacs'
date: Sun, 19 Jun 2016 16:03:08 +0000
draft: false
tags: ['emacs', 'org-mode', 'Text Editors', 'vim']
---

_Disclaimer: This is not a "Vim vs Emacs" type of blog post. I wrote this to share my thoughts of using both of them._

Vim
===

![Vim](http://www.alvinsim.com/wp-content/uploads/2016/06/vim.png "Vim")

Vi or vim (_Vi IMproved_) is a text editor. It is installed on almost all of the \*nix systems. You can choose to use it with the GUI, or, use it in the terminal or command prompt.

I started using vim at around 2006/07. This was at one of my previous jobs where the servers were mainly \*nix based systems - IBM AIX (ver 5.x) and/or Red Hat-based distros.

It was really difficult when I first started.

But the more I used it, the more I grew to love it. My fingers were already used to the key-bindings.

I then started using [gvim](http://www.vim.org/download.php#pc) in my Windows machine. Not only that, I also installed [jVi](http://jvi.sourceforge.net/ReadmeNetBeans.html), a NetBeans plugins.

During this period, I did try to use [Emacs](https://en.wikipedia.org/wiki/Emacs). But, I got lost.

Emacs is not your ordinary text editor. Some say it is an Operating System because not only can you edit text, but also many other things e.g. manipulate the file system, check your emails, play games, project management, organize your tasks, documentation, etc.

Emacs
=====

After another job change, I had a problem. Prior to that, I was a big user of [Evernote](https://evernote.com/). I kept most of my work related notes there. But this organization, which I just joined, blocked access to Evernote.

I had to find an alternative. And I didn't want to use [Microsoft One Note](http://onenote.com/).

Then, I stumbled upon [org mode](http://orgmode.org/).

Org mode is a feature in emacs, or to be more precise, it is an [emacs major mode](http://www.tldp.org/HOWTO/Emacs-Beginner-HOWTO-3.html).

Quoting from its website, "_Org mode is for keeping notes, maintaining TODO lists, planning projects and authoring documents with a fast and effective plain-text system._"

Of course, one needs to understand emacs before starting to use org mode.

Now, at work and at home, I use org mode for

*   Notes, tasks lists, etc.
*   Writing documents and then exporting them to other formats.
*   Writing drafts of my blog posts.
*   Montly budgets and daily expenses.

Org mode is the only reason I am using Emacs, and I am still trying to use it as my default text editor.

![Screen capture of my emacs with this blog post draft](http://www.alvinsim.com/wp-content/uploads/2016/06/emacs.png "Screen capture of my emacs with this blog post draft")

To have an overview or introduction of org mode, go to [FLOSS Weekly](https://twit.tv/shows/floss-weekly) and download [Episode 136](https://twit.tv/shows/floss-weekly/episodes/136), where [Randal Schwartz](https://twit.tv/people/randal-schwartz) and [Aasron Newcomb](https://twit.tv/people/aaron-newcomb) interviewed [Carsten Dominik](https://twitter.com/carstendominik) - the creator of org mode.

For more resources on emacs or org mode, you can refer to the URLs below.

*   [Sacha Chua's blog posting on emacs and org mode](http://sachachua.com/blog/)
*   [youtube videos of how people are using org mode](https://www.youtube.com/results?search_query=org+mode)
*   [Emacs Life](http://emacslife.com)
*   [Org mode for Emacs - Your Life in Plain Text](http://orgmode.org)
*   [A guided tour of Emacs](http://www.gnu.org/software/emacs/tour/)

In case you missed it, there was a scene in [Tron Legacy](http://www.imdb.com/title/tt1104001/?ref_=fn_al_tt_1) where they showed a hacker using emacs. You can read the blog post [here](http://jtnimoy.com/blogs/projects/14881671-tron-legacy).

![Screen capture of Tron Legacy with emacs](http://www.alvinsim.com/wp-content/uploads/2016/06/tronLegacy-emacs.jpg "Screen capture of Tron Legacy with emacs. Source: http://jtnimoy.com/blogs/projects/14881671-tron-legacy")

Vim or Emacs
============

If you have not tried either of them and am wondering which one to learn, I would suggest vim. Vim is easier to learn and uses less key-strokes, as compared to emacs. Plus, vim is installed by default in most \*nix systems.

Once you know your way around vim, then go and try emacs. See which one suits you best.

"But why should I learn vim or emacs? I am already using '_insert-text-editor-name-here_'?"

If you with \*nix systems (at work or at home), I strongly recommend to learn either one, or start with vim. Many a time I have seen people ftp a file, which they want to edit in a \*nix system, to their Windows machine. Open the file using their favourite text editor and make changes and then ftp the file back to the server.

It would safe a whole lot of time if they had just ssh to the server and run `vim /path/to/file` or `emacs /path/to/file`.

Finally, there is no one text editor to rule them all. Everyone has their own use cases and preferences. Try them and see which one works for you.

\--