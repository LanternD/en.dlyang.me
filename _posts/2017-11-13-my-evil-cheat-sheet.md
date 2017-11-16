---
layout: post
title: My Evil Cheat Sheet
description: Evil-mode is an Emacs layer that allows editing using Vim. Therefore this is a also a cheat sheet for Vim itself.
permalink: /my-evil-cheat-sheet/
categories: [blog]
tags: [spacemacs, emacs, vim, evil, hacking]
date: 2017-11-13 12:34:56
---

# Cheat Sheet for Evil mode

## Navigating

-   `h`
-   `j`
-   `k`
-   `l`
-   `w`: move forward by one word
-   `b`: move backward by one word, the opposite of `w`.
-   `e`: move forward to the end of a word
-   `gg`
-   `G`
-   `:<NUM>`: Go to line number
-   `0`: = `Home`
-   `$`: = `End`
-   `C-u`: move up half screen
-   `C-d`: move down half screen
-   `C-f`: move down a whole page
-   `C-b`: move up a whole page

## Enter Insert State

-   `i`
-   `a`
-   `I`
-   `A`
-   `$a`
-   `s`: delete a char and insert.
-   `S`: (substitute) delete the whole line and start from the begining, = `0C`.

## Editing

-   `y`: yank/copy
-   `yy`: yank the current line
-   `p`: paste
-   `P`: paste before cursor
-   `d`: delete/cut
-   `D`: delete to the end of the line
-   `dt.`: delete to the period. Similar as `df.`, which will delete `.` as well.
-   `u`: undo
-   `C-R`: redo
-   `x`: delete char at current position.
-   `X`: delete char before current position.

## Replace

-   `r`
-   `R`
-   `:s/old_word/new_word/gc`: `g` means "global", parameter `c` means "confirmation"
-   `cw`: change word

## Search

-   `/`: search forward.
-   `?`: search backward.
-   `*` or `#`: find the previous/next occurance of current word in Evil-mode.
-   `f<char>`: find the next `<char>`. `f3c` can find the 3rd occurence of `c`.
-   `F<char>`: the opposite of the above.
-   `t<`: find forward and land right before the char.

## Miscellaneous Command

-   `:!<command>`
-   `.`: repeat the previous command. Be careful of what is the "previous command".

## Formatting

-   `~`: toggle upper and lower case of the current char.
-   `gq ap`: format the whole paragraph.

## Visual Mode

-   `v`: select char
-   `V`: select line
-   `C-v`: select paragraph

## Advanced

-   `daw`: delete around word.
-   `diw`: delete inside word.
-   `dis`
-   `das`
-   `cis`: delete and insert at current sentence
-   `dip`: paragraph
-   `dap`
-   `di'` / `da'`: single quote
-   `di"` / `da"`: double quote
-   ``[ai]["`([{"]``: all kinds of scope
-   `dit` / `dat`: inside / around tag
-   replace `d` above by `v`: visualize the designated scope.
-   `vipyjjp`: copy this paragraph and paste it below. (just some combination)
-   `qa`, insert a `:` at the beginning of the line, go to next line, `q`: finish recording a macro, next, `100@a`, now, next 100 lines has a `:` in front of them.
-   Some possible macros:
    -   Search within the line for "widget";
    -   Go to the end of line and add a `.`;
    -   Delete any whitespaces at the end of the line.
-   `cs"'`: change the surrounding double quotes to single ones.
-   `cs'<p>`: change single quotes to `<p>`.
-   `ds'`: delete the surrounding single quotes.
-   `ysiw'`: wrap current word with `'`.
-   `:%y+`: copy all, = `Ctrl + A` in casual text editor.
    -   `gg"+yG`: similar function.
    -   `ggvG`: similar function, text not copied. Press `y` to do so.
