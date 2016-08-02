---
layout: post
title: "Installing qtile on Ubuntu 16.04"
description: "Tutorial how to install the qtile window manager on Ubuntu 16.04 (probably also works on other versions)"
category: HowTo
tags: ["tutorial", "qtile", "howto", "ubuntu"]
---

As there is no ppa or official deb for Ubuntu for the [qtile window manager](http://qtile.org/) I decided to write this
guide. The official [docs page](http://docs.qtile.org/en/latest/manual/install/ubuntu.html) essentially only says that
you have to install from source and that there are no prebult packages for ubuntu and the ppa does not work.
So installing with pip is the way to go. To do that follow these steps.

```bash
# binary dependencies
sudo apt-get install python3-pip python3-xcffib python3-cairocffi libcairo2 libxcb-render0-dev libffi-dev libpangocairo-1.0-0 python-dbus

# install qtile
sudo pip3 qtile

```

Create the file `/usr/share/xsessions/qtile.desktop` with the following content

```bash
sudo vim /usr/share/xsessions/qtile.desktop
```

```ini
[Desktop Entry]
Name=Qtile
Comment=This session logs you into Qtile
Exec=qtile
Type=Application
DesktopNames=Qtile
```

Now you can log out and select Qtile as display manager when logging in.
