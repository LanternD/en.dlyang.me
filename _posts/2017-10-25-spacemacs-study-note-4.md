---
layout: post
title: Spacemacs Rocks Note Day 4
description: A series of notes that I learn Emacs hacking. Package loading mechanism, auto-indentation, hippie-expand, dired-mode, basic about org-mode.
permalink: /spacemacs-study-note-4/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-10-25 22:34:56
---


# Spacemacs Rocks Note Day 4


## More about `require` and `load-file`

-   More accurate exaplaination: If require can not find a feature, Emacs will load that file.
-   Priority: `require` ->= `load` ->= `load-file`.
-   Load first time: compile and load the `.el` file; load second time, it will load the corresponding `.elc` file.
-   If there is no "load-path" variable, we must specify whether `.el` or `.elc` to be loaded (absolute path).
-   `byte-compile-file`: generate `.elc` from `.el`.
-   `.elc` can be executed fasted than `.el`.
-   After executing (provide), the file will be added to feature-list.
-   autoload: kind of complicated. Find something on the web if interested.


## Indent

-   `C-M-\`: auto indent. This method require file selection.
-   Use another function snippet to help us to do the indent job.

```emacs-lisp
(defun indent-whole-buffer()
  (interactive)
  (indent-region (point-min) (point-max))
  )

(defun indent-region-or-buffer()
  (interactive)
  (save-excursion 
    (if (region-active-p)
    (progn
      (indent-region (region-begin) (region-end))
      (message "Selected region is indented.")
     )
      (progn 
	(indent-whole-buffer)
	(message "The whole buffer is indented.")
       )
      )
    )
  )

(global-set-key (kbd "C-M-\\") 'indent-region-or-buffer)
```


## More about auto-complete - hippie-expand

-   `company-mode` somethimes doesn't work.
    -   For example, type a path without quote mark: `~/.emacs`.
    -   "`~/.emacs.d/lisp/custom.el`".
-   use `hippie-expand` to deal with these cases.
-   Use the following snippet to augment the auto-complete function:

```emacs-lisp
;; set the list for hippie-expand
(setq hippie-expand-try-functions-list '(try-expand-dabbrev
					 try-expand-dabbrev-all-buffers
					 try-expand-dabbrev-from-kill
					 try-complete-file-name-partially
					 try-complete-file-name
					 try-expand-all-abbrevs
					 try-expand-list
					 try-expand-line
					 try-complete-lisp-symbol-partially
					 try-complete-list-symbol))
(global-set-key (kbd "M-/") 'hippie-expand) ;; this is the default key set
```


## About `dired-mode`

-   Short for "directory edit"
-   key `<+>`: create a folder.
-   Then `C-x C-f` create new file.
-   `<g>`: to refresh the Dired buffer.
-   `<C>`: capital C to copy folder or file.
-   `<D>`: capital D to delete a file or folder.
-   `<d>`: mark the file to delete status.
-   `<u>`: unmark current file status (delete or sth else).
-   `<x>`: execute the marker.
-   `<R>`: rename a file or directory
-   Use the following key to limit the dired buffers to only one.

```emacs-lisp
;; (require 'dired)
(with-eval-after-load 'dired)
(put 'dired-find-alternate-file 'disabled nil)
(define-key dired-mode-map (kbd "RET") 'dired-find-alternate-file)
```

-   `with-eval-after-load`: load something after everything is loaded, which improves the loading speed of Emacs.
-   `C-x C-j`: open the directory of the current editting file `(require 'dired-x)`.
-   `(setq dired-dwim-target t)`: optimize the copy destination dir path.


## Save-excursion

-   Save the position of the current cursor.


## Use org-mode to organize the initialization files

-   Use the following snippet:

```emacs-lisp
(require 'org-install)
(require 'ob-tangle)
(org-babel-load-file (expand-file-name "lanternd_int.org" user-emacs-directory))
```

-   It will generate an `.el` file, which is equivalent to the `init-xxx.el`.
