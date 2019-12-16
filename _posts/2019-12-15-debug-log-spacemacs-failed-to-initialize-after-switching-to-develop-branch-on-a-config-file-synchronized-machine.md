---
layout: post
title: ~[DEBUG LOG] Spacemacs Failed to Initialize After Switching to develop Branch on a Config File Synchronized Machine
description: I know the title is long. But I don't know how to describe my problem clearly. So just read the post. I'm sure generally you find this post by Google, so the title won't bother you.
permalink: /debug-log-spacemacs-failed-to-initialize-after-switching-to-develop-branch-on-a-config-file-synchronized-machine/
categories: [blog]
tags: [spacemacs, emacs, debug, config]
date: 2019-12-15 00:48:25
---

# Situation

I have two machines, one Ubuntu desktop and a MacBook Pro laptop. On my Linux machine, I switched to the `develop` branch of Spacemacs without any problem, about 2 months ago. Now I would like to checkout the branch on my MBP from `master` to `develop` as well. But this time I was with no luck.

# Bug Behavior

When I restarted Spacemacs after `git checkout develop` in my `~./emacs.d` folder, I got the following error:

> Warning (initialization): An error occurred while loading ‘/Users/my\_user\_name/.emacs.d/init.el’:
> 
> File is missing: Setting current directory, No such file or directory, ~/
> 
> To ensure normal operation, you should investigate and remove the cause of the error in your initialization file. Start Emacs with the ‘&#x2013;debug-init’ option to view a complete error backtrace.

(You may have come here after these sentence in Google :) )

The Spacemacs could not loaded properly, so it is just like a vanilla emacs. No packages are loaded, no modes are running.

I ran `emacs --debug-init` in terminal and I got the following messages:

```emacs-lisp```
Debugger entered--Lisp error: (file-missing "Setting current directory" "No such file or directory" "~/")
  call-process("zsh" nil t nil "-c" "/usr/local/bin/timeout --help")
  apply(call-process "zsh" nil t nil ("-c" "/usr/local/bin/timeout --help"))
  process-file("zsh" nil t nil "-c" "/usr/local/bin/timeout --help")
  shell-command-to-string("/usr/local/bin/timeout --help")
  (string-match-p "^ *-k" (shell-command-to-string (concat prog " --help")))
  (and prog (string-match-p "^ *-k" (shell-command-to-string (concat prog " --help"))))
  (if (and prog (string-match-p "^ *-k" (shell-command-to-string (concat prog " --help")))) (progn prog))
  (when (and prog (string-match-p "^ *-k" (shell-command-to-string (concat prog " --help")))) prog)
  (let ((prog (or (executable-find "timeout") (executable-find "gtimeout")))) (when (and prog (string-match-p "^ *-k" (shell-command-to-string (concat prog " --help")))) prog))
  eval((let ((prog (or (executable-find "timeout") (executable-find "gtimeout")))) (when (and prog (string-match-p "^ *-k" (shell-command-to-string (concat prog " --help")))) prog)))
  custom-initialize-reset(quelpa-build-timeout-executable (let ((prog (or (executable-find "timeout") (executable-find "gtimeout")))) (when (and prog (string-match-p "^ *-k" (shell-command-to-string (concat prog " --help")))) prog)))
  custom-declare-variable(quelpa-build-timeout-executable (let ((prog (or (executable-find "timeout") (executable-find "gtimeout")))) (when (and prog (string-match-p "^ *-k" (shell-command-to-string (concat prog " --help")))) prog)) "Path to a GNU coreutils \"timeout\" command if available.\nThis must be a version which supports the \"-k\" option." :type (file :must-match t))
  eval-buffer(#<buffer  *load*-71122> nil "/Users/my_user_name/.emacs.d/core/libs/quelpa.el" nil t)  ; Reading at buffer position 15106
  load-with-code-conversion("/Users/my_user_name/.emacs.d/core/libs/quelpa.el" "/Users/my_user_name/.emacs.d/core/libs/quelpa.el" nil t)
  require(quelpa)
  configuration-layer//configure-quelpa()
  (let ((display-buffer-alist (quote (("\\(\\*Compile-Log\\*\\)\\|\\(\\*Warnings\\*\\)" (display-buffer-in-side-window) (inhibit-same-window . t) (side . bottom) (window-height . 0.2)))))) (configuration-layer//configure-quelpa) (let* ((upkg-names (configuration-layer//get-uninstalled-packages packages)) (not-inst-count (length upkg-names)) installed-count) (if upkg-names (progn (spacemacs-buffer/set-mode-line "Installing packages..." t) (let ((delayed-warnings-backup delayed-warnings-list)) (spacemacs-buffer/append (format "Found %s new package(s) to install...\n" not-inst-count)) (configuration-layer/retrieve-package-archives) (setq installed-count 0) (spacemacs//redisplay) (let ((--dolist-tail-- upkg-names) pkg-name) (while --dolist-tail-- (setq pkg-name ...) (let ... ...) (setq --dolist-tail-- ...))) (let ((--dolist-tail-- upkg-names) pkg-name) (while --dolist-tail-- (setq pkg-name ...) (let ... ...) (setq --dolist-tail-- ...))) (spacemacs-buffer/append "\n") (if init-file-debug nil (setq delayed-warnings-list delayed-warnings-backup)))))))
  configuration-layer//install-packages((ac-ispell ace-link ace-window aggressive-indent anaconda-mode async auctex auctex-latexmk auto-compile auto-complete auto-dictionary auto-highlight-symbol auto-yasnippet avy bind-key bind-map blacken cc-mode ccls centered-cursor-mode clang-format clean-aindent-mode column-enforce-mode company company-anaconda company-auctex company-c-headers company-lsp company-reftex company-rtags company-statistics company-tern company-web company-ycmd counsel counsel-css counsel-projectile cpp-auto-include cquery css-mode csv-mode cython-mode dactyl-mode desktop devdocs diminish disaster doom-modeline dotenv-mode dumb-jump ...))
  (let ((packages (append (configuration-layer//filter-distant-packages configuration-layer--used-packages t (quote (not (oref pkg :lazy-install)))) (if (eq (quote all) dotspacemacs-install-packages) (progn (let (all-other-packages) (let ... ...) (configuration-layer//filter-distant-packages all-other-packages nil))))))) (configuration-layer//install-packages packages) (if (and (or (eq (quote used) dotspacemacs-install-packages) (eq (quote used-only) dotspacemacs-install-packages)) (not configuration-layer-force-distribution) (not configuration-layer-exclude-all-layers)) (progn (configuration-layer/delete-orphan-packages packages))))
  (progn (let ((packages (append (configuration-layer//filter-distant-packages configuration-layer--used-packages t (quote (not ...))) (if (eq (quote all) dotspacemacs-install-packages) (progn (let ... ... ...)))))) (configuration-layer//install-packages packages) (if (and (or (eq (quote used) dotspacemacs-install-packages) (eq (quote used-only) dotspacemacs-install-packages)) (not configuration-layer-force-distribution) (not configuration-layer-exclude-all-layers)) (progn (configuration-layer/delete-orphan-packages packages)))))
  (if spacemacs-sync-packages (progn (let ((packages (append (configuration-layer//filter-distant-packages configuration-layer--used-packages t (quote ...)) (if (eq ... dotspacemacs-install-packages) (progn ...))))) (configuration-layer//install-packages packages) (if (and (or (eq (quote used) dotspacemacs-install-packages) (eq (quote used-only) dotspacemacs-install-packages)) (not configuration-layer-force-distribution) (not configuration-layer-exclude-all-layers)) (progn (configuration-layer/delete-orphan-packages packages))))))
  configuration-layer//load()
  (cond (changed-since-last-dump-p (configuration-layer//load) (if (spacemacs/emacs-with-pdumper-set-p) (progn (configuration-layer/message "Layer list has changed since last dump.") (configuration-layer//dump-emacs)))) (spacemacs-force-dump (configuration-layer//load) (if (spacemacs/emacs-with-pdumper-set-p) (progn (configuration-layer/message (concat "--force-dump passed on the command line, " "forcing a redump.")) (configuration-layer//dump-emacs)))) ((spacemacs-is-dumping-p) (configuration-layer//load)) ((and (spacemacs/emacs-with-pdumper-set-p) (spacemacs-run-from-dump-p)) (configuration-layer/message "Running from a dumped file. Skipping the loading process!")) (t (configuration-layer//load) (if (spacemacs/emacs-with-pdumper-set-p) (progn (configuration-layer/message (concat "Layer list has not changed since last time. " "Skipping dumping process!"))))))
  configuration-layer/load()
  (let ((file-name-handler-alist nil)) (require (quote core-spacemacs)) (spacemacs/dump-restore-load-path) (configuration-layer/load-lock-file) (spacemacs/init) (configuration-layer/stable-elpa-init) (configuration-layer/load) (spacemacs-buffer/display-startup-note) (spacemacs/setup-startup-hook) (spacemacs/dump-eval-delayed-functions) (if (and dotspacemacs-enable-server (not (spacemacs-is-dumping-p))) (progn (require (quote server)) (if dotspacemacs-server-socket-dir (progn (setq server-socket-dir dotspacemacs-server-socket-dir))) (if (server-running-p) nil (message "Starting a server...") (server-start)))))
  (if (not (version<= spacemacs-emacs-min-version emacs-version)) (error (concat "Your version of Emacs (%s) is too old. " "Spacemacs requires Emacs version %s or above.") emacs-version spacemacs-emacs-min-version) (let ((file-name-handler-alist nil)) (require (quote core-spacemacs)) (spacemacs/dump-restore-load-path) (configuration-layer/load-lock-file) (spacemacs/init) (configuration-layer/stable-elpa-init) (configuration-layer/load) (spacemacs-buffer/display-startup-note) (spacemacs/setup-startup-hook) (spacemacs/dump-eval-delayed-functions) (if (and dotspacemacs-enable-server (not (spacemacs-is-dumping-p))) (progn (require (quote server)) (if dotspacemacs-server-socket-dir (progn (setq server-socket-dir dotspacemacs-server-socket-dir))) (if (server-running-p) nil (message "Starting a server...") (server-start))))))
  eval-buffer(#<buffer  *load*> nil "/Users/my_user_name/.emacs.d/init.el" nil t)  ; Reading at buffer position 1880
  load-with-code-conversion("/Users/my_user_name/.emacs.d/init.el" "/Users/my_user_name/.emacs.d/init.el" t t)
  load("/Users/my_user_name/.emacs.d/init" t t)
  #f(compiled-function () #<bytecode 0x400bd7e9>)()
  command-line()
  normal-top-level()
```

Pretty long, right? I didn't read through it.

I Googled the keywords for a while with no luck. People had similar error messages but the reasons were different from mine.

# Road on Debug

I started to debug. Here's what I found.

-   If I remove my original `.spacemacs.d` folder, the emacs starts to work. The version is '0.300.0@26.3'.
-   If I run `emacs -nw`, with my original `.spacemacs.d`, the emacs starts normally.
-   The problem occurs when I run emacs GUI, with my original `.spacemacs.d`.

# Reason

After one hour or so, I found the reason.

Spacemacs `develop` branch, which will be 0.300.0 in the future, introduces a new mechanism to import the environment variables from your shell, stored in a file called `.spacemacs.env`. (Otherwise you need a package called `exec-path-from-shell` for that.)

Since my MBP shares/synchronizes the Spacemacs configuration (the whole `.spacemacs.d` folder) with the Ubuntu desktop via the Dropbox, the Spacemacs on MBP `develop` branch found the `.spacemacs.env` file, which was generated by the Ubuntu machine.

However, you know, these two machines have significantly different set of environment variables. The env vars in `.spacemacs.env` crashed the MBP Spacemacs and it failed to load many of the important things from the disk. For example, the "`~`" is different. It is `/home/my_user_name` in Ubuntu, but is `/Users/my_user_name` in MBP. In other words, the MBP loads a wrong environment variable config file.

This problem only occurs for the GUI version Emacs. Because when you run it in terminal, the environment variables can be inherited directly from the shell. Only the GUI version needs special care.

I do have another Windows machine using Spacemacs, with `develop` branch without any problem. Because I synchronizes the configuration file only in one way (`git pull`). So the system will generate the `.spacemacs.env` for itself, without affecting other machines.

# Solution

The keypoint here is to isolate the `.env` file for different system. I have two solutions + another possible solution right now.

Spacemacs offers two location to put that file, one is "`~`", the other one is "`~/.spacemacs.d`". The only way to avoid conflicts is put `.spacemacs.env` in `~`. In other words, the file should not be synchronized with Dropbox across different machines.

## Solution 1: change the order of the directories to be discovered

If you take a look at `~/.emacs.d/core/core-env.el`, there is a variable `spacemacs-env-vars-file` defining the directory:

```emacs-lisp
(defvar spacemacs-env-vars-file
  (concat (or dotspacemacs-directory user-home-directory) ".spacemacs.env")
  "Absolute path to the env file where environment variables are set.")
```

You can see that it first tries to find it at `.spacemacs`, and then `~`. If this file is found in the previous one, it will just load it. So we can swap their order, to let it go for `~` first:

```emacs-lisp
(defvar spacemacs-env-vars-file
  (concat (or user-home-directory dotspacemacs-directory) ".spacemacs.env")
  "Absolute path to the env file where environment variables are set.")
```

If you don't have your `.spacemacs.env` files, it is generated first in `~`, avoiding contaminating the `.spacemacs.d` folder.

This solves the problem, but the drawback is that it returns to its original value after you `git pull` in `.emacs.d`.

## Solution 2 (what I'm using right now): Create symbol link for the `env` file

I create several `env` files for different machines in `.spacemacs.d` and create symbol link in `~`.

-   `.spacemacs.env.machine1`
-   `.spacemacs.env.machine2`
-   `.spacemacs.env.machine3`

```sh
ln -s ~/Dropbox/sync_folder/.spacemacs.d/.spacemacs.env.machine1 ~/.spacemacs.env
```

So now I have separated `env` files for different machines, they will not affect each other. Probably two machines with the same OS can share them as well.

## Potential solution: just move the `.spacemacs.env` to `~` after it is generated

Once the file is generated in `.spacemacs.d` (usually when you initialize the Spacemacs), move it to `~`. The Spacemacs can still find it.

I haven't try this myself. But I think it will work. The difference between this solution and Solution 2 is that the latter one has version control, either through Dropbox or git. If you think you need to keep track of this file, use Solution 2, otherwise just use the Potential solution.
