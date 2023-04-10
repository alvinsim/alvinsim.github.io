---
title: 'FreeBSD - Install Python 3 and Pip'
date: Sat, 09 Jul 2016 15:46:35 +0000
draft: false
tags: ['freebsd', 'pip', 'Python', 'python3']
---

I am starting a [Python](https://www.python.org/) web project, and taking this oppotunity to learn [django](https://www.djangoproject.com/) or [flask](http://flask.pocoo.org/). Development work will be done in my [FreeBSD](https://en.wikipedia.org/wiki/FreeBSD) [VirtualBox](https://www.virtualbox.org/) virtual machine.

Before I started, I checked if Python was already installed. And yes, it was already loaded with version 2.7.12.

```
[alvinsim@freebsd ~]$ which python
/usr/local/bin/python
[alvinsim@freebsd ~]$ python --version
Python 2.7.12
[alvinsim@freebsd ~]$ 
```

But, I wanted to develop using Python 3. So, I searched if there was a port for it.

```
[alvinsim@freebsd ~]$ psearch python3
accessibility/py3-atspi   Python3 API for the D-BUS based SPI framework
audio/py3-pylast          Python3 interface to Last.fm
devel/py3-dbus            Python3 bindings for the D-BUS messaging system
lang/python3              The "meta-port" for version 3 of the Python interpreter
lang/python33             Interpreted object-oriented programming language
lang/python34             Interpreted object-oriented programming language
lang/python35             Interpreted object-oriented programming language
www/mod_python33          Apache module that embeds the Python interpreter within the server
www/mod_python35          Apache module that embeds the Python interpreter within the server
x11-toolkits/py-wxPython30 GUI toolkit for the Python programming language
[alvinsim@freebsd ~]$ 
```

And there are four ports for Python 3.

To install, I ran the command `sudo portmaster lang/python3`. This will build from source, including its dependencies. Or if you prefer to fetch only the binary files and install them, you can run the command `sudo pkg install python3`.

```
[alvinsim@freebsd ~]$ which python3
/usr/local/bin/python3
[alvinsim@freebsd ~]$ 
```

After successfully installing Python 3, it has its own executable and it didn't override the current one.

As for `pip`, it is used to install/update python packages in your project. Based on the [pip documentation](https://pip.pypa.io/en/stable/installing), it is already installed if you are using Python 2 >= 2.7.9 or Python 3 <= 3.4. Before using `pip`, we need to upgrade it first. I ran the command `python3 -m pip install -U pip`. And it was successfully upgraded.

Now, I can start on my project.

–