---
layout: post
title: Thinks to Do After Installing Ubuntu 17.10
description: A quick note. It includes installing packages and configuring the system. Most of the stuff works for other Ubuntu versions as well.
permalink: /things-to-do-after-installing-ubuntu/
categories: [blog]
tags: [linux, system, OS, ubuntu]
date: 2017-11-27 16:34:56
---

Final update: 2018.03.20

# Software and Library Installation　

## TL;DR

`sudo apt install git emacs25 vim python-apt python-pip python3-pip curl zsh ruby-full cmake silversearcher-ag autojump gir1.2-gtop-2.0 gir1.2-networkmanager-1.0`

## Install through CLI

Add `sudo` if needed.

### git

`apt install git`

-   Global settings
    -   `git config --global user.name "LanternD"`
    -   `git config --global user.email the_email@gmail.com`
    -   `git config --global core.editor emacs`
    -   `git config --global credential.helper cache`

### curl

`apt install curl`

### Zsh (Z shell)

`apt-get install zsh`

Follows by `oh-my-zsh` ([Official Github Link](https://github.com/robbyrussell/oh-my-zsh)).

`sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

### pyenv

Link: [Pyenv/pyenv - GitHub](https://github.com/pyenv/pyenv)

-   Install the required packages first. See [here](https://github.com/pyenv/pyenv/wiki/Common-build-problems).

`sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncursesservice cups restart5-dev libncursesw5-dev xz-utils tk-dev`

-   Install `pyenv` through the official installation script in [this link](https://github.com/pyenv/pyenv-installer).

`curl -L https://raw.githubusercontent.com/pyenv/pyenv-installer/master/bin/pyenv-installer \| bash`

Don't forget the add `PATH` and `eval` stuff to the `.bashrc` or `.zshrc` (Step 3 in the installation tutorial).

After the installation, **use `pyenv` to install certain python version**.

`python global 3.6.x`

Get ride of every annoying version selection between Python 2.7.x and 3.6.x.

### pip

`apt install python-pip python3-pip`

### Emacs

`apt install emacs25`

1.  Emacs Configuration

    1.  First `git clone` the `.emacs.d` to `~` directory.
    2.  Use symbolic link to create `~/.spacemacs.d` folder. `ln -s ~/Dropbox/Misc_Cfg_Sync/.spacemacs.d ~/.spacemacs.d`

### Vim

`apt install vim`

### Sublime Text 3

Official site: [Linux Repositories](https://www.sublimetext.com/docs/3/linux_repositories.html#apt)

```sh
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text
```

### LaTeX environment

-   TeXlive
    
    `apt-get install texlive-full`
    
    It has 4.4 GB, so be **patient**.

-   PDF viewer: `Envice` by default in GNOME.
    
    `customize-variable RET tex-view-program-selection RET`, insert `evince` as `output-pdf` viewer.

### Ruby

**Tutorial**: [Ruby Installation](https://www.ruby-lang.org/en/documentation/installation/)

`apt-get install ruby-full`

The packages in ruby:

-   gem: `apt-get install rubygems`. (Usually it is included in the `ruby-full` installation.)
-   jekyll: `gem install jekyll bundler`.
    -   (`bundler` is required to run jekyll)
    -   Run `bundle install` after `bundler` is installed.
    -   `bundle exec jekyll serve`.

### cmake

Simply `apt install cmake`.

### WhatPulse

**Tutorial**: [WhatPulse Linux Installation](http://help.whatpulse.org/kb/client/linux-installation)

Optional.

### Zotero

-   [Installation guide](https://www.zotero.org/support/installation)
-   `Zotfile`: [Link](http://zotfile.com/)

### Sogou Pinyin Input Method

**Tutorial**: [Sogou Pinyin Official Help](https://pinyin.sogou.com/linux/help.php)

-   Make sure `fcitx` is installed.
-   Enter `im-config` in terminal, set the corresponding items.
-   Install Sogou Pinyin via the `.deb` package.
-   Let `fcitx` start after loging-in. Use `gnome-tweaks-tool` to do so.
-   [!important] `fcitx` only works in `Xorg` environment, make sure you logged into that.

### ag

**Tutorial**: [the\_silver\_searcher - Github](https://github.com/ggreer/the_silver_searcher)

A fast code searching tool.

`apt-get install silversearcher-ag`

### autojump

`agi autojump`

(after adding `ubuntu` plugins in `zsh`, we will have `alias agi="sudo apt-get install`.)

### PostgreSQL

**Tutorial**: [How to Install PostgreSQL 10 on Ubuntu 16.04 and 14.04 LTS](https://tecadmin.net/install-postgresql-server-on-ubuntu/)

-   Installation

Add the Apt Repo to source list in Ubuntu and then sudo install.

`sudo apt-get install postgresql postgresql-contrib`

Python use `psycopg2` to manipulate the PostgreSQL database. Do not forget to install it as well.

`pip install psycopg2`

-   Setting user info

**Tutorial**: [Setting a password for the `postgres` user](http://suite.opengeo.org/docs/latest/dataadmin/pgGettingStarted/firstconnect.html#setting-a-password-for-the-postgres-user)

Use `psql` command and `\password` command to do so.

Update: it would be less painful to create a new role (user) and use it to create a database.

### pgAdmin

A python-written program that manages PostgreSQL. Install it using python wheel. Use python in system (not those in `pyenv`) to install.

`pip install pgAdmin`

This app requires `sudo` permission to run.

### powerline

-   Official site: [powerline/powerline - GitHub](https://github.com/powerline/powerline)
-   Installation: [powerline - readthedocs.io](https://powerline.readthedocs.io/en/latest/installation.html)

`pip install powerline-status`

## Install via `.deb` file

### Google Chrome

Of cause. Link: [Chrome](https://www.google.com/chrome/).

### Dropbox

Use the client provided by Dropbox. [Download link](https://www.dropbox.com/install).

### VNC Viewer

It supports connection from remote computers.

[Download](https://www.realvnc.com/en/connect/download/viewer/), install, login, done. `Google Remote Desktop` somewhat does not support Ubuntu 17.10.

The `VNC Viewer` only works under `Xorg` environment.

### Visual Studio Code

An programming IDE provided by Microsoft. [Link](https://code.visualstudio.com/docs/setup/linux).

## Install via `ppa`

-   [KiCad](http://kicad-pcb.org/download/ubuntu/)
-   [bladeRF](https://github.com/Nuand/bladeRF/wiki/Getting-Started%253A-Linux#Easy_installation_for_Ubuntu_The_bladeRF_PPA)

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

`alias svim="sudo -E vim"`

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

(Sometimes this file is not there.)

# UI Related

## Add Fonts

**Tutorial**: [How To Install New Fonts In Ubuntu 14.04 and 16.04](https://itsfoss.com/install-fonts-ubuntu-1404-1410/)

Font list:

-   Source Code Pro
-   Operator
-   Fira Code
-   icon font (see `NeoTree` GitHub page)
-   Chinese fonts

## Gnome Extensions

-   We can find plenty of extensions from the official Gnome website:

[Gnome Extensions](https://extensions.gnome.org/)

-   Some of the helpful ones:
    -   `system-monitor` (there is a hyphen in the word). Need to install `gir` dependencies before installing this extensions.

> `apt install gir1.2-gtop-2.0 gir1.2-networkmanager-1.0`

-   `OpenWeather`: A plugin for the live weather conditions.
-   `User themes`: an extension that changes **shell** themes from user directory.

## Remove Redundant Icons and Softwares

-   Amazon Link in the docker

`sudo rm -f /usr/share/applications/com.canonical.launcher.amazon.desktop`

`sudo rm -f /usr/share/applications/ubuntu-amazon-default.desktop`

-   Firefox browser

`sudo apt-get autoremove firefox firefox-locale-en`

## Beautify the UI

-   Use `ocs-url` to install them (install `osc-url` [here](https://www.linux-apps.com/p/1136805/)).

### Theme

-   Install `chrome-gnome-shell` first:
    -   `apt install chrome-gnome-shell`

-   Theme: [`Ant` Theme](https://www.gnome-look.org/p/1099856/)

### Icons

-   Icons theme: [Papirus Icons](https://www.gnome-look.org/p/1166289/)

-   Set the theme and icons in `Gnome-tweak-tool`, the one used in setting the Caps Lock key.

-   Change folder icons:
    -   Tutorial: [Custom icon selection - AskUbuntu](https://askubuntu.com/questions/79110/how-can-i-assign-custom-icons-to-folders)
    -   Key point: the custom icons are in `~/.local/share/icons/`. The default icons are in `/usr/share/icons/`.
    -   Open the properties window for the folder, click the icon and select.
    -   Change the following: Downloads, Github, Dropbox etc.

### ZSH themes

Most of the work is done by synchronizing the `.oh-my-zsh` folder and `.zshrc` file via Dropbox, the rest things we can do is:

-   Install powerline fonts. [powerline/fonts - GitHub](https://github.com/powerline/fonts)
-   Install the powerline plugin.

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
