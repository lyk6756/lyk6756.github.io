---
layout: post
title: "Running X Window Graphical Application Via SSH"
---

SSH gives a solution of remote command-line login and remote command execution on Unix-like operating system. If you want to run server's software with GUI on your client however, unlike RFB (VNC) protocol, SSH itself is not applicable to windowing systems and applications at the framebuffer level. But we can enable SSH's X11 forwarding function and launch GUI using a X Window System display server if needed.

# Server setup

First, we need to configure our server (CentOS 7) to make sure it allows X11 forwarding.

Edit configuration file `/etc/ssh/sshd_config`, make sure the option

```
X11Forwarding yes
```

is enabled.

# Client setup

It will be quite easy if you are using a Linux system with GUI installed, which means you already have a X display at the local end. Simply add `-X` option while using `ssh` command:

```shell
$ ssh -X <username>@<hostname or IP address>
```

Then you can launch your GUI apps by command line.

If you are using a Microsoft Windows system, you need two programs installed before using, a SSH client and a X windows display server. Here I recommend two softwares, PuTTY and Xming.

* [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) is a free, opensource implementation of SSH and Telnet for Windows and Unix platforms, along with an xterm terminal emulator. Prortable EXE programs are provided on [PuTTY Download Page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

* [Xming](http://www.straightrunning.com/XmingNotes/) is an X11 display server for Microsoft Windows operating systems. [Public Domain Releases](https://sourceforge.net/projects/xming/files/) of [Xming X Server for Windows](https://sourceforge.net/projects/xming/?source=directory) are provided on SourceForge.

Here is a quick-start:

1. Install Xming, choose `Portable PuTTY Link SSH client - use with Portable PuTTY` while selecting components.
2. Launch Xming, choose `Start no client`
3. Launch SSH client and Enable X11 forwarding (Under category: *SSH -> X11*)
4. Login and enjoy

[This page](http://www.geo.mtu.edu/geoschem/docs/putty_install.html) gives a more detailed tutorial on Installing/Configuring PuTTy and Xming.

# Further reading

* [X Window System - wikipedia](https://en.wikipedia.org/wiki/X_Window_System)