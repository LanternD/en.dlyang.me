---
layout: post
title: ~[DEBUG LOG] Resolve Character Decoding Error in Spacemacs on Windows
description: I encountered a wierd bug on my newly-bought laptop that runs a Windows OS. The character cannot be decoded correctly in Spacemacs (Emacs 26.1). Here is a quick fix. 
permalink: /resolve-character-decoding-error-in-spacemacs-on-windows/
categories: [blog]
tags: [emacs, spacemacs, character, debug, display]
date: 2019-03-01 21:31:35 
---


# Problem

The problem is like this: the system fails in displaying some of the Chinese characters. If you check the `Messages` buffer, the error is: "Invalid coding system: cp65001" or "file mode specification error: coding-system-error cp65001".

![img](../assets/post-img/resolve-character-decoding-error-in-spacemacs-on-windows/spacemacs-before.png "Bug")


# Solution

I found the solution on Reddit: [Invalid coding system: cp65001](https://www.reddit.com/r/emacs/comments/98qq5k/invalid_coding_system_cp65001/).

Basically the solution is to disable the "BETA: Use Unicode UTF-8 for worldwide language support".

![img](../assets/post-img/resolve-character-decoding-error-in-spacemacs-on-windows/solution.png "Solution")

Remember to reboot the computer.


# After Fixing

Here is what it looks like after the bug is fixed.

![img](../assets/post-img/resolve-character-decoding-error-in-spacemacs-on-windows/spacemacs-after.png "After fixing")

Done
