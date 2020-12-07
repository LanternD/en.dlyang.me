---
layout: post
title: DEBUG > AUCTeX Failed to Respect the Tex-master Change
description: What to do if the `pdflatex` command failed to run because of change of the Tex-master variable.
permalink: /debug-auctex-failed-to-respect-the-tex-master-change/
categories: [blog]
tags: [Emacs, AUCTeX, LaTeX, debug, compile]
date: 2020-12-06 16:03:18
---

# Problem

After I duplicated one of my LaTeX project folders and changed the name of the main file, the compile command will not find the new main file.

It worked fine if I compiled within the main file. However, when I changed the bottom matters of the sub-source `.tex` files, the AUCTeX failed to recognize the new main file name.

The project has the following files (simplified for illustration purpose):

-   `new_main.tex` (was "`old_main.tex`")
-   `1_intro.tex`
-   `2_method.tex`
-   `3_evaluation.tex`
-   `4_conclusion.tex`

In each of the sub-files, I have the variables section, identifying the main file to use.

```tex
%%% Local Variables: 
%%% mode: latex
%%% TeX-master: "new_main"
%%% End: 
```

(It was `TeX-master: "old_main"`.) The purpose of this part is that you can initiate the compile command from the sub-source files, without the need to switch back to the main file.

---

The error message was like:

> ```shell
> Running `LaTeX' on `old_main' with ``pdflatex  -file-line-error  --synctex=1 -interaction=nonstopmode old_main.tex''
> This is pdfTeX, Version 3.14159265-2.6-1.40.19 (TeX Live 2018) (preloaded format=pdflatex)
>  restricted \write18 enabled.
> entering extended mode
> ! I can't find file `old_main.tex'.
> <*> old_main.tex
> 
> (Press Enter to retry, or Control-D to exit)
> Please type another input file name
> ! Emergency stop.
> <*> old_main.tex
> 
> !  ==> Fatal error occurred, no output PDF file produced!
> Transcript written on texput.log.
> 
> TeX Output exited abnormally with code 1 at Sun Dec  6 15:58:55
> ```

# Diagnose

Basically, I changed the name of the main file to use, but the AUCTeX failed to load the new value and kept trying the `old_main`.

# Solution

Go to the sub-source `.tex` files, run `revert-buffer` (<kbd>M-x</kbd> or in Spacemacs <kbd>SPC SPC</kbd>). Done!
