---
layout: post
title: "Automatic screenshot sharing with bepasty and scrot"
description: "Easily share a screenshot with scrot and bepasty"
category: Tools
tags: ["tools", "helpers", "linux"]
---

## What

I have running an instance of [bepasty](https://bepasty-server.readthedocs.io/en/latest/) and wanted to share
screenshots with it. I couldn't find a tool, so I wrote a small bash script that uses `scrot` to capture a screenshot,
`bepasty-client-cli` to upload the image, `xsel` to put the link in the clipboard and then opens `google-chrome` with
the link:

## Install dependencies

On Ubuntu (and debian?) you need to run this to install the dependencies:

```bash
sudo aptitude install xsel scrot python-pip
sudo pip install -e git+https://github.com/bepasty/bepasty-client-cli.git#egg=bepasty-client-cli
```

I tested with `3080f88bf13917b00b65a7210c7fe8c3efeeeb0c` in branch master. To install that specific version run:
```bash
# optional
pip install -e git+https://github.com/bepasty/bepasty-client-cli.git@3080f88bf13917b00b65a7210c7fe8c3efeeeb0c#egg=bepasty_client_cli
```


## Set up the script

Put the following script somewhere you find it later and make it executable (`chmod +x`). I have it in my home in the
file `.take_screenshot.sh`. Also replace the URL and password to match your installation:

```bash
#!/bin/bash

bepasty_url=https://paster.example.org
bepasty_pass=secretpass

old=`xsel -o -b`
sleep 0.1
f=$(scrot -s -e 'echo $f')
bepasty-cli -n screen.png -p $bepasty_pass -u $bepasty_url $f | tail -n 1 | xsel -i -b
url=`xsel -o -b`
if [ "$old" != "$url" ]
then
    google-chrome $url
fi
rm $f
```

You might also want to set up some keyboard shortcut in your window manager to call the script. In qtile you would put
something like the following in your `~/.config/qtile/config.py`:

```python
keys = [
    .... # other key bindings,

    Key([], "Print", lazy.spawn("bash /home/user/.take_screenshot.sh")),
]
```
