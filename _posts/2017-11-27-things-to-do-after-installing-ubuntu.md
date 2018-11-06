---
layout: post
title: Things to Do After Installing Ubuntu
description: A quick note. It includes installing packages and configuring the fresh system.
permalink: /things-to-do-after-installing-ubuntu/
categories: [blog]
tags: [linux, system, OS, ubuntu]
date: 2017-11-27 16:34:56
---

Final update: 2018.06.25

Note:

-   You don't have to `sudo apt update` anymore after adding a apt-key or PPA after Ubuntu 18.04 LTS.
-   `apt` is equivalent (in most of the cases) to `apt-get`, so I just write `apt`.

# Software and Library Installation　

## TL;DR

Too long; didn't read version.

Run the following command directly to save (my) time. Check them all first if you are not familiar with them.

```shell
sudo apt install git emacs25 vim vim-gtk3 python-apt python-pip python3-pip curl zsh ruby-full cmake silversearcher-ag autojump gir1.2-gtop-2.0 gir1.2-networkmanager-1.0 autotools-dev automake fonts-powerline gtk2-engines-pixbuf gnome-themes-standard chrome-gnome-shell clang-6.0 shutter
```

Note: there is high probability that you fail to exectute the command with so many packages to install. You may want to install them separately.

## Install through CLI

Add `sudo` if needed. If you saw `agi` in the command, it is an alias to "sudo apt-get install". You can enable this feature after installing `Oh-My-Zsh` and the `Ubuntu` plugin.

### git

For version control.

```sh
apt install git
```

-   Global settings
    
    Change the iuser name and emaiError (use-package): exec-path-from-shell/:init: Non-zero exit code from shell /usr/bin/zsh invoked with args ("-l" "-i" "-c" "/usr/bin/printf '\_\_RESULT\\\\000%s\\\\000%s\\\\000\_\_RESULT' \\"\({PATH-87922f8a678e8c83b4bbdc20816cbc3c}\" \"\){MANPATH-87922f8a678e8c83b4bbdc20816cbc3c}\\""). Output was:

"open terminal failed: not a terminal " l before execution.

```shell
git config --global user.name "LanternD"
git config --global user.email the_email@gmail.com
git config --global core.editor emacs
git config --global credential.helper cache
```

### curl

A tool to access the url.

```sh
apt install curl
```

### Zsh (Z shell)

An augmented shell, a substitution of the default `bash`. `oh-my-zsh` further augments the Zsh with (better) package management.

```sh
apt install zsh
```

Follows by `oh-my-zsh` ([Official Github Link](https://github.com/robbyrussell/oh-my-zsh)).

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

after adding `ubuntu` plugins in `zsh`, we will have `alias agi="sudo apt-get install"` in the `~/.zshrc` file.

### cmake

```sh
apt install cmake
```

### tmux

Link: [tmux/tmux - Github](https://github.com/tmux/tmux)

A terminal multiplexer. It helps to manage terminal sessions and windows easily. A must have if you work extensively with CLI.

According to the doc, it depends on `libevent` and `ncurses`. Usually ncurses is already included in the system, so we just need [libevent](https://github.com/libevent/libevent#cmake-general).

Install `libevent`:

```sh
git clone https://github.com/libevent/libevent.git
cd libevent
mkdir build && cd build
cmake ..
make
sudo make install
```

Install `tmux`:

```sh
git clone https://github.com/tmux/tmux.git
cd tmux
sh autogen.sh
./configure && make
sudo make install
```

Read more:

-   A popular tmux configuration by [gpakosz](https://github.com/gpakosz/.tmux).
-   If you want to start `tmux` each time you start the terminal, add the following two lines to the `.zshrc` file.
    
    ```sh
    [[ $- != *i* ]] && return
    [[ -z "$TMUX" ]] && exec tmux
    ```

---

A note here: should install Dropbox and synchronize everything before proceed.

---

### pyenv

Link: [Pyenv/pyenv - GitHub](https://github.com/pyenv/pyenv)

A great Python version management tool. You can easily switch between 2.x and 3.x (or whatever) versions globally, with consistent `python xxx.py` command.

-   Install the required packages first. See [here](https://github.com/pyenv/pyenv/wiki/Common-build-problems).
    
    ```sh
    sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev
    ```

-   Install `pyenv` through the official installation script in [this link](https://github.com/pyenv/pyenv-installer#github-way-recommended).
    
    ```sh
    curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer | bash
    ```

-   Don't forget the add `PATH` and `eval` stuff to the `.bashrc` or `.zshrc` (Step 3 in the installation tutorial).
    
    ```sh
    export PATH="~/.pyenv/bin:$PATH"
    eval "$(pyenv init -)"
    eval "$(pyenv virtualenv-init -)"
    ```

After the installation, **use `pyenv` to install certain python version**.

```sh
pyenv install 3.6.5
pyenv install 2.7.15
python global 3.6.5
```

Get ride of every annoying version selection between Python 2.7.x and 3.6.x.

### pip

Python package management system. Note that this is for the Python in the system, not the one installed by `pyenv`. After you switch to the `pyenv` Python, the `pip` also changed by itself.

```sh
apt install python-pip python3-pip
sudo pip install --upgrade pip
```

For Python packages, see [my another post](../python-packages-installation/).

### clang

[Link](https://clang.llvm.org/). A language fontend for C and C++.

```sh
agi clang-6.0
```

### Emacs (Spacemacs)

`Emacs` is the "best" editor after configuration, while `Spacemacs` is **best** editor and IDE, because it is equipped with `evil` (a vim emulator).

```sh
apt install emacs25
```

-   Emacs Configuration
    1.  First `git clone` the `.emacs.d` to `~` directory.
        
        ```sh
        git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d
        ```
    2.  Use symbolic link to create `~/.spacemacs.d` folder. (for my personal use only)
        
        ```sh
        ln -s ~/Dropbox/Misc_Cfg_Sync/.spacemacs.d ~/.spacemacs.d
        ```
        
        (You can put your own Spacemacs configuration in (`~/.spacemacs.d` folder.)

### svn (Optional)

An old version control software.

```sh
agi subversion
```

### vim

Great editor. Need some more configurations.

```sh
apt install vim vim-gtk3
```

Seems `vim-gtk3` is needed to yank text to system clipboard.

### Sublime Text 3

Official site: [Linux Repositories](https://www.sublimetext.com/docs/3/linux_repositories.html#apt)

```shell
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text
```

### LaTeX environment (work with Spacemacs)

-   TeXlive
    
    A complete LaTeX distribution, maintained by a group. Cross-plateform, first choice.
    
    ```sh
    agi texlive-full
    ```
    
    It has 4.4 GB, so be **patient**. I recommend you install it in the end.

-   PDF viewer: `Envice` by default in GNOME.

-   Spacemacs settings:
    
    `SPC SPC customize-variable RET tex-view-program-selection RET`, insert `evince` as `output-pdf` viewer.

### Ruby (for Jekyll)

**Tutorial**: [Ruby Installation](https://www.ruby-lang.org/en/documentation/installation/)

```sh
agi ruby-full
```

The packages in ruby:

-   install `jekyll` (`bundler` is required to run jekyll)
    
    ```sh
    sudo gem install jekyll bundler
    bundle install
    ```

-   To run jekyll:
    
    ```sh
    bundle exec jekyll serve
    ```

### Pinyin input method

1.  fcitx

    Follow this [link](https://fcitx-im.org/wiki/Install_(Ubuntu)).
    
    ```sh
    add-apt-repository ppa:fcitx-team/stable
    apt-get update
    agi fcitx fcitx-module-cloudpinyin fcitx-googlepinyin fcitx-sunpinyin
    ```
    
    [!important] `fcitx` only works in `Xorg` environment, make sure you log into that.
    
    Let `fcitx` start after loging-in. Use `gnome-tweaks-tool` to do so.

2.  Sogou Pinyin Input Method

    **Tutorial**: [Sogou Pinyin Official Help](https://pinyin.sogou.com/linux/help.php)
    
    -   Make sure `fcitx` is installed properly.
    -   Enter `im-config` in terminal, set the corresponding items.
    -   Install Sogou Pinyin via the `.deb` package.

### gtk missing packages

Sometimes the `gtk+` GUI looks ugly, that is because of the missing of some packages, such as `pixmap` and `adwaita`.

This can be reproduced by running a software with command line. There will be a warning like:

> Gtk-WARNING \*\*: Unable to locate theme engine in module\_path: "pixmap"
> 
> Gtk-WARNING \*\*: Unable to locate theme engine in module\_path: "adwaita"

Install them to solve this issure.

```sh
agi gtk2-engines-pixbuf
agi gnome-themes-standard
```

### ag

**Tutorial**: [the\_silver\_searcher - Github](https://github.com/ggreer/the_silver_searcher)

A fast code searching tool.

```sh
agi silversearcher-ag
```

### autojump

A great tool to boost the efficiency. For example, if your project directory is `~/aa/bb/cc/dd/ee/my_project`. After you visit there once, you can jump to the your project folder by a simple command `j my_project`. Fantastic!

```sh
agi autojump
```

### Shutter

Link: [Shutter Project](http://shutter-project.org/downloads/).

One of the best screenshot tools on Ubuntu.

```sh
agi shutter
```

If you want to edit the photo after screenshot, you may need a plugin.

Bind the shortcut: See [this post](https://en.dlyang.me/tips-on-ubuntu/#taking-area-screenshot-with-shortcut).

### PostgreSQL (Optional)

**Tutorial**: [How to Install PostgreSQL 10 on Ubuntu 16.04 and 14.04 LTS](https://tecadmin.net/install-postgresql-server-on-ubuntu/)

-   Installation
    
    Add the Apt Repo to source list in Ubuntu and then sudo install.
    
    ```sh
    agi postgresql postgresql-contrib
    ```
    
    Python use `psycopg2` to manipulate the PostgreSQL database. Do not forget to install it as well.
    
    ```sh
    pip install psycopg2
    ```

-   Setting user info
    
    **Tutorial**: [Setting a password for the `postgres` user](http://suite.opengeo.org/docs/latest/dataadmin/pgGettingStarted/firstconnect.html#setting-a-password-for-the-postgres-user)
    
    Use `psql` command and `\password` command to do so.
    
    Update: it would be less painful to create a new role (user) and use it to create a database.

### pgAdmin (Optional)

A python-written program that manages PostgreSQL. Install it using python wheel. Use python in system (not those in `pyenv`) to install.

```sh
pip install pgAdmin
```

This app requires `sudo` permission to run.

### powerline

-   Official site: [powerline/powerline - GitHub](https://github.com/powerline/powerline)
-   Installation: [powerline - readthedocs.io](https://powerline.readthedocs.io/en/latest/installation.html)

An enhanced status bar for `vim`, `zsh`, `tmux`, etc.

```sh
pip install powerline-status
```

## Install via `.deb` file

### Google Chrome

Of cause. Link: [Chrome](https://www.google.com/chrome/).

### Dropbox

Use the client provided by Dropbox. [Download link](https://www.dropbox.com/install).

### VNC Viewer

It supports connection from remote computers.

[Download](https://www.realvnc.com/en/connect/download/viewer/), install, login, done. `Google Remote Desktop` somewhat does not support Ubuntu 17.10.

The `VNC Viewer` only works under `Xorg` environment. `VNC Connect` is the server software required in the computer to be connected to.

### Visual Studio Code

[Link](https://code.visualstudio.com/docs/setup/linux).

An open source programming IDE provided by Microsoft.

### TeXstuidio

Link: [texstudio.org](https://www.texstudio.org/).

A substitution if you are not interested in working in Spacemacs. Still need `texlive-full` installation.

Found the corresponding package for the system in the link.

## Other Installation

These packages are installed via `ppa` or downloaded `.tar.gz` files. They are not directly accessible or have multiple steps, so you need to click into the website and follow the instructions out there.

-   [KiCad](http://kicad-pcb.org/download/ubuntu/): an open source schematics and PCB EDA software.
-   [bladeRF](https://github.com/Nuand/bladeRF/wiki/Getting-Started%253A-Linux#easy-installation-for-ubuntu-the-bladerf-ppa): the driver for the bladeRF software-defined radio.
-   [Java SE Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)
    -   Check the installation walkthrough on [WikiHow](https://www.wikihow.com/Install-Oracle-Java-JRE-on-Ubuntu-Linux).
-   [PyCharm](https://www.jetbrains.com/pycharm/download/#section=linux): one of the best Python IDE.
-   [FileZilla](https://filezilla-project.org/download.php): a file transfer software with multiple protocols supported.
-   [Zotero](https://www.zotero.org/download/): a document management system. It organizes everything perfectly, especially my paper database.
    -   [Installation guide](https://www.zotero.org/support/installation)
    -   `Zotfile`: [Link](http://zotfile.com/)

# Settings

## GitHub SSH key

Follow the instructions on these two posts:

-   [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
-   [Adding a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)

## Remove Unused Folders in `Home`

**Tutorial**: [Ubuntu - permanently remove ~/Videos and ~/Public](https://superuser.com/questions/223918/ubuntu-permanently-remove-videos-and-public)

Change the following:

-   `~/.config/user-dirs.dirs`.
-   `/etc/xdg/user-dirs.conf`: `enabled=False`.
-   `/etc/xdg/user-dirs.defaults`.

Then we can `rmdir` those folders.

## Replace `Caps Lock` by `Ctrl`

**Tutorial**: [MovingTheCtrlKey - EmacsWiki](https://www.emacswiki.org/emacs/MovingTheCtrlKey)

Install `GNOME Tweaks` and changes the settings: `Keyboard & Mouse` -> `Additional Layout Options` -> `Caps Lock key behavior` -> `Caps Lock is also a Ctrl`.

## Enable `vim` in `sudo` mode

In `.zshrc` file, add:

`alias svim="sudo -E vim"`

## Enable Chinese Character Input in Spacemacs

In `.zshrc` file, add:

`alias emacs_chn="LC_CTYPE=zh_CN.UTF-8 emacs &"`

Use `emacs_chn` to open `Spacemacs`.

## Disable Auto Printer Discovery

Tutorial: [How do I disable automatic remote printer installation?](https://askubuntu.com/a/556963)

-   `svim /etc/cups/cups-browsed.conf`
-   Add (uncomment) this line: `BrowseProtocols none`
-   `sudo service cups-browsed restart`
-   `sudo service cups restart`

## SSH timeout settings

Prevent the disconnection due to keyboard inactive.

Link: [解决SSH自动断线，无响应的问题](<https://www.coder4.com/archives/3751>)

```sh
sudo vim /etc/ssh/ssh_config
# Add or uncomment the following code at client side
ServerAliveInterval 20
ServerAliveCountMax 999
```

And

```sh
sudo vim /etc/ssh/sshd_config
# Uncomment the following code at server side 
ClientAliveInterval 30
ClientAliveCountMax 6
```

(Sometimes this file is not there. You need to create one.)

# UI Related

## Add Fonts

**Tutorial**: [How To Install New Fonts In Ubuntu 14.04 and 16.04](https://itsfoss.com/install-fonts-ubuntu-1404-1410/)

Font list:

-   Source Code Pro
-   Operator
-   Fira Code
-   icon font (For Spacemacs. See [NeoTree](https://github.com/jaypei/emacs-neotree) and [all-the-icons](https://github.com/domtronn/all-the-icons.el) GitHub page)
-   Chinese fonts

## Gnome Extensions

-   We can find plenty of extensions from the official Gnome website:
    
    [Gnome Extensions](https://extensions.gnome.org/)

-   Some of the helpful ones:
    -   `system-monitor` (there is a hyphen in the word). Need to install `gir` dependencies before installing this extensions.
        
        ```
        agi gir1.2-gtop-2.0 gir1.2-networkmanager-1.0
        ```
    
    -   `OpenWeather`: A plugin for the live weather conditions.
    -   `User themes`: an extension that changes **shell** (the top bar) themes from user directory.

## Beautify the UI

Use `ocs-url` to install them (see how to install `osc-url` [here](https://www.linux-apps.com/p/1136805/)).

### Theme

-   Install `chrome-gnome-shell` first:
    
    ```sh
    apt install chrome-gnome-shell
    ```

-   Theme: [Ant Theme](https://www.gnome-look.org/p/1099856/)

### Icons

-   Icons theme: [Papirus Icons](https://www.gnome-look.org/p/1166289/)

-   Set the **theme and icons** in `Gnome-tweak-tool`, the one used in setting the Caps Lock key.

-   Change **folder icons**:
    -   Tutorial: [Custom icon selection - AskUbuntu](https://askubuntu.com/questions/79110/how-can-i-assign-custom-icons-to-folders)
    -   Key point: the custom icons are in `~/.local/share/icons/`. The default icons are in `/usr/share/icons/`.
    -   Open the properties window for the folder, click the icon and select.
    -   Change the following: Downloads, Github, Dropbox etc.

### ZSH themes (Optional)

Most of the work is done by synchronizing the `.oh-my-zsh` folder and `.zshrc` file via Dropbox, the rest things we can do is:

-   Install powerline fonts. [powerline/fonts - GitHub](https://github.com/powerline/fonts)
    
    ```shell
    agi fonts-powerline
    ```

-   Install the powerline plugin (see [above](./#powerline)).

## Remove Redundant Icons and Softwares (Optional)

-   Amazon Link in the docker
    
    ```sh
    sudo rm -f /usr/share/applications/com.canonical.launcher.amazon.desktop
    sudo rm -f /usr/share/applications/ubuntu-amazon-default.desktop
    ```

-   Firefox browser
    
    (You may keep it in case Google Chrome crashes.)
    
    ```sh
    sudo apt-get autoremove firefox firefox-locale-en
    ```

# Lagacy (not used anymore)

### ~~Google Drive~~

**Update**: I don't use Google Drive anymore because it doesn't officially support Linux.

Bad solution: In Ubuntu `Settings`, enter `Online Accounts`, and add `Google` account. After a while, the files in Google Drive will be synchonized as a mounted folder.

Better solution: the above method is not convenient. Use `Grive2` instead.

-   [Grive2 - Github](https://github.com/vitalif/grive2)
    
    Just follow the instructions. Remember to add the `.griveignore` file before running `grive -a` command.

### GNU Radio

Tutorials: [GNURadio - GitHub](https://github.com/gnuradio/gnuradio#pybombs)

Follow the instruction. Use `pybombs` to install it. It will take care of UHD at the same time.

### WhatPulse

A tool for keyboard and mouse input statistic.

**Tutorial**: [WhatPulse Linux Installation](http://help.whatpulse.org/kb/client/linux-installation)

Optional.
