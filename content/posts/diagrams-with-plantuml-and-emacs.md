---
title: 'Diagrams With PlantUML and Emacs'
date: Sat, 15 Apr 2017 15:13:21 +0000
draft: false
tags: ['emacs', 'org-mode', 'plantuml', 'UML', 'uml', 'windows']
---

Starting With Dia
=================

When I had to draw [UML diagrams](https://en.wikipedia.org/wiki/Unified_Modeling_Language#Diagrams), the tool I first used was [Dia](https://wiki.gnome.org/Apps/Dia/) - an open-sourced diagraming software. Dia is a great tool. I have not used [Microsoft Visio](https://en.wikipedia.org/wiki/Microsoft_Visio) before, so I cannot compare what short-comings it has compared to Visio.

The other tool I tried was [yEd](http://www.yworks.com/yed). I did not feel comfortable using it, and always went back to using Dia.

Couple of years ago, with a new job, I had to draw lots of [sequence diagrams](https://en.wikipedia.org/wiki/Sequence_diagram). And drawing them using Dia was a bit tedious. So, I went to the interwebs and stumbled upon [WebSequenceDiagrams](https://www.websequencediagrams.com).

Next Was WebSequenceDiagrams
============================

Using WebSequenceDiagrams to draw sequence diagrams was fun and fast. Instead of the conventional way of using the mouse to drag-and-drop the objects and linking them together and setting the necessary properties, you just have to type it. Yes! TYPE! It uses a simple code syntax and WebSequenceDiagrams will render the it into a diagram.

For example, the code snippet below will render into the diagram below.

```
title Authentication Sequence

Alice->Bob: Authentication Request
note right of Bob: Bob thinks about it
Bob->Alice: Authentication Response 
```

![img](http://www.alvinsim.com/wp-content/uploads/2017/04/Authentication_Sequence.png "Image generated from WebSequenceDiagrams.")

Once you get familiar with the code syntax, generating sequence diagrams is blazingly fast! Not only that, but it has other features for non-premium users, such as applying different styles to your diagram, print, export your diagram to image or PDF, etc. Using WebSequenceDiagrams as a free service is suffice, if you do not mind their logo as a watermark in all your diagrams. Be a paying customer, and you will unlock other [premium features](https://www.websequencediagrams.com/order.html) including no watermark in all your diagrams.

And Then, Came PlantUML
=======================

I lived with the watermark for awhile, until I came across [PlantUML](http://plantuml.com). It is a [Java](https://en.wikipedia.org/wiki/Java) library which parses your diagram's code to generate the diagram. And guess what? It uses the same code syntax as the one you use in WebSequenceDiagrams! Then only I realised that from [here](http://plantuml.com/external-links) that WebSequenceDiagrams actually is using PlantUML to generate the diagrams.

At this point, I tried the PlantUML plugin for [Sublime Text](http://www.sublimetext.com), [sublime\_diagram\_plugin](https://github.com/jvantuyl/sublime_diagram_plugin). Unfortunately, this plugin is not available in [Package Control](https://packagecontrol.io). So, it had to be installed manually. :(

Besides that, because [IntelliJ IDEA](http://www.jetbrains.com/idea/) is my main Java IDE (and currently my favourite) at work, I also installed the PlantUML plugin for it.

But using PlantUML with both Sublime Text and IntelliJ IDEA was not at all fun.

Since I began to use [Emacs](https://www.gnu.org/software/emacs/) more now, I explored at how to get PlantUML working in Emacs.

[According to PlantUML](http://plantuml.com/emacs), are there few ways to do that. I opted for the easier one, which is to use [Org Babel](http://orgmode.org/worg/org-contrib/babel/intro.html). Babel now supports PlantUML code. Hooray! Well, actually since August of 2010.

Setting it up in Emacs is pretty straight forward. And this also works without much additional configuration if you are unfortunately using Windows.

1.  Download the PlantUML JAR file from [here](http://sourceforge.net/projects/plantuml/files/plantuml.jar/download) and put it in a location somewhere. I installed [PlantUML via chocolatey](https://chocolatey.org/packages/plantuml), so it is located at `C:\ProgramData\chocolatey\lib\plantuml\tools\plantuml.jar`.
2.  If you need to use PlantUML to do other types of diagrams other than sequence diagrams, then you will need to [install Graphviz](http://plantuml.com/graphviz-dot). As always, I used chocolatey by running the command `choco install graphviz`.
3.  Open your Emacs' config or init file - `$HOME/.emacs.d/init.el` or in Windows `%HOMEPATH%\AppData\Roaming\.emacs.d\init.el` and add the below code snippet to add PlantUML to `org-babel-load-languages`.
    
    (org-babel-do-load-languages 'org-babel-load-languages '((plantuml . t)))
    
4.  Next we will need to tell Org mode where the `plantuml.jar` file is by using the code snippet below.
    
    (setq org-plantuml-jar-path (expand-file-name "/path/to/plantuml.jar"))
    

Once that is done, create a new `org` file like so `C-x C-f some-org-file.org RET`. Then you can start writing PlantUML code within the `#+begin_src` and `#+end_stc` blocks.

Your `org` file will look something like below.

```
#+begin_src plantuml :file my-diagram.png
title Authentication Sequence

Alice->Bob: Authentication Request
note right of Bob: Bob thinks about it
Bob->Alice: Authentication Response
#+end_src 
```

To execute the code and generate the diagram, move the cursor to anywhere in the code and run `C-c C-c y RET`. The diagram will be generated to the file name specified e.g. my-diagram.png. This will be shown in the results section in the org file, like below.

```
#+results:
file:my-diagram.png 
```

You can then open the file, which is located in the same directory of the org file.

I Did That, But Got An Error Instead :(
=======================================

I tried this on another machine, my home laptop. When evaluating the PlantUML code, I got this error message "Evaluation of this plantuml code block is diabled".

![img](http://www.alvinsim.com/wp-content/uploads/2017/04/sample-plantuml-with-error.png "Emacs cannot evaluate plantuml code")

DAMN!

Checking my `init.el` again and again, and I didn't find anything wrong with it.

Then, I checked my emacs packages in `%HOMEPATH%/AppData/Roaming/.emacs.d/elpa` and found two different versions of Org packages installed.

I removed both versions, re-started emacs and re-installed the Org package again.

YAY! Finally, the code block evaluated successfully and the diagram was generated.

What's Next?
============

As mentioned above, when the code is successfully evaluated, Org will generate the diagram and append the link to it in the Org file.

Now, if you click on the link or you bring your cursor to the link and hit `C-c C-o`, Emacs will split into another window and display the image there.

Unfortunately, what I got was only this :(

![img](http://www.alvinsim.com/wp-content/uploads/2017/04/emacs-not-displaying-the-diagram-correctly.png "Emacs not able to display the diagram")

Searching the interwebs again, brought me to this [Stackoverflow post](https://stackoverflow.com/questions/2650041/emacs-under-windows-and-png-files). But trying the solutions there didn't work for me.

But, the main point was, I was missing some libraries in Windows or emacs.

This is what I tried.

1.  In your web browser, go to [emacs download page for windows](https://ftp.gnu.org/gnu/emacs/windows/).
2.  Depending on the version of emacs you have, download this extra file with the word "deps" in between. For me, I have emacs major version 25 installed, so I downloaded the `emacs-25-x86_64-deps.zip` file. Well, if we all RTFM, it is already stated there in the `README` file.

> We also provide a set of optional dependencies, in emacs-25-x8664\-deps.zip or emacs-25-i686-deps.zip respectively, which provide Emacs with an number of additional capabilities. To add these, unpack them directly over the emacs directory structure.

1.  Copy the downloaded dependencies zip file to your emacs directory i.e. the path you installed emacs. Example for me, I used the command `copy %HOMEPATH%/Downloads/emacs-25-x86_64-deps.zip %HOMEPATH%/AppData/Local/emacs/`.
2.  Extract the contents of the zip file.
3.  Delete the zip file.
4.  Re-start emacs.

Now, open the org file again and click on the file link, or move the cursor to it and hit `C-c C-o`.

Voilà!

![img](http://www.alvinsim.com/wp-content/uploads/2017/04/emacs-displaying-the-diagram.png "Emacs can now display the diagram")

However, this is not an issue if you are on a Unix/Linux system. By default, when emacs is built from source, the graphic libraries, such as PNG, JPEG, GIF, SVG, etc., are selected by default. On FreeBSD when you first install emacs either using the `make` or `portmaster` command, you'll be presented with the configuration screen, as shown below.

![img](http://www.alvinsim.com/wp-content/uploads/2017/04/emacs-config-graphics.png "FreeBSD emacs' make config for")

There Is More?
==============

Isn't it a bit cumbersome to do that each time we want to see the diagram(s) inside emacs.

So, I was thinking "Can we just display the image right there, like inline, instead of another window?"

Searching the interwebs again, I realised this is already supported in Org mode.

To toggle it, you can either type `M-x org-toggle-inline-images RET` or with the key-binding `C-c C-x C-v`.

By doing this, you will see something like so.

![img](http://www.alvinsim.com/wp-content/uploads/2017/04/emacs-displaying-the-diagram-inline.png "Emacs diplay diagram inline")

And We Are Done!
================

Finally, we are done. We are able to get emacs to display images and also to write PlantUML code to generate UML diagrams. Unfortunately, more effort if you are on Windows.

–