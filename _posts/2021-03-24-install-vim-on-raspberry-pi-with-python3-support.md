---
layout: post
title: Install Vim on Raspberry Pi with Python3 Support
description: Install the latest version of vim on Raspberry Pi (4B in my case).
permalink: /install-vim-on-raspberry-pi-with-python3-support/
categories: [blog]
tags: [Raspberry Pi, vim, python, support]
date: 2021-03-24 20:52:53
---

# Why

We need to have `+python3` in `vim --version` output.

Before (`vim` by `sudo apt install vim`):

```shell
$ vim --version | ag "python"
+cmdline_hist      +langmap           -python            +visual
+cmdline_info      +libcall           -python3           +visualextra
```

After (my manually installed `vim`):

```shell
$ vim --version | ag "python"
+comments          +libcall           -python            +visual
+conceal           +linebreak         +python3           +visualextra
Linking: gcc -lrt -L/usr/local/lib -Wl,--as-needed -o vim -lSM -lICE -lXt -lX11 -lXdmcp -lSM -lICE -lm -ltinfo -ldl -L/usr/local/lib/python3.8/config-3.8-arm-linux-gnueabihf -lpython3.8 -lcrypt -lpthread -ldl -lutil -lm -lm
```

# How

To find the detail steps for installing vim in local machine: [Install Vim for Local User](../install-vim-for-local-user/) (My previous post).

What makes it special is that I install **my own python** version (3.8 in my case) on the Raspberry Pi.

Key step:

```shell
./configure --prefix=$HOME/.local --enable-python3interp --with-python3-config-dir=/usr/local/lib/python3.8/config-3.8-arm-linux-gnueabihf --with-python3-command=/usr/bin/python
```

Note:

-   `--with-python3-config-dir` needs the config dir of your python3 version, which is machine-dependent. The built-in python3's config dir is `/usr/lib/python3.7/config-3.7m-arm-linux-gnueabihf/`. My manually installed python3's config dir is shown in the above command.
-   `--with-python3-command=` can set to be the output of `which python` (or `which python3`).

You need to see the following in the output of `./configure` to guarantee the success of compilation:

```shell
...
checking --enable-pythoninterp argument... no
checking --enable-python3interp argument... yes
checking --with-python3-command argument... /usr/bin/python
checking Python version... 3.8
checking Python is 3.0 or better... yep
checking Python's abiflags...
checking Python's install prefix... /usr/local
checking Python's execution prefix... /usr/local
checking Python's configuration directory... (cached) /usr/local/lib/python3.8/config-3.8-arm-linux-gnueabihf
checking Python3's dll name... libpython3.8.a
checking if -pthread should be used... yes
checking if compile and link flags for Python 3 are sane... yes
checking if -fPIE can be added for Python3... yes
...
```

**Wrong** example:

```
...
checking --enable-pythoninterp argument... no
checking --enable-python3interp argument... yes
checking --with-python3-command argument... /usr/bin/python
checking Python version... 3.8
checking Python is 3.0 or better... yep
checking Python's abiflags...
checking Python's install prefix... /usr/local
checking Python's execution prefix... /usr/local
checking Python's configuration directory... (cached) /usr/local/lib/config-3.8-arm-linux-gnueabihf/config
cat: /usr/local/lib/config-3.8-arm-linux-gnueabihf/config/Makefile: No such file or directory
auto/configure: line 6766: cd: /usr/local/lib/config-3.8-arm-linux-gnueabihf/config: No such file or directory
checking Python3's dll name...
checking if -pthread should be used... yes
checking if compile and link flags for Python 3 are sane... yes
checking if -fPIE can be added for Python3... yes
...
```

If `Python3's dll name...` output is NULL, then you need to double check your python config dir again. Otherwise you will encounter the following error during `make`:

```
/usr/bin/ld: /usr/local/lib/libpython3.8.a(thread.o): undefined reference to symbol 'pthread_getspecific@@GLIBC_2.4'
/usr/bin/ld: //lib/arm-linux-gnueabihf/libpthread.so.0: error adding symbols: DSO missing from command line
collect2: error: ld returned 1 exit status
link.sh: Linking failed
make: *** [Makefile:2134: vim] Error 1
```

If no error prompt out, then just `make && make install`.

Do not forget to set your `vim` alias in your `.bashrc` or `.zshrc`.

If you need `+python` support, locate Python 2.7 related paths accordingly.

# Read More

-   <https://stackoverflow.com/questions/19901934/libpthread-so-0-error-adding-symbols-dso-missing-from-command-line>
-   [Compiling vim with python3 support! - Siddharth Kannan's Blog](https://blog.siddharthkannan.in/vim/2019/08/31/compiling-vim-with-python/)
