---
layout: post
title: Thinks to Do After Installing Ubuntu
description: A quick note. It includes installing packages and configuring the system.
permalink: /things-to-do-after-installing-ubuntu/
categories: [blog]
tags: [linux, system, OS, ubuntu]
date: 2017-11-27 16:34:56
---

# 　

## Package and Software to Install

Add `sudo` if needed.

### git

`apt install git`

-   Global settings
    -   `git config --global user.name "LanternD"`
    -   `git config --global user.email the_email@gmail.com`
    -   `git config --global core.editor emacs`

### Chrome

Of cause.

### pyenv

[Pyenv/pyenv - GitHub](https://github.com/pyenv/pyenv)

Don't forget the add `PATH` and `eval` stuff to the `.bashrc` (Step 3 in the installation tutorial).

After the installation, **use `pyenv` to install certain python version**.

`python global 3.6.x`

Get ride of every annoying version selection between Python 2.7.x and 3.6.x.

### pip

`apt install python-pip python3-pip`

### Emacs

`apt install emacs25`

### Vim

`apt install vim`

### Dropbox

Use the client provided by Dropbox

### Google Drive

In Ubuntu `Settings`, enter `Online Accounts`, and add `Google` account. After a while, the files in Google Drive will be synchonized as a mounted folder.

**Update**: the above method is not convenient. Use `Grive2` instead. [Grive2 - Github](https://github.com/vitalif/grive2)

Just follow the instructions. Remember to add the `.griveignore` file before running `grive -a` command.

### LaTeX environment

-   TeXlive
    
    `apt-get install texlive-full`
    
    It has 4.4 GB, so be patient.

-   PDF viewer: `Envice` by default in GNOME.
    
    `customize-variable RET tex-view-program-selection RET`, insert `evince` as `output-pdf` viewer.

### Ruby

Tutorial: [Ruby Installation](https://www.ruby-lang.org/en/documentation/installation/)

`apt-get install ruby-full`

The packages in ruby:

-   gem: `apt-get install rubygems`. (Usually it is included in the `ruby-full` installation.)
-   jekyll: `gem install jekyll bundler`.
    -   (`bundler` is required to run jekyll)
    -   Run `bundle install` after `bundler` is installed.
    -   `bundle exec jekyll serve`.

### WhatPulse

Tutorial: [WhatPulse Linux Installation](http://help.whatpulse.org/kb/client/linux-installation)

Optional.

### Zotero

-   [Installation guide](https://www.zotero.org/support/installation)
-   Zotfile: [Link](http://zotfile.com/)

### Sogou Pinyin Input Method

Tutorial: [Sogou Pinyin Official Help](https://pinyin.sogou.com/linux/help.php)

-   Make sure `fcitx` is installed.
-   Enter `im-config` in terminal, set the corresponding items.
-   Install Sogou Pinyin via the `.deb` package.
-   Let `fcitx` start after loging-in. Use `gnome-tweaks-tool` to do so.

### ag

Tutorial: [the\_silver\_searcher - Github](https://github.com/ggreer/the_silver_searcher)

A fast code searching tool.

`apt-get install silversearcher-ag`

### PostgreSQL

Tutorial: [How to Install PostgreSQL 10 on Ubuntu 16.04 and 14.04 LTS](https://tecadmin.net/install-postgresql-server-on-ubuntu/)

-   Installation

Add the Apt Repo to source list in Ubuntu and then sudo install.

`sudo apt-get install postgresql postgresql-contrib`

Python use `psycopg2` to manipulate the PostgreSQL database. Do not forget to install it as well.

`pip install psycopg2`

-   Setting user info

Tutorial: [Setting a password for the `postgres` user](http://suite.opengeo.org/docs/latest/dataadmin/pgGettingStarted/firstconnect.html#setting-a-password-for-the-postgres-user)

Use `psql` command and `\password` command to do so.

### pgAdmin

A python-written program that manage PostgreSQL. Install it using python wheel. Use python in system (not those in pyenv) to install. This app requires `sudo` permission to run.

## Remove Unused Folders in `Home`

Tutorial: [Ubuntu - permanently remove ~/Videos and ~/Public](https://superuser.com/questions/223918/ubuntu-permanently-remove-videos-and-public)

Change the following:

-   `~/.config/user-dirs.dirs`.
-   `/etc/xdg/user-dirs.conf`: `enabled=False`.
-   `/etc/xdg/user-dirs.conf`.

Then we can `rmdir` those folders.

## Add Fonts

Tutorial: [How To Install New Fonts In Ubuntu 14.04 and 16.04](https://itsfoss.com/install-fonts-ubuntu-1404-1410/)

Font list:

-   Source Code Pro
-   Operator
-   Fira Code
-   icon font (see `NeoTree` Github page)
-   Chinese fonts

## Emacs Configuration

1.  First `git clone` the `.emacs.d` to `~` directory.
2.  Use symbolic link to create `~/.spacemacs.d` folder.

## Replace `Caps Lock` by `Ctrl`

Tutorial: [MovingTheCtrlKey - EmacsWiki](https://www.emacswiki.org/emacs/MovingTheCtrlKey)

Install `GNOME Tweaks` and changes the settings: `Keyboard & Mouse` -> `Additional Layout Options` -> `Caps Lock key behavior` -> `Caps Lock is also a Ctrl`.
