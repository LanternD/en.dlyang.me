---
layout: post
title: Tips on Ubuntu
description: Some quick fixes and minor hacks on Ubuntu. I update it every now and then.
permalink: /Tips-on-ubuntu/
categories: [blog]
tags: [Ubuntu, operating system, tips]
date: 2018-07-01 20:20:39 
---

# A Few Words

I encounter problem every now and then on Ubuntu. I decide to take some notes on what I get when searching through websites like StackOverflow.

Last update: 2018-07-01

# Tips

## How to add a `.desktop` executable file to start menu and "favorites"?

`.desktop` file usually comes with the software packages in `.tar.bz` format, for example, Zotero. When you double click to execute the `zotero.desktop`, you can not add it to the side bar (favorites). The solution is:

```sh
ln -s ~/Software/Zotero_linux-x86_64/zotero.desktop ~/.local/share/applications
```

I just use Zotero to illustrate, other software is likewise. After the symbol exists, you can find it in start menu by press the super (win) key. Open Zotero, and now you can add it to the side bar by right clicking the icon.
