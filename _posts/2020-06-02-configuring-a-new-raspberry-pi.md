---
layout: post
title: Configuring A New Raspberry Pi
description: A short note about what I've done to set the Pi up.
permalink: /configuring-a-new-raspberry-pi/
categories: [blog]
tags: [Raspberry Pi, configuration]
date: 2020-06-02 16:35:14
---

# A new Raspberry Pi

Let's get started and setup our new Raspberry Pi!

## Whatever config

Use `sudo raspi-config` to configure the basic of the system, including:

-   Display
-   WLAN
-   Audio
-   Password
-   Hostname

This command will be also used in this post.

## Default password

`raspberry`, FYI.

## Reliable reference

The `bash` / `zsh` history from previous setuped Raspberry Pi, including default user and the `root`.

# Guideline

Do the following in order:

-   Set root password.
-   Install vim.
-   Enable `ssh`.
-   Install `xrdp`.
-   (Optional but recommanded) Change username from `pi` to something else.
-   (Optional) Change hostname.
-   Install `zsh`.
-   `sudo apt update` and `sudo apt upgrade`.
-   Update python to a newer version.
-   Install other software/packages.

# Enable SSH

Source: [SSH (Secure Shell) - Raspberry Pi Official Documentation](https://www.raspberrypi.org/documentation/remote-access/ssh/).

1.  `sudo raspi-config`
2.  `Interfacing Options`
3.  SSH

## About root login

Enable root login by changing the `/etc/ssh/sshd_config`, around line 32, `PermitRootLogin yes`.

Restart `ssh` service:.

```shell
sudo service ssh restart
```

I prefer to allow root login only at the initialization stage. Otherwise, only switch to root from your normal user. Don't allow root login through `ssh`.

# Enable `xrdp`

Read more: [How to Install Xrdp Server (Remote Desktop) on Raspberry Pi](https://linuxize.com/post/how-to-install-xrdp-on-raspberry-pi/).

```shell
sudo apt-get install xrdp
```

How you can access the pi GUI desktop via remote desktop apps.

# Change the Username of Default `pi`

Change the name from `pi` to whatever else.

Source: [How to Change the Default Account Username and Password - PiHut](https://thepihut.com/blogs/raspberry-pi-tutorials/how-to-change-the-default-account-username-and-password).

Read more: [[HowTo!]Change default username pi](https://www.raspberrypi.org/forums/viewtopic.php?t=231702)

First of all we will make sure the user `pi` do not run any program.

Login via `ssh` as `root`, run `who` to check:

```shell
root@your-hostname:~# who
pi       tty1         2020-06-02 21:34
root     pts/0        2020-06-02 21:34
```

Stop the services by `pi`:

```shell
systemctl list-units --type=service --state=running
systemctl stop getty@tty1.service
who
```

Make sure there is no `pi` running services. If there is any, kill them all by.

```shell
pkill -KILL -u pi
```

Then follow the description in the referance link above.

```shell
usermod -l newusername pi
ls /home  # pi folder
usermod -m -d /home/newusername newusername
ls /home  # changed to 'newusername' folder
groupmod -n newusername pi  # change group name
```

Logout and re-login using the new username.

Change password by `passwd`.

Change the `ssh` root login permission to "no" in `sshd_config`.

# Change Hostname

`sudo raspi-config` -> `System Options` -> `S4 Hostname`.

# Change Default Boot-to

Read more: [Adding PIXEL/GUI to Raspbian Lite](https://gist.github.com/kmpm/8e535a12a45a32f6d36cf26c7c6cef51).

By default the system will boot to GUI desktop. You can change this to command line to save power and CPU resources.

`sudo raspi-config` -> `System Options` -> `S5 Boot / Auto Login` -> `B2 Console Autologin`.

## Start GUI desktop from command line

Install `Xinit` and run `startx`. See the "Read more" link above.

# Setup Vim

`git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

Copy/link `.vimrc` to `$HOMEDIR`.

In `vim`: `:PluginInstall`

Or `vim +PluginInstall +qall` in command line.

# Upgrade `python`

Source: [Installing the latest Python 3 on Raspberry Pi](https://samx18.io/blog/2018/09/05/python3_raspberrypi.html). Read more: [Python 3 Installation & Setup Guide](https://realpython.com/installing-python/).

The default python is 3.7.x. You may upgrade it to a higher version.

Follow the link above.

-   Switch to root (`sudo su`).
-   Download installation files.
-   Install dependencies.
-   Configure and install python. Note that you should use `make altinstall` to avoid overriding the system default python. Otherwise unexpected error could happen.

Note: The whole `make` process takes about 40 minutes to finish on a Raspberry Pi 3B+.

## `lsb_release` issue

Installing the python from source may lack of the `lsb_release` executable.

We can create a symbolic link for it.

Source: [No module named 'lsb\_release' after install Python 3.6.3 from source](https://askubuntu.com/questions/965043/no-module-named-lsb-release-after-install-python-3-6-3-from-source).

```shell
sudo ln -s /usr/share/pyshared/lsb_release.py /usr/local/lib/python3.9/site-packages/lsb_release.py
```

## Install python packages

Note: Some packages, like `numpy`, `scipy`, `pillow`, should be installed via `sudo apt-get install`, not `python -m pip install`. Otherwise building dependencies will fail.

It can take hours. Be patient.

# Tips

## Pinout map

If we install a python library `gpiozero`, we can check the pinout of the Raspberry Pi in the command line by `pinout` command.

```shell
python -m pip install gpiozero
pinout
```

Output:

```shell
RAM                : 1024MbRAM
Storage            : MicroSD
USB ports          : 4 (excluding power)
Ethernet ports     : 1
Wi-fi              : True
Bluetooth          : True
Camera ports (CSI) : 1
Display ports (DSI): 1

J8:
   3V3  (1) (2)  5V
 GPIO2  (3) (4)  5V
 GPIO3  (5) (6)  GND
 GPIO4  (7) (8)  GPIO14
   GND  (9) (10) GPIO15
GPIO17 (11) (12) GPIO18
GPIO27 (13) (14) GND
GPIO22 (15) (16) GPIO23
   3V3 (17) (18) GPIO24
GPIO10 (19) (20) GND
 GPIO9 (21) (22) GPIO25
GPIO11 (23) (24) GPIO8
   GND (25) (26) GPIO7
 GPIO0 (27) (28) GPIO1
 GPIO5 (29) (30) GND
 GPIO6 (31) (32) GPIO12
GPIO13 (33) (34) GND
GPIO19 (35) (36) GPIO16
GPIO26 (37) (38) GPIO20
   GND (39) (40) GPIO21

For further information, please refer to https://pinout.xyz/
```
