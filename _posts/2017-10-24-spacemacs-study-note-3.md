---
layout: post
title: Spacemacs Rocks Note Day 3
description: A series of notes that I learn Emacs hacking. Splitting the `init.el` file, enabling auto revert mode, package loading mechanism overview, enable abbreivation mode, about popwin package, more about major and minor mode in Eamcs, function and variable naming convention, counsel-git to find files.
permalink: /spacemacs-study-note-3/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-10-24 22:34:56
---


# Split the `init.el` configuration into multiple files


## Use git to keep track of your `.emacs.d`

-   `git init`
-   `git add .`
-   `git commit -m "initial commit"`
-   Or do it with Github (my choice).
-   We can also use git to backup `./elpa`, in case bug occurs after upgrading a package.
-   Use `git throw` (a self-defined command) to discard anything that is not committed.


## Auto-revert-mode

-   Auto load a file from disk once it is revised by external command.
-   `M-x auto-revert-mode`


## Package loading mechanism

-   `load-file`
-   `load`
-   `require`
-   `autoload`
-   The differences can be found on the web
-   `C-h v features`: view all the features available.


## The real topic of this part

-   Recommended organization of configuration files.
    -   `init-packages.el`: deal with the 3rd party packages, loading and configurations.
    -   `init-ui.el`: how Emacs looks like.
    -   `init-better-defaults.el`: improvement of built-in settings.
    -   `init-keybindings.el`
    -   `custom.el`: save customize-group.
-   Such that we can view and edit things faster.
-   Remember to add `(provide 'xx)` and `(require 'xx)`.
-   Remember to add the configuration file directory to `load-path` variable.
-   For the `custom.el`, we have to all one line code to set the customize group.


# Abbrevation mode

-   Help to type things fast!
-   Code

```emacs-lisp
(abbrev-mode t)
(define-abbrev-table 'global-abbrev-table '(
					    ("ltd" "LanternD")
					    ))
```

-   Recommand: use '8' as the start of the abbrev, prevent typo accidentally.
-   `<space>` or `<enter>` to complete the word.
-   For key binding, `C-c` is for customize key, while `C-x` is for built-in keys.


# Popwin package

-   It helps to move the cursor to the new opened window, such as function manual.
-   Configuration:

```emacs-lisp
(require 'popwin)
(popwin-mode t)
```


# More about major and minor mode


## `require` and `load-file`

-   Some package just use `(global-xx-mode 1)`, while some use `require` and `(xx-mode t)`.
-   The difference is `autoload` marco. it needs `xx-autoloads.el`.
-   It works with `(package-initialize)` function.
-   "Require" will load a file indirectly, we can do it by calling load-file function.


## Naming conventions

-   `LanternD/xxx` as personal variable or function names.
-   Mode naming: everything (variable and function) in the mode should starts with the name of the mode.
-   e.g. `happy-mode`, `happy-init`, `happy-status`.
-   Naming of features: `xxx-mode-key-map`, `xxx-mode-hook`.
-   We can use prog-mode-hook to turn on line number only for programing mode.


## 3 types of major mode

-   `text-mode`
-   `special-mode`
-   `prog-mode`


# Set key for counsel-git

-   counsel-git can find a file very fast in a git managed directory.
-   Add key binding to it.

```emacs-lisp
(global-set-key (kbd "C-c p f") 'counsel-git)
```
