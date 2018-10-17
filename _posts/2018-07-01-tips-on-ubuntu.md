---
layout: post
title: Tips on Ubuntu
description: Some quick fixes and minor hacks on Ubuntu. I update it every now and then.
permalink: /tips-on-ubuntu/
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

## Change file owner and user group

Suppose the file name is "so\_happy.org"

```sh
sudo chown user:group so_happy.org
```

The `user` and `group` are the ones you want to set.

## Change file permission

Allow file execution:

```sh
sudo chmod +x your_file
```

Set read/write/execute

```sh
sudo chmod 755 your_file
```

There are three bits to represent readable/writable/executable. Then 000 - 111 are mapped to 0-7 decimal digits.

The three digits in the command are owner, group, others.

Read more: [AskUbuntu](https://askubuntu.com/q/932713).

## Hold back a package in `apt upgrade`

[Link](https://askubuntu.com/questions/99774/exclude-packages-from-apt-get-upgrade).

```sh
sudo apt-mark hold <package>
```

[] TODO How to ignore packages in Ubuntu Software Updater?

## Change End-of-Line (EOL) of a file

[Link](https://askubuntu.com/questions/803162/how-to-change-windows-line-ending-to-unix-version).

Install `dos2unix`.

```sh
sudo apt install dos2unix
```

Process file with it.

```sh
dos2unix input_file.txt output_file.txt
```

This is especially helpful for the file `~/.aspell_pws/.aspell.en.pws`. Once Spacemacs is run on Windows, the EOL will be changed to DOS (I synchronize this file with Dropbox).
