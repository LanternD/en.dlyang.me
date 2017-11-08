---
layout: post
title: Spacemacs Rocks Note Day 10
permalink: /spacemacs-study-note-10/
categories: [blog]
tags: [spacemacs, emacs, lecture, note, hacking]
date: 2017-11-08 12:34:56
---


# 　


## More on `cask` and `use-package`


### `cask`

-   After you upgrade a package, there is chance that some latest version has bugs or incompitible. In this scenario, we can set the version we want in `.cask` file,

```emacs-lisp
(depends-on "monokai-theme" :git "https://github.com/xxx/yyy" :ref "178dfc9")
```

Then we can install that stable version to avoid bugs.

-   With `cask` we can avoid latency in the bug fixing. (MELPA refresh every 3 or 4 hours.)


### `use-package`

-   `:ensure t` key word in `use-package`: if a pacage does not exist in the `elpa`, `use-package` will download it for you. After that the configuration will be executed.
-   `:pin melpa-stable`: we can change it to `gnu` or `melpa`, so that it will download from certain source. Remember to add the source in your `use-package` config file.


## `company-mode` advanced auto-completion


### Backend

-   `company-mode` has multiple backends. They supports different workspaces by preparing different completion candidates.
-   `C-h v company-backends` for detail. It is a list, showing the available backends. The program starts from the first one and traverse all of them to find the match one. Then the candidates are found by the `company-mode`. For example, we type `/`, `company-files` backend is activated.
-   For another example, when we type `stude` and we forget how to spell the rest, we can use `M-x company-ispell` to list all candidates from the system dictionary.
-   `customize-group company-dabbrev`: we can choose which buffer the `company-mode` will "watch".
-   `company-mode` also has frontend. We can customize it as well, however we don't have to do so. Let it as default.
-   `C-f C-v` to check how the backend is implemented.

-   Situation where `company-mode` not working quite well.
    -   `company-anaconda` mode for python has issue on Mac. (Not going to take notes here)
-   There are two types of auto-completion implementation in `company-mode`. One is finding the candidates from local algorithm or database. The other one is server-client architecture. `anaconda-mode` connects with server, where the candidates are fetched from. The server is in `localhost` btw, not on the internet.
-   Other examples are: `company-jedi` (for python), `company-ycmd` (for C++), `company-tern` (for JavaScript), .etc.
-   You need to make sure the **server side** works properly in the first place, then you may want to check whether you use the correct backend.
-   If we have multiple backends, `company` get confused. Use `M-x company-xxx` or use hook to make sure the correct backend is enabled.

```emacs-lisp
(add-hook 'python-mode-hook 
	  (lambda ()
	    (setq (make-local-variable 'company-backends) '(company-anaconda company-dabbrev))))
```


### Group backend

-   For example, `company-dabbrev-code` only complete in code, and not in comments etc. We can group a bunch of backends together. See example below

```emacs-lisp
(add-hook 'python-mode-hook 
	  (lambda ()
	    (setq (make-local-variable 'company-backends) '((company-anaconda company-dabbrev-code) company-dabbrev))))
```

-   There are two backends in the setting, the first one is a group backend, the second one is a single backend. We can make it for our best use.
-   Once the first item in the company backend group, the "single" backend after the backend group will not be enabled.

-   How to write your own backend. Check the following blog:

[Writing the Simplest Emacs company-mode Backend - Sixty-north](http://sixty-north.com/blog/writing-the-simplest-emacs-company-mode-backend.html)


### Sort candidates by statistics

Address this next time.
