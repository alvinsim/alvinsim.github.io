---
title: 'A Better Web Experience with the Keyboard'
date: Mon, 29 Jul 2019 11:57:06 +0000
draft: false
tags: ['chrome', 'firefox', 'keyboard', 'Productivity', 'productivity', 'web']
---

When I use a computer, I like to have both hands on the keyboard, or specifically on the [home row](https://www.dictionary.com/browse/home-row). I find that it is more productive than having to move them to grab the mouse every few seconds. This is one reason I am grateful for

*   Software with great keyboard shortcuts and also that are easily customisable.
*   Terminal (or terminal emulator) and command prompt which you do not really need to use the mouse.
*   Websites with great keyboard shortcuts support like [Gmail](https://mail.google.com), [Remember The Milk](https://www.rememberthemilk.com/), [DuckDuckGo](https://duckduckgo.com), etc.
*   Lenovo ThinkPad laptops with the strategically placed Trackpoint and I like their keyboards too.

The main focus of this article is about website navigation with the keyboard.

Making a website keyboard accessible or compatible is one of the aspects of web accessibility. Unfortunately, most websites and web applications are built with minimal keyboard support and rely a lot on the mouse. The usual supported keyboard navigation in web browsers are the `<Tab>`, `Alt` `<Left/Right Arrow>`, `<Enter>`, `<Space>`, `Shift` `<Space>`, `Ctrl` `<TAB>`, etc. These are fine. But imagine if you had to open a link and your mouse or trackpad refuses to work properly and the link is 20 `<Tab>` s away. Or, you have to fill in some details into a complicated web form.

There is an extension (add-on) for that
=======================================

![img](/images/sakakey-logo_with_title.png)

There is a web browser extension or add-on which improves the user experience of navigating a website using a keyboard and it is called [Saka Key](https://key.saka.io/docs/about/introduction).

I stumbled upon this when I was searching on the internet on how to change one of Firefox's keyboard shortcut, which was the `/`. In one of the previous versions of Firefox, this key was mapped to the `Ctrl` `f` or "Find" command. And coincidentally, it is also the key which [DuckDuckGo](https://duckduckgo.com) uses to have the cursor focus on the "Search" input field. So, that was a bit annoying for me.

Unfortunately, I couldn't find any help topics or documentation or anywhere inside Firefox's settings on how to change its default keyboard shortcuts. But, one search result pointed to this browser extension.

![img](/images/sakaKey.png)

What Saka Key does is quite unique. Besides providing a default and configurable list of keyboard shortcuts, it also finds links and other interactive HTML elements in the web page and assigns random keymaps to them. You can see the keymaps highlighted in the screen capture above. To toggle the keymaps, press the `ff` key. To hide them, press the `<ESC>` key. Once the keymaps are displayed, you can then hit the specific letter to go to the link or focus on a form element.

Saka Key is an [open source project](https://github.com/lusakasa/saka-key) and supports both Firefox and Chrome, including Chromium-based web browsers like Brave, Vivaldi, Opera, etc.

Here are some of its keyboard shortcuts that I often use.

*   **`ff`:** Open link in the current tab.
*   **`fb`:** Open link in a background tab.
*   **`fi`:** Focus cursor on a form element.
*   **`i` or `o`:** Move the tab to the left/right.
*   **`w` or `q`:** Go to the next/previous tab.
*   **`cc` or `vv`:** Go back/forward based on your browser's history.
*   **`rr`:** Reload the tab.
*   **`j` or `k`:** Scroll up or down.
*   **`Shift` `j` or `Shift` `k`:** Scroll half page up or down.
*   **`gg`:** Scroll to the top.
*   **`Shift` `g`:** Scroll to the bottom.

If you haven't noticed, they are quite similar to vim's key bindings.

Users also have the option to change the keyboard shortcuts or delete them. And there are options to import or export your settings.

There is also a blacklist section for users to specific websites which they do not want to use Saka Key on. For me, I have Gmail in the blacklist as my fingers are already accustomed to its default keyboard shortcuts.

Conclusion
==========

To me, Saka Key is a great browser extension or add-on to have, especially when we use the web browser most of the time, for work and leisure. There are times when we do need to use the mouse such as to draw diagrams, drag-and-drop things, games, interacting with annoying i-am-not-a-robot CAPTCHAs to click on busses, storefronts, pedestrian crossings, traffic lights, etc. But with just the keyboard, you'd start to notice you get more work done and quicker.

–
