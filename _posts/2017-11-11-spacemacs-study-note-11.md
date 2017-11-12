---
layout: post
title: Spacemacs Rocks Note Day 11
description: A series of notes that I learn Emacs hacking. Spacemacs installation and some introduction to layers, a read list and some tips. 
permalink: /spacemacs-study-note-11/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-11-11 12:34:56
---

# Spacemacs!

## Installation

Clone from Github. It is a set of configuration, so it is based on Emacs.

Rmember to backup the current configurations in `~/emacs.d`.

```sh
git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d 
```

In the first place, the system will ask which edit mode:

-   Vim
-   Emacs

Let's choose `vim`. Yeah! I start to learn `vim` from scratch.

Second question, what distribution would you like to install

-   Spacemacs (recommended)
-   Spacemacs-base

The second one is more like a customized version with less packages installed.

## Try leader key in `evil-mode`

-   `SPC f e d`: Go to the `.spacemacs` file and jump to `user-init` section=.
-   `SPC f j`: open `dired-mode` and locate current file.
-   `SPC f e R`: rerun the `.spacemacs` file to make changes. We don't need to restart Spacemacs from now on.
-   `SPC f e v`: check the current version of Spacemacs.
-   `SPC q R`: restart Spacemacs
-   `SPC h SPC <layer-name>`: check what packages are installed for the given layer.
-   `SPC s s`: gUse `swiper` to search in the document.
-   `F11`: maximize the window.

## Add some layers to Spacemacs

-   Open `.spacemacs`, find the function `dotspacemacs-configuration-layers`.
-   Uncomment the layer we need, for example, `org`, `auto-complete`, `git`, `markdown`, `spell-checking`, `syntax-checking` etc.
-   Remember the layer is not packages. It is a set of packages.

## To Read

-   [Documentation of Spacemacs](http://spacemacs.org/doc/DOCUMENTATION.html)
-   [FAQ](http://spacemacs.org/doc/FAQ.html#common)

Actually most of the stuff that shall be recorded here are already in the FAQ or documentation. Read them carefully if you want to master Spacemacs or maybe Emacs.

## More tips

-   All additional package should be put in `dotspacemacs-additional-packages` in the `.spacemacs` file.
-   Search "exclude" on [Emacs-China](https://www.emacs-china.org) to find the list that may be potentially removed safely. Thus improve the start up performance.
-   Before you can write your own layer, put all the config in `user-config` function.
-   Find more available "official" layers on spacemacs Github repo, or [Configuration layers](http://spacemacs.org/layers/LAYERS.html).
-   Some other example themes:
    -   spacemacs-dark
    -   spacemacs-light
    -   solarized-light
    -   solarized-dark
    -   leuven
    -   monokai
    -   zenburn
-   A list of Spacemacs cheat sheet can be found [robphoenix/spacemacs-cheshe.md](https://gist.github.com/robphoenix/9e4db767ab5c912fb558).
