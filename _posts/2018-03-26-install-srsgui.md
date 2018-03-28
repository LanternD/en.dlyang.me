---
layout: post
title: Steps to successfully install srsGUI
description: srsGUI is the graphic user interface (GUI) for srsLTE. There are some dependencies issues to be solved to make it.
permalink: /install-srsgui/
categories: [blog]
tags: [srsGUI, library, software, srsLTE]
date: 2018-03-26 16:34:56
---

# About srsGUI

As mentioned in [srsLTE - GitHub](https://github.com/srsLTE/srsLTE#build-instructions), srsGUI is an optional requirements for real time plotting. Today we are going to install it.

# Steps

Certainly, one can follow the instructions on `srsGUI` website: [srsLTE/srsGUI - GitHub](https://github.com/srslte/srsgui#download--install-instructions).

## Install `boost`

`sudo apt-get install libboost-system-dev libboost-test-dev libboost-thread-dev`

## Install `Qt4` and `Qwt6`

`sudo apt-get install libqwt-dev libqt4-dev`

### Alternative approach (try the above one first)

1.  Download `Qwt6` from the official website: [Qwt User's Guide](http://qwt.sourceforge.net/qwtinstall.html#DOWNLOAD).
2.  Install libs to install `Qwt6`:

`sudo apt install libqt4-dev libqt4-dev-bin libqt4-opengl-dev libqtwebkit-dev qt4-linguist-tools qt4-qmake`

1.  Install `Qwt6`:

```sh
qmake qwt.pro
make
sudo make install
```

## Install `srsGUI`

If there is nothing missing, run:

```sh
mkdir build && cd build
cmake ../
make
sudo make install
```

The printout of `cmake` is like:

```sh
-- 
-- Configuring Boost C++ Libraries...
-- Boost version: 1.62.0
-- Found the following Boost libraries:
--   thread
--   unit_test_framework
--   system
--   chrono
--   date_time
--   atomic
-- Boost version: 106200
-- Boost include directories: /usr/include
-- Boost library directories: /usr/lib/x86_64-linux-gnu
-- Boost libraries: /usr/lib/x86_64-linux-gnu/libboost_thread.so;/usr/lib/x86_64-linux-gnu/libboost_unit_test_framework.so;/usr/lib/x86_64-linux-gnu/libboost_system.so;/usr/lib/x86_64-linux-gnu/libboost_chrono.so;/usr/lib/x86_64-linux-gnu/libboost_date_time.so;/usr/lib/x86_64-linux-gnu/libboost_atomic.so;/usr/lib/x86_64-linux-gnu/libpthread.so
-- Found Qwt: /usr/lib/libqwt.so (found version "6.1.2") 
--    srsGUI library will be installed.
-- Configuring done
-- Generating done
-- Build files have been written to: /home/Software/srsGUI/build
```

If you have missing package, it would be like

```sh
-- 
-- Configuring Boost C++ Libraries...
-- Boost version: 1.62.0
-- Found the following Boost libraries:
--   thread
--   unit_test_framework
--   system
--   chrono
--   date_time
--   atomic
-- Boost version: 106200
-- Boost include directories: /usr/include
-- Boost library directories: /usr/lib/x86_64-linux-gnu
-- Boost libraries: /usr/lib/x86_64-linux-gnu/libboost_thread.so;/usr/lib/x86_64-linux-gnu/libboost_unit_test_framework.so;/usr/lib/x86_64-linux-gnu/libboost_system.so;/usr/lib/x86_64-linux-gnu/libboost_chrono.so;/usr/lib/x86_64-linux-gnu/libboost_date_time.so;/usr/lib/x86_64-linux-gnu/libboost_atomic.so;/usr/lib/x86_64-linux-gnu/libpthread.so
-- Looking for Q_WS_X11
-- Looking for Q_WS_X11 - found
-- Looking for Q_WS_WIN
-- Looking for Q_WS_WIN - not found
-- Looking for Q_WS_QWS
-- Looking for Q_WS_QWS - not found
-- Looking for Q_WS_MAC
-- Looking for Q_WS_MAC - not found
-- Found Qt4: /usr/bin/qmake (found version "4.8.7") 
-- Could NOT find Qwt (missing: QWT_LIBRARY QWT_INCLUDE_DIR) 
--    QT4 or Qwt6 not found. srsGUI library is not generated
-- Configuring done
-- Generating done
-- Build files have been written to: /home/Software/srsGUI/build
```

After we install `srsGUI`, we can build `srsLTE` again.

# Read More

[srsLTE Build Process - ShareTechNote](http://www.sharetechnote.com/html/SDR_srsLTE_Build.html#Boost_Installation)
