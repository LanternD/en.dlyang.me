---
layout: post
title: Spacemacs Rocks Note Day 7
description: A series of notes that I learn Emacs hacking. Introduction to evil-mode, packages to augment evil, such as evil-leader, eveil-surrond, evil-nerd-commenter, powerline-evil; misc. improvement, such as window-numbering, which-key and powerline packages.
permalink: /spacemacs-study-note-7/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-11-06 22:34:56
---


# 　


## Use Evil to enable `vim` editing

-   aka "Extensible vi layer for Emacs".
-   `package-install evil-mode`
-   In the `init-packages.el`, add the configuration below

```emacs-lisp
(evil-mode 1)
(setcdr evil-insert-state-map nil)
(define-key evil-insert-state-map [escape] 'evil-normal-state)
```

-   Some difference between `vim` and `evil-mode`

`C-d` to page down, but `C-u` does not page up. Because `C-u` is used as "Universal args" in Emacs. We can change this in `customize-group`

-   PDF manual for user switching from vim to Emacs. [Evil.pdf](https://github.com/emacs-evil/evil/blob/master/doc/evil.pdf).
-   Evil state = Emacs mode
    -   evil normal state
    -   evail insert state
    -   evil visual state
    -   evil motion state
    -   evil emacs state
    -   evil operator state (diw)

We want to set the evil state when we enter certain mode, use the following code

```emacs-lisp
(dolist (mode '(ag-mode
		flycheck-error-list-mode
		occur-mode
		git-rebase-mode
		))
  (add-to-list 'evil-emacs-state-mode mode))
```

-   Enable key binding in certain mode

```emacs-lisp
(add-hook 'occur-mode-hook (lambda ()
			     (evil-add-hjkl-bindings occur-mode-map 'emacs
			      (kbd "/") 'evil-search-forward
			      (kbd "n") 'evil-search-next
			      (kbd "N") 'evil-search-previous
			      (kbd "C-d") 'evil-scroll-down
			      (kbd "C-u") 'evil-scroll-up
			      )))

```

-   Add more plugins to customize `evil`.
    -   `evil-leader`. `(global-evil-leader-mode)` Helps to add short key to evil normal state. Add as much key bindings as you like.
        
        ```emacs-lisp
        (evil-leader/set-keyword
         "ff" 'find-file
         "fr" 'recentf-open-files
         "bs" 'switch-to-buffer
         "bk" 'kill-buffer
         "pf" 'counsel-git
         "ps" 'helm-do-ag-project-root
         "0" 'select-window-0
         "1" 'select-window-1
         "2" 'select-window-2
         "3" 'select-window-3
         "w/" 'split-window-right
         "w-" 'split-window-below
         "wo" 'delete-other-windows
         ":" 'counsel-M-x
         )
        ```
    -   `evil-surround` package. When you select a word and type something, the word will be surrounded by that.
    -   `evil-nerd-commenter` package. We can add comment or remove the comment of current section. Add toggle comment line to visual state and normal state:

```emacs-lisp
(define-key evil-normal-state-map (kbd ",/") 'evilnc-comment-or-uncomment-lines)
(define-key evil-visual-state-map (kbd ",/") 'evilnc-comment-or-uncomment-lines)
```

-   `powerline-evil` package. A powerline minor mode for the evil mode. Try to add window number to the powerline, but failed. In the video, window numbering is finally enabled without loading the powerline.


## Miscellaneous improvement


### Use `C-w` to delete a word backward

```emacs-lisp
(global-set-key (kbd "C-w") 'backward-kill-word)
```


### `window-numbering` package

-   `package-install window-numbering`
-   `(window-numbering-mode 1)`


### `powerline` package

-   Polish the mode line, make it special and beautiful.
-   `(require 'powerline)`
-   `(powerline-default-theme)`


### `which-key` package

-   Installation:

```emacs-lisp
(require which-key)
(which-key-mode 1)
```

-   Set popup window properties

```emacs-lisp
(setq which-key-side-window-max-height 0.25)
(setq which-key-side-window-location 'right)
```


### Search in org agenda

-   `C-a` enter agenda mode.
-   `s` to search.
-   Read the key in list for details.
