---
layout: post
title: Spacemacs Rocks Note Day 2
description: A series of notes that I learn Emacs hacking. Change variable globally, disabling auto-save and auto-backup; `require` keyword, enabling recent files opening, enabling delete selection mode; code block and example block fast typing; initializing Emacs with full screen; showing matching parenthesis, highlighting current line; package management system configuration; adding a new theme, hundgry delete mode, swiper, smartparens; customize-group; ordered list in org-mode; JavaScript IDE in Emacs; setting schedule in org-mode.
permalink: /spacemacs-study-note-2/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-10-23 22:34:56
---


# `setq` vs. `setq-default`

-   Cursor type is a `buffer-local` variable. setq will change a local buffer cursor type.
-   Use `setq-default` to change global setting.


# Disable auto-save / auto-backup

-   `(setq make-backup-files nil)`


# Require

-   There are files in the system, use this function to load them, similarly to include or import.
-   `(require 'org)`


# Deal with the recent files

-   `(require 'recentf)`: activate it.
-   `(recentf-mode 1)`
-   `(setq recentf-max-menu-items 25)`
-   `(global-set-key "\C-x\ \C-r" 'recentf-open-files)`: such that we can open recent file by `C-x C-r`.


# Delete the selection words

-   `(delete-selection-mode t)`: select some block and type sth, it will change. The previous version do this by append.


# shortkey for entering SRC block

-   `<s and <tab>`
-   Example block: `<e <tab>`


# start Emacs with full screen

-   `(setq initial-frame-alist (quote ((fullscreen . maximized))))`


# Show matched Parenthesis

-   `(add-hook 'emacs-lisp-mode-hook 'show-paren-mode)`


# Highlight the current line

-   `(global-hl-line-mode t)`


# Configurate the Package Management system

-   MELPA: <https://melpa.org/#/>
-   Note: number of download is not neccessarily means it is useful.
-   Use the following command to add the package:

```emacs-lisp
;; Add the package source
(when (>= emacs-major-version 24)
  (require 'package)
  (package-initialize)
  (add-to-list 'package-archives '("melpa" . "http://melpa.org/packages/") t)
  )

(require 'cl)
;; Add whatever packages you want here
(defvar LanternD/packages '(
			    company
			    monokai-theme
			    ) "Default packages")

(defun LanternD/packages-installed-p ()
  (loop for pkg in LanternD/packages
	when(not (package-installed-p pkg)) do (return nil)
	finally (return t)))

(unless (LanternD/packages-installed-p)
  (message "%s" "Refreshing package database...")
  (package-refresh-contents)
  (dolist (pkg LanternD/packages))
  (when (not (package-installed-p pkg))
    (package-install pkg))
  )
```

-   If the above is not working, go to Melpa's home page to find instruction.

```emacs-lisp
(require 'package) ;; You might already have this line
(let* ((no-ssl (and (memq system-type '(windows-nt ms-dos))
		    (not (gnutls-available-p))))
       (url (concat (if no-ssl "http" "https") "://melpa.org/packages/")))
  (add-to-list 'package-archives (cons "melpa" url) t))
(when (< emacs-major-version 24)
  ;; For important compatibility libraries like cl-lib
  (add-to-list 'package-archives '("gnu" . "http://elpa.gnu.org/packages/")))
(package-initialize) ;; You might already have this line
```

-   We can now add package from the Package management system.


# Add a new theme

-   Go to Package Management, install "monokai-theme"
-   `M-x load <enter> monokai <enter>`, done.


# Install hungry-delete-mode

-   Delete similar stuff all at once!


# Package management advanced

-   `M-x package-list-packages <enter>`: this is equivalent to open the package management system in the menu.
-   Press `<i>`, `<d>`, `<u>` to mark "Install", "Delete" and "Upgrade" to the packages.
-   After marking a package, press `<x>` to confirm.
-   `<U>`: captical `U` to execute global upgrade to all installed packages.
-   If too many packages are installed, be CAUTIOUS to upgrade all packages at once. Something terrible may happen.
-   `M-x package-autoremove`: Auto remove packages.


## About smex package

-   An augmented `M-x`.
-   after key-binding, press `M-x`, use `C-s` to navigate in the command available.


## About swiper package

-   type in the stuff
-   Use `C-n`, `C-p` to navigate
-   `C-x C-f` now can navigate like a folder access.


## About smartparens package

-   Help you type in the right parenthensis after you enter the left one.
-   Remember to add hook to certain major mode.


# Customize group

-   `M-x customize-group`, then type in the name, then we can enter the configuration for each package.
-   `M-x customize-option`: a more detailed option list.


# Tips on order list in `org-mode`

-   `M-<return>` can help to reorder the list, so that the numbers are current.

    ()
    1. ss
    2. r234
    3. 553233
    4. 443saf
    5. asdjio

Be careful, `M-<return>` will match the previous format.


# About JavaScript IDE

-   By default, Emacs open js with the JavaScript major mode.
-   Suppose we already have `js2-mode` installed, we can switch to that.
-   Install `js2-mode` for the IDE.

```emacs-lisp
(setq auto-mode-alist
  (append
    '(("\\.js\\'" . js2-mode))
      auto-mode-alist))
```

-   Install `nodejs-repl`, which is for executing the `.js` file. (require `node.js` installed in the system).
-   `M-x nodejs-repl-send-buffer`: execute this command in the `.js` file. Then the file will be executed in the frame.


# TODO Reading recommendation

-   `M-x Info`: open Info.
-   `C-h i`: same as above.
-   Read "Emacs Lisp Intro" ("Introduction to Emacs Lisp Programming"), especially the section of loop and recursion.


# Use org to set schedule

-   Create a "`gtd.org`" file

```emacs-lisp
(setq org-agenda-files '("~/org"))
(global-set-key (kbd "C-c a") 'org-agenda)
```

-   Bind a key to open the `.org` file.
-   `C-c C-s`: set a scheduled time.
-   `C-c C-d`: set the deadline time.
