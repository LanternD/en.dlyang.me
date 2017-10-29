---
layout: post
title: Spacemacs Rocks Note Day 5
description: A series of notes that I learn Emacs hacking. Parenthesis highlighting, web-mode for web development, js2-refactor, occur-mode, imenu-mode, expand-region, iedit-mode, org-mode export.
permalink: /spacemacs-study-note-5/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-10-27 22:34:56
---


# Highlight parenthesis within the bracket

-   Code snippet:

```emacs-lisp
;; Highlight the enclosing parenthensis while the cursor is inside it.
(define-advice show-paren-function (:around (fn) fix-show-paren-functioon)
  (cond ((looking-at-p "\\s(") (funcall fn))
	(t (save-excursion
	     (ignore-errors (backward-up-list))
	     (funcall fn)))))
```

-   Note: define-advice can extend the scope of a function.
-   `backward-up-list`: looking backward to the first left parenthesis. if exists, call function.
-   `cond`: condition, similar to switch-case.


# Towards web development


## DOS EOL processing

-   DOS line break exists in some web pages, they appear as `^M` in Unix OS. We need to eliminate them first.
-   Option 1, hide them:

```emacs-lisp
(defun hidden-dos-eol()
  (interactive)
  (setq buffer-display-table (make-display-table))
  (aset buffer-display-table ?\^M []))
```

-   Option 2, remove(replace) them:

```emacs-lisp
;; Option 2: remove ^M
(defun remove-dos-eol()
  (interactive)
  (goto-char (point-min))
  (while (serach-forward "\r" nil t) (replace-match "")))
```

-   This is an example showing how to scan the whole document and make some changes.


## Deal with the toggle of the web-mode

```emacs-lisp
;; Configuration for web-mode
;; set the indent to 2 by default.
(defun my-web-mode-indent-setup ()
  (setq web-mode-markup-indent-offset 2) ; html
  (setq web-mode-css-indent-offset 2) ; css
  (setq web-mode-code-indent-offset 2)) ; js

(add-hook 'web-mode-hook 'my-web-mode-indent-setup)
;; toggle between 2 indent and 4 indent
(defun my-toggle-web-indent ()
  (interactive)
  (if (or (eq major-mode 'js-mode) (eq major-mode 'js2-mode))
      (progn
	(setq js-indent-level (if (= js-indent-level 2) 4 2))
	(setq js2-basic-offset (if (= js2-basic-offset 2) 4 2))))
  (if (eq major-mode 'web-mode)
      (progn
	(setq web-mode-markup-indent-offset (if (= web-mode-markup-indent-offset 2) 4 2))
	(setq web-mode-css-indent-offset (if (= web-mode-css-indent-offset 2) 4 2))
	(setq web-mode-code-indent-offset (if (= web-mode-code-indent-offset 2) 4 2))))
  (if (eq major-mode 'css-mode)
      (setq css-indent-offset (if (= css-indent-offset 2) 4 2)))
  (setq indent-tabs-mode nil))

(global-set-key (kbd "C-c t i") 'my-toggle-web-indent)
```


## Use js2-refactor to increase the development efficiency

-   `package-install <ret> js2-refactor`

```emacs-lisp
(add-hook 'js2-mode-hook #'js2-refactro-mode)
(js2r-add-keybindings-with-prefix "C-c C-m")
```

-   `C-c C-m`: activate the js2-refactor.
-   `ef`: extract function.
-   `em`: extract &#x2013;method.
-   `sl`: forward-slurp (put a line of code into loop or sth).
-   `ba`: opposite of the above one.
-   Read the doc for more detail! It is useful.


# Improve some built-in modes


## Occur-mode

-   Find a word with regular expression.
-   `M-s o`: enter a regexp to find in in the buffer. Similar to search using swiper. But occur can do both forward and backward serach.
-   Use the `=customize-variable=` to move the popout window to the right hand side.
-   In the `*occur*` buffer, we can edit it by `M-x occur-edit-mode`.
-   Improve the `occur-mode`, change the default value to the word that the cursor currently pointing to.

```emacs-lisp
(defun occur-dwim ()
  (interactive)
  (push (if (region-active-p)
	    (buffer-substring-no-properties
	     (region-beginning)
	     (region-end))
	  (let ((sym (thing-at-point 'symbol)))
	    (when (stringp sym)
(regexp-quote sym))))
	regexp-history)
  (call-interactively 'occur))
(global-set-key (kbd "M-s o") 'occur-dwim)
```

-   In the occur-mode window, press `e` can also enter occur-edit mode.


## imenu-mode

-   show all the functions in the current buffer.
-   However the default one is not convenient, use `counsel-imenu` instead.
-   Bind a key `M-s i` to it. Use regular expression to improve it.


# Expand-region and iedit-mode (Pretty useful)


## expand-region

-   `(requre 'expand-region)`
-   `(global-set-key (kbd "c-=") 'er/expand-region)`
-   Repeatly use `C-=` or `C--` to change the scope of selection.


## iedit-mode

-   multiple selection and edit them simutaneously.
-   `M-x iedit-mode <ret>`
-   Bind a key to it. (`C-;`)
-   change the iedit occurence from "highlight" to "region".


# Export in Org-mode

-   `C-c C-e`: pop up window to choose the output selection.
