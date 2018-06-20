---
layout: post
title: Using LimeSDR Mini on Ubuntu with Lime Suite and SoapySDR
description: Step by step installation of the software needed for LimeSDR mini to run on Ubuntu.
permalink: /limesdr-mini-on-ubuntu/
categories: [blog]
tags: [Ubuntu, SDR, LimeSDR Mini, API, driver, installation]
date: 2018-06-19 18:24:51 
---

# Introduction

## About LimeSDR Mini

[LimeSDR Mini](https://www.crowdsupply.com/lime-micro/limesdr-mini) is a minimized/lite version of [LimeSDR](https://www.crowdsupply.com/lime-micro/limesdr). It costs \\$179 when comes with a pair of antennae.

You can check the hardware specification in the product link. The hardware source schematics and PCB files are available on [Github - myriadrf](https://github.com/myriadrf/LimeSDR-Mini).

## About Lime Suite

[Lime Suite](http://wiki.myriadrf.org/Lime_Suite) is a software package developed by [myriadRF](https://myriadrf.org). myriadRF and Lime Microsystems are very close to each other. I guess myriadRF is for open source, while Lime micro is for commercial profit. Both of their websites advertise the LimeSDR.

Lime Suite provides the driver of LMS7 and the API to SoapySDR.

## About SoapySDR

[SoapySDR](https://github.com/pothosware/SoapySDR/wiki) is a software suite developed by [Pothosware](http://www.pothosware.com/) that provides uniform API to the host system.

Its introduction on the website says:

> A fresh and clean vendor neutral and platform independent SDR support library.

Basically, SoapySDR communicates with the SDR API, and packages it into a new API. As we known, there are so many SDR hardwares available on the market. Yet most of them implement their individual drivers, which is painful for the RF developers to migrate their projects to different hardwares. So SoapySDR builds a bridge to connect miscellaneous SDR drivers.

## Test Environment

Ubuntu 18.04 LTS.

# Installation

There are two methods to finish the task. However, they are exclusive. One should choose **only one** of them. The mixed choice is not going to work.

Portal:

-   Method One: right below. Install via PPA.
-   Method Two: [anchor link](./#method-two). Install via source build.

## Method One

Install both SoapySDR and Lime Suite via system package management system.

### Step 1

**Always install SoapySDR first!** [Here](https://github.com/pothosware/PothosCore/wiki/Ubuntu) is the post that you may want to follow.

```sh
#core framework and toolkits (required)
sudo add-apt-repository -y ppa:pothosware/framework

#support libraries for pothos (required)
sudo add-apt-repository -y ppa:pothosware/support

#supplies soapysdr, and drivers (required)
sudo add-apt-repository -y ppa:myriadrf/drivers

sudo apt-get update
```

`ppa:myriadrf/drivers` is the one that contains the SoapySDR package.

After that,

```sh
sudo apt-get install pothos-all

#install bindings for python2
sudo apt-get install python-pothos

#or install bindings for python3
sudo apt-get install python3-pothos

#install development files for python blocks
sudo apt-get install pothos-python-dev
```

Next, Install Soapy SDR runtime and utility packages:

```sh
#soapy sdr runtime and utilities
sudo apt-get install soapysdr-tools 

#python language bindings
sudo apt-get install python-soapysdr python-numpy

#python3 language bindings
sudo apt-get install python3-soapysdr python3-numpy

#using soapy sdr for remote device support?
sudo apt-get install soapysdr-module-remote soapysdr-server
```

The key point here is, there is no module called `soapysdr`, use `soapysdr-tools` instead.

After this step, you should be able to use `SoapySDRUtil`. Try:

```sh
SoapySDRUtil --probe
```

Output:

```
######################################################   
##     Soapy SDR -- the SDR abstraction library     ##   
######################################################    

Probe device  
----------------------------------------------------    
-- Device identification  
----------------------------------------------------     
  driver=null  
  hardware=null  
----------------------------------------------------     
-- Peripheral summary  
----------------------------------------------------     
  Channels: 0 Rx, 0 Tx  
  Timestamps: NO  
```

It tells you no device is found. So that's why we need Lime Suite. Notice that the packages in Section "[SDR hardware Packages](https://github.com/pothosware/PothosCore/wiki/Ubuntu#sdr-hardware-packages)" are not necessary, since we will be working on LimeSDR Mini. Anyway, you can use

```sh
sudo apt install soapysdr-module-all
```

to install the individual modules all at once. I believe that a module named "soapysdr-module-lms7" is for the LimeSDR system, but I have not tried to use that individually. You may give it a try, and comment if it works or not.

### Step 2

Next, install the Lime Suite **from PPA**. Just follow the instruction in the [Lime Suite page](https://wiki.myriadrf.org/Lime_Suite#Ubuntu_PPA).

```sh
sudo add-apt-repository -y ppa:myriadrf/drivers
sudo apt-get update
sudo apt-get install limesuite liblimesuite-dev limesuite-udev limesuite-images
sudo apt-get install soapysdr soapysdr-module-lms7
```

Maybe the third line is not necessary.

### Step 3 - Test

Plug in the LimeSDR Mini and try to probe it again.

Here is the expected output:

```
######################################################             
##     Soapy SDR -- the SDR abstraction library     ##             
######################################################             

Probe device                                                       
[INFO] Make connection: 'LimeSDR Mini [USB 3.0] 1D3AC6D55F1263'    
[INFO] Reference clock 40.00 MHz                                   
[INFO] Device name: LimeSDR-Mini                                   
[INFO] Reference: 40 MHz                                           
[INFO] LMS7002M calibration values caching Disable                 
[1]    1303 segmentation fault (core dumped)  SoapySDRUtil --probe 
```

I am currently working on solving the "LMS7002M calibration values caching Disable" issue. I will share if there is anything new.

Done.

## Method Two

The second method is to build the software suite from the source.

The **advantage** is the software is more up-to-date. For example, the SoapySDR is 0.7.x right now on Github, while the PPA version is 0.6.x.

The **disadvantage** is that the softwares might be harder to maintain or uninstall.

### Step 1

**Always install SoapySDR first!**

The build guide of SoapySDR can be found [here](https://github.com/pothosware/SoapySDR/wiki/BuildGuide).

Dependencies:

```sh
sudo apt-get install \
    cmake g++ \
    libpython-dev python-numpy swig
```

Make and install:

```sh
mkdir build
cd build
cmake ..
make
sudo make install
sudo ldconfig #needed on debian systems
SoapySDRUtil --info
```

The output is like:

```
######################################################
##     Soapy SDR -- the SDR abstraction library     ##
######################################################

Lib Version: v0.7.0-g69c16e98
API Version: v0.7.0
ABI Version: v0.7
Install root: /usr/local
Search path: /usr/local/lib/SoapySDR/modules0.7
No modules found!
Available factories... No factories found!
Available converters...
 -  CF32 -> [CF32, CS16, CS8, CU16, CU8]
 -  CS16 -> [CF32, CS16, CS8, CU16, CU8]
 -  CS32 -> [CS32]
 -   CS8 -> [CF32, CS16, CS8, CU16, CU8]
 -  CU16 -> [CF32, CS16, CS8]
 -   CU8 -> [CF32, CS16, CS8]
 -   F32 -> [F32, S16, S8, U16, U8]
 -   S16 -> [F32, S16, S8, U16, U8]
 -   S32 -> [S32]
 -    S8 -> [F32, S16, S8, U16, U8]
 -   U16 -> [F32, S16, S8]
 -    U8 -> [F32, S16, S8]
```

It indicates that there is no module found. Now we need the Lime Suite.

### Step 2

Installation guide: [Link](https://wiki.myriadrf.org/Lime_Suite#Building_from_source).

Dependencies:

```sh
#packages for soapysdr available at myriadrf PPA
sudo add-apt-repository -y ppa:myriadrf/drivers
sudo apt-get update

#install core library and build dependencies
sudo apt-get install git g++ cmake libsqlite3-dev

#install hardware support dependencies
sudo apt-get install libsoapysdr-dev libi2c-dev libusb-1.0-0-dev

#install graphics dependencies
sudo apt-get install libwxgtk3.0-dev freeglut3-dev
```

Build and install:

```sh
git clone https://github.com/myriadrf/LimeSuite.git
cd LimeSuite
mkdir builddir && cd builddir
cmake ../
make -j4
sudo make install
sudo ldconfig

cd ../LimeSuite/udev-rules
sudo bash ./install.sh
```

### Step 3 - Test

Check the SoapySDRUtil info and probe:

```sh
SoapySDRUtil --info
SoapySDRUtil --probe
```

Output:

```
######################################################
##     Soapy SDR -- the SDR abstraction library     ##
######################################################

Lib Version: v0.7.0-g69c16e98
API Version: v0.7.0
ABI Version: v0.7
Install root: /usr/local
Search path: /usr/local/lib/SoapySDR/modules0.7
Module found: /usr/local/lib/SoapySDR/modules0.7/libLMS7Support.so (18.06.1-739bd85)
Available factories... lime
Available converters...
 -  CF32 -> [CF32, CS16, CS8, CU16, CU8]
 -  CS16 -> [CF32, CS16, CS8, CU16, CU8]
 -  CS32 -> [CS32]
 -   CS8 -> [CF32, CS16, CS8, CU16, CU8]
 -  CU16 -> [CF32, CS16, CS8]
 -   CU8 -> [CF32, CS16, CS8]
 -   F32 -> [F32, S16, S8, U16, U8]
 -   S16 -> [F32, S16, S8, U16, U8]
 -   S32 -> [S32]
 -    S8 -> [F32, S16, S8, U16, U8]
 -   U16 -> [F32, S16, S8]
 -    U8 -> [F32, S16, S8]
```

Now we found the LimeSDR module via `lime`. The probe result is the same as the [Method 1 Step 3](./#step-3---test), so I won't show it here.

Done.
