---
layout: post
title: Things to Do After Installing Ubuntu
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

### Chrome

Of cause.

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

Just follow the instructions. Remember to add the `.griveignore` file before running `-grive -a` command.

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
-   Chinese fonts

## Emacs Configuration

1.  First `git clone` the `.emacs.d` to `~` directory.
2.  Use symbolic link to create `~/.spacemacs.d` folder.

## Replace `Caps Lock` by `Ctrl`

Tutorial: [MovingTheCtrlKey - EmacsWiki](https://www.emacswiki.org/emacs/MovingTheCtrlKey)

Install `GNOME Tweaks` and changes the settings: `Keyboard & Mouse` -> `Additional Layout Options` -> `Caps Lock key behavior` -> `Caps Lock is also a Ctrl`.
