---
layout: post
title: Spacemacs Rocks Note Day 6
description: A series of notes that I learn Emacs hacking. Org-capture, org-pomodoro; file encoding with utf-8; batch rename files in dired mode, seach and replace with helm-ag; flycheck; snippets auto complete.
permalink: /spacemacs-study-note-6/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-11-01 22:34:56
---


# 　


## Use org-capture to take notes

-   A module in org-mode. We can customize the template to make it easier to use.
-   Configuration of the template.

```emacs-lisp
(setq org-capture-templates
      '(("t" "Todo" entry (file+headline "D:/Dropbox/AGDA/Orz.org" "Agenda")
	 "* TODO [#B] %?\n %i\n"
	 :empty-line 1)))
```

-   Use `C-c C-s` to add timestamp to the TODO item. Enter a time to schedule.
-   Use `C-a a` to view the scheduled TODO list. Remember to set the location value of the `org-agenda-files`.

```emacs-lisp
(setq org-agenda-files '("D:/Dropbox/AGDA"))
```

-   `org-pomodoro`: A package to track the time. Pomodoro Technique.
-   `M-x org-pomodoro`: Execute this command to start 25-min clock counter.


## Miscellaneous optimization

-   Change the default buffer encoding. So that in case we type some Chinese characters, the coding of the buffer will becomes "UTF-8". And we don't need to bother again typing the encoding when we save that file.

```emacs-lisp
(set-language-environment "UTF-8")
```

-   Insert current url of the first activate tab in Chrome (This is only achieved in Mac in the video). Try to implement that in Windows.
-   Use `C-n` and `C-p` instead of `M-n`, `M-p` to select the candidates in company-mode:

```emacs-lisp
(with-eval-after-load 'company
  (define-key company-active-map (kbd "M-n") nil)
  (define-key company-active-map (kbd "M-p") nil)
  (define-key company-active-map (kbd "C-n") #'company-select-next)
  (define-key company-active-map (kbd "C-p") #'company-select-previous))
```


## Batch rename files in dired mode

-   Use `C-x C-q` in dired mode. The major mode becomes `Editable Dired`.
-   Use `expand-region` and `iedit` to batch change files.
-   Use `C-;` to enter iedit mode. And then we can change the filename all together.
-   Use `C-c C-c` to save the buffer to confirm the changes.


## Search and replace (Important)

-   Use `helm-ag`: install `ag` first

```sh
brew install the_silver_searcher
apt-get install silversearcher-ag
```

-   Search speed: `ag` > `pt` > `ack` > `grep`
-   Not quite convenient on Windows.
-   Why not using `helm` in Emacs? `helm` loads slower than `ivy`. However, `helm-ag` is an exception.
-   `M-x helm-do-ag-project-root`: find the occurence of certain keyword in the projoct directory.
-   We can bind a key to it. (`C-c p s`).
-   type `!` to eliminate the undesired results.
-   In the result buffer, press `C-c C-e` enter editing mode.
-   Use similar things in previous section (Batch rename) to change everything at once!


## Use flycheck to highlight typos

-   `eslint` for JavaScript.
-   Install `flycheck` package.
-   enable it globally: `(global-flycheck-mode)`
-   Use `M-x flycheck-verify-setup` to show the candidate flychecker module available.
-   Add more module to support more programming language.
-   Option: Add hook to enable it only in programming mode instead of global mode.


## About snippets.


### yasnippet package

-   Called `yasnippets`.
-   It can help us to enter some commonly used code snippets, such as `for`, `while`, `if-else`.
-   For more details, find the `YASnippets` menu on the top in programming mode.


### auto-yasnippet package

-   Use `~` to make the template. At that line, call `aya-create`.
-   At the new line, call `aya-expand`, then we create a template that has multiple cursors marked at the previous `~` point. Type in the stuff you want and create a new sentence.
