---
layout: post
title: Spacemacs Rocks Note Day 8 & 9
description: A series of notes that I learn Emacs hacking. Cask and pallet package for multi-version Emacs collaboration; Macro in emacs-lisp; use-package package introduction.
permalink: /spacemacs-study-note-8-9/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-11-07 22:34:56
---

Prologue: Not too much for day 8. Previous video is 1 hour's long, the author decrease the length of each video to 30 min for better performance. Therefore I put the content in two days' video into single post.


# Day 8

There are not too many in this video.


## Visit Melpa from China

-   [Elpa China Mirror](https://elpa.emacs-china.org)


## `cask`, a package for project monitoring

-   Clone from the Github repo, and install. Find more from the official site.
-   If we have multiple Emacs installed, we can employ `cask` to make them work simutaneously.
-   If there is only one Emacs on the compter, there you are good to go.


## `pallet` package

-   A package management system based on `cask`.
-   `M-x pallet-init`. A `cask` file will be generated in the `.emacs.d` folder.
-   `(cask-initialize)`: a similar code snippet as `(package-initialize)`
-   Will help to synchronize packages between different version of Emcas.
-   Add the following code before any of the package are required.

```emacs-lisp
(require 'cask "~/.cask/cask.el")
(cask-initialize)
(require 'pallet)
(pallet-mode t)
```

-   `cask install` in the terminal to merge the package directory.

-   Now we can get rid of the previous package initialization code.


## `mwe-log-command` package

-   `M-x mwe:open-command-log-buffer`
-   Now we can have an idea on what key is pressed in history.

---


# Day 9


## Macro

-   We can consider it as "code that generates code".
-   Analog as macro in C or template in C++.
-   See an example below

```emacs-lisp
(defmacro inc (var)
  (list 'setq var (list '1+ var)))
```

-   Usage of the example

```emacs-lisp
(setq my-var 1)
(inc my-var)
(macroexpand '(inc my-var))
```

-   Write macro is similar as writing function in elisp.
-   However, to achieve similar result we can use `defun`, why bother? What's the difference between function and macro?
    -   Evaluation: the macro arguments are the actual expressions appearing in the macro call. For functions, the value in the argument is first fetched or calculated then the function is executed. For macro, the expression is first expanded and then executed.
    -   Expansion: the value returned by the macro body is an alternate Lisp expresion, aka the expansion of the macro.

-   Backquote matters. Emacs will automatically insert two backquotes all together. Use the following code to disable it.

```emacs-lisp
(sp-local-pair 'emacs-lisp-mode "`" nil :actions nil)
```

-   Backquote `` ` `` works with `,`. It means we do not execute the program after the quote. However, the expression (program) after `,` will be execute first, and then pass as argument.

-   Use `pp` to pretty print your `macroexpand`.
-   Take a look at another example

```emacs-lisp
(defun my-print (number)
  (message "%d" number))
(my-print 2)

(my-print (+ 2 3))

(defmacro my-print-2 (number)
`(message "%d" ,number))
(my-print-2 2)
(my-print-2 (+ 2 3))

(defmacro inc (var)
(list 'setq var (list '1+ var)))

(setq my-var-2)
(inc my-var)

(defmacro inc2 (var1 var2 )
(list 'progn (list 'inc var1) (list 'inc var2)))
(macroexpand '(inc2 my-var my-var)) ;; this will expand only one layer.
(macroexpand-all '(inc2 my-var my-var))
```


## `use-package` package

-   All the stuff can be found on its official page.
-   `(use-package xxx)`: a better solution to substitute `(require 'xxx)`. If the 'xxx' is not in `elpa`, we will encounter an error if we use `require`. However, `use-package` can help you load packages safer.
-   We can merge similar configuration together by using `:init` and `:config`. The difference is that, `:init` will be executed before requiring the package, while `:config` will be executed after loading the pacakge, when we can add more configuration to the package.

```emacs-lisp
(use-package xxx
  :init 
  (progn
    (setq var1 1)
    (setq var2 "s"))
  :config 
  (setq var3 5))			
```

-   `require` will load everything, which is too slow. We can use `autoload` instead. Now we can integrate `autoload` into `use-package`. Use `:command` to do so. `:defer` is equal to `eval-after-load`.

```emacs-lisp
(use-package xxx
  :commands
  (global-company-mode)
  :defer t
```

-   Key binding:

```emacs-lisp
(use-package color-moccur
  :commands (isearch-moccur iseach-all)
  :bind (("M-s O" . moccur)
	 :map isearch-mode-map
	 ("M-o" . isearch-moccur)
	 ("M-O" . isearch-moccur-all))
  :init 
  (setq isearch-lazy-highlight t)
  :config 
  (use-package moccur-edit)
  )
```

-   In a word, it makes your code neat and robust.
-   Spacemacs use `use-package` frequenctly.
