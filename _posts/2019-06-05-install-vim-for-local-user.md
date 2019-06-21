---
layout: post
title: Install Vim for Local User
description: A short post showing how to install vim for local user. For my own record
permalink: /install-vim-for-local-user/
categories: [blog]
tags: [vim, software, install, Linux]
date: 2019-06-05 11:13:22 
---

# Why do I need to install `vim` for local user?

Sometimes I `ssh` to other servers to develop code. The server is shared with many other people. If you update the `vim` using `sudo`, other people's `.vimrc` may encounter problems. So we install our own version, and keep the environment clean.

# Steps

Basically I follow this website: [Is it possible to install vim for a user? - StackOverflow](https://superuser.com/questions/228366/is-it-possible-to-install-vim-for-a-user).

-   Download `vim`. Currently the version is 8.1 (the machine version is 7.2).

```sh
git clone https://github.com/vim/vim.git
cd vim/src
```

-   Change the "prefix" in `src/MakeFile` to `$HOME/.local`.
-   Install `ncurses-devel` if you haven't done so. This actually requires `sudo` permission. Note: the package name varies with the OS distribution, please check [this](https://www.ostechnix.com/how-to-install-ncurses-library-in-linux/).
-   In the `src` folder, run `make`.
-   If no error occurs, run `make install`.
-   You will see `bin` and `share` under your `$HOME/.local/` folder.
-   Add the alias in your `.bashrc` or `.zshrc`.

```sh
alias vim="$HOME/.local/bin/vim"
```

Note: I tried to add `$HOME/.local/bin` to `$PATH` but failed. The `vim` is still the old version. The alias works for me.

# End

Now there is no "Unknown option: relativenumber" error showing up when I open `vim`.
