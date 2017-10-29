---
layout: post
title: Spacemacs Rocks Note Day 1
description: A series of notes that I learn Emacs hacking. Basic key mapping and functions; Emacs start up settings; introduction to "modes", company-mode; basic of package management; introduction to org-mode.
permalink: /spacemacs-study-note-1/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-10-22 22:34:56
---


# Emacs basics


## Key meaning

-   `M-x`: execute an interactive function
-   `C-x C-f`: Open file
-   `C-x C-s`: Save file
-   `C-h k`: find the meaning of a key
-   `C-h v`: find the meaning of a variable
-   `C-h f`: find the meaning of a function. By default, it is the function that the current cursor points to.
-   `q`: quit buffer (for example, quit the help buffer opened just now.)
-   `C-x C-e`: Execute elisp functions


### Navigation keys

-   `C-f`: next char
-   `C-b`: previous char
-   `C-n`: next line
-   `C-p`: previous line
-   `M-v`: previous screen (page)
-   `C-v`: next screen (page)
-   =M-=b: move backward by word
-   `M-f`: move forward by word
-   `C-m`: add a new blank line

TO Read: <https://learnxinyminutes.com/docs/elisp/> and the official tutorial


## Functions

-   `(interactive)`: make the function available to M-x, but remember first `C-x C-e` the function.
-   `(global-set-key (kbd "<the-key-to-bind>") 'function-name)`: bind a global key to execute the function.


# itialization

-   Things will disappear once we exit Emacs. So we need to save it first
-   Save everything that need to run to `C:\Users\yout-user-name\AppData\Roaming\.emacs.d\init.el`


## Miscellaneous initialization configurations

-   `(tool-bar-mode -1)`: hide tool bar.
-   `(scroll-bar-mode -1)`: turn off scroll bar.
-   `(global-inum-mode t)`: show line number.
-   `(electric-indent-mode -1)`: deal with the indent (optional).
-   `(setq inhibit-splash-screen t)`: do not open the welcome page each time we open Emacs.
-   `(setq-default cursor-type 'bar)`: Change cursor.


## About modes

-   Major mode: the [] at the bottom. There is only one Major mode for each file.
-   Minor mode: tool-bar-mode is minor mode. No minor bar limit for the file.


## Package management

-   Options -> Manage Emacs Packages.
-   `C-h m`: show all the minor mode.


## company mode

-   Means "Complete anything", not literally "company".
-   Install it in the package management
-   `M-x company-mode`: Enable the company mode
-   `(global-company-mode t)`: enable it with emacs-lisp code


## Introduction to Org-mode

-   GTD (get things done)
-   Tab key to toggle lists.
-   `M-x org-mode`
-   `C-c C-t` to toggle TODO DONE None at list item.
