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

Ubuntu 18.04 LTS + LimeSDR Mini.

# Installation

There are two methods to finish the task. However, they are exclusive. One should choose **only one** of them. The mixed choice is not going to work.

Portal:

-   Method One: right below. Install via PPA. (Personally recommended)
-   Method Two: [anchor link](./#method-two). Install via source build.

## Method One

Install both SoapySDR and Lime Suite via the system package management system (`apt`).

### Step 1 - SoapySDR

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

`ppa:myriadrf/drivers` is the one that contains the `SoapySDR` package.

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

#using soapy sdr for remote device support? Optional
sudo apt-get install soapysdr-module-remote soapysdr-server
```

The key point here is, there is no module called `soapysdr`, use `soapysdr-tools` instead.

After this step, you should be able to use `SoapySDRUtil`. Try:

```sh
SoapySDRUtil --info
```

This tells you the packages or interfaces that SoapySDR supports.

-   Example `--info` Output:

```
user@server:~$ SoapySDRUtil --info
######################################################
## Soapy SDR -- the SDR abstraction library
######################################################

Lib Version: v0.6.1-2
API Version: v0.6.0
ABI Version: v0.6
Install root: /usr
Search path: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6
Search path: /usr/local/lib/x86_64-linux-gnu/SoapySDR/modules0.6
Search path: /usr/local/lib/SoapySDR/modules0.6
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libHackRFSupport.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libLMS7Support.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libRedPitaya.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libairspySupport.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libaudioSupport.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libbladeRFSupport.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libosmosdrSupport.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libremoteSupport.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/librtlsdrSupport.so
Module found: /usr/lib/x86_64-linux-gnu/SoapySDR/modules0.6/libuhdSupport.so
Loading modules... linux; GNU C++ version 7.3.0; Boost_106501; UHD_003.010.003.000-0-unknown

done
Available factories...airspy, audio, bladerf, hackrf, lime, null, osmosdr, redpitaya, remote, rtlsdr, uhd,
```

If you probe the device, the output might be:

```
user@server:~$ SoapySDRUtil --probe
######################################################
## Soapy SDR -- the SDR abstraction library
######################################################

Probe device
linux; GNU C++ version 7.3.0; Boost_106501; UHD_003.010.003.000-0-unknown

Cannot connect to server socket err = No such file or directory
Cannot connect to server request channel
jack server is not running or cannot be started
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
libusb: error [_get_usbfs_fd] libusb couldn't open USB device /dev/bus/usb/001/010: Permission denied
libusb: error [_get_usbfs_fd] libusb requires write access to USB device nodes.
[ERROR] SoapySSDPEndpoint::sendTo(udp://[ff02::c]:1900) = -1
  sendto(udp://[ff02::c]:1900) [99: Cannot assign requested address]
Cannot connect to server socket err = No such file or directory
Cannot connect to server request channel
jack server is not running or cannot be started
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
Cannot connect to server socket err = No such file or directory
Cannot connect to server request channel
jack server is not running or cannot be started
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
Cannot connect to server socket err = No such file or directory
Cannot connect to server request channel
jack server is not running or cannot be started
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock
JackShmReadWritePtr::~JackShmReadWritePtr - Init not done for -1, skipping unlock

----------------------------------------------------
-- Device identification
----------------------------------------------------
  driver=Audio
  hardware=Audio
  device_id=0
  origin=https://github.com/pothosware/SoapyAudio

----------------------------------------------------
-- Peripheral summary
----------------------------------------------------
  Channels: 1 Rx, 0 Tx
  Timestamps: NO
  Other Settings:
     * Stereo Sample Offset - Offset stereo samples for off-by-one audio inputs.
       [key=sample_offset, default=0, type=string, options=(-2, -1, 0, 1, 2)]
     * Rig Control - Select hamlib rig control type.
       [key=rig, type=string, options=(2901, 2516, 2517, 2513, 2518, 508, 506, 505, 504, 514, 503, 515, 502, 501, 513, 516, 1701, 2506, 2503, 2303, 2304, 902, 903, 221, 229, 238, 2501, 2507, 2512, 2301, 236, 2515, 1, 2, 354, 302, 303, 372, 304, 306, 307, 360, 355, 309, 310, 311, 312, 370, 313, 361, 314, 315, 316, 373, 319, 320, 321, 322, 367, 323, 346, 324, 326, 327, 347, 357, 363, 328, 329, 362, 330, 345, 356, 331, 332, 334, 344, 368, 365, 335, 3001, 3003, 3002, 402, 401, 403, 404, 336, 358, 340, 337, 341, 338, 339, 343, 366, 369, 342, 371, 605, 606, 607, 2511, 1801, 215, 233, 217, 219, 220, 223, 226, 234, 227, 230, 225, 214, 202, 203, 228, 201, 204, 216, 231, 237, 224, 205, 206, 207, 208, 209, 210, 222, 211, 213, 239, 1004, 374, 2514, 353, 352, 2801, 2401, 1105, 1103, 804, 2702, 2701, 2502, 232, 1404, 1402, 2509, 2201, 364, 351, 1603, 1612, 1604, 1605, 1607, 1602, 1601, 1608, 1609, 1611, 1613, 802, 806, 801, 803, 812, 810, 811, 133, 2601, 2602, 1204, 1501, 1502, 1503, 1504, 1505, 1506, 1507, 1509, 117, 119, 118, 121, 103, 124, 134, 129, 127, 110, 105, 106, 107, 109, 120, 111, 101, 122, 115, 123, 113, 114, 128, 131, 116, 135, 132, 130, 104, 125, 126, 2508)]
     * Rig Serial Rate - Select hamlib rig serial control rate.
       [key=rig_rate, default=57600, type=string, options=(1200, 2400, 4800, 9600, 19200, 38400, 57600, 115200, 128000, 256000)]
     * Rig Serial Port - hamlib rig Serial Port dev / COMx / IP-Address
       [key=rig_port, default=/dev/ttyUSB0, type=string]

----------------------------------------------------
-- RX Channel 0
----------------------------------------------------
  Full-duplex: YES
  Supports AGC: YES
  Stream formats: CS8, CS16, CF32
  Native format: CS16 [full-scale=65536]
  Stream args:
     * Channel Setup - Input channel configuration.
       [key=chan, default=mono_l, type=string, options=(mono_l, mono_r, stereo_iq, stereo_qi)]
  Antennas: RX
  Full gain range: [0, 0] dB
  Full freq range: [0, 6000] MHz
    RF freq range: [0, 6000] MHz
  Sample rates: 0.0441, 0.048 MSps
```

Basically it will find the **audio card** in your computer and **can not detect the LimeSDR Mini** (at least on my computer). It is recommended that you remove the `audio` module. So that the audio card is not detected every time. Also, the "Jack server" warning will disappears.

```sh
sudo apt remove limesdr0.6-module-audio
```

It is indicated that

> libusb: error [\_get\_usbfs\_fd] libusb couldn't open USB device /dev/bus/usb/001/010: Permission denied
> 
> libusb: error [\_get\_usbfs\_fd] libusb requires write access to USB device nodes.

So I guess that's why we need Lime Suite. Notice that the packages in Section "[SDR hardware Packages](https://github.com/pothosware/PothosCore/wiki/Ubuntu#sdr-hardware-packages)" are not necessary, since we will be working on only the LimeSDR Mini. Anyway, you can use

```sh
sudo apt install soapysdr-module-all
```

to install the individual modules all at once. I believe that the module named `soapysdr-module-lms7` is for the LimeSDR system, but I have not tried to use that individually. You may give it a try, and comment if it works or not.

### Step 2 - Lime Suite

Next, install the Lime Suite **from PPA**. Just follow the instruction in the [Lime Suite page](https://wiki.myriadrf.org/Lime_Suite#Ubuntu_PPA).

```sh
sudo add-apt-repository -y ppa:myriadrf/drivers
sudo apt-get update
sudo apt-get install limesuite liblimesuite-dev limesuite-udev limesuite-images
sudo apt-get install soapysdr soapysdr-module-lms7
```

Maybe the third line is not necessary. Lime Suite also plays an important role, and I will discuss that later in [Other issue - Use LimeSDR Mini in srsLTE - Step 2](./#step-2---calibration).

### Step 3 - Test

Plug in the LimeSDR Mini and try to probe it again.

Here is the expected output:

```
user@server:~$ SoapySDRUtil --probe
######################################################
## Soapy SDR -- the SDR abstraction library
######################################################

Probe device
linux; GNU C++ version 7.3.0; Boost_106501; UHD_003.010.003.000-0-unknown

[ERROR] SoapySSDPEndpoint::sendTo(udp://[ff02::c]:1900) = -1
  sendto(udp://[ff02::c]:1900) [99: Cannot assign requested address]
[INFO] Make connection: 'LimeSDR Mini [USB 3.0] 1D3ACXXXXXXXXX'
[INFO] Reference clock 40.00 MHz
[INFO] Device name: LimeSDR-Mini
[INFO] Reference: 4e+07 MHz
[INFO] LMS7002M calibration values caching Disable

----------------------------------------------------
-- Device identification
----------------------------------------------------
  driver=FT601
  hardware=LimeSDR-Mini
  boardSerialNumber=0x1d3ac6d55f1263
  firmwareVersion=5
  gatewareVersion=1.26
  hardwareVersion=0
  protocolVersion=1

----------------------------------------------------
-- Peripheral summary
----------------------------------------------------
  Channels: 1 Rx, 1 Tx
  Timestamps: YES
  Sensors: clock_locked, lms7_temp
  Registers: BBIC
  GPIOs: MAIN

----------------------------------------------------
-- RX Channel 0
----------------------------------------------------
  Full-duplex: YES
  Supports AGC: NO
  Stream formats: CF32, CS12, CS16
  Native format: CS16 [full-scale=2048]
  Stream args:
     * Buffer Length - The buffer transfer size over the link.
       [key=bufferLength, units=samples, default=0, type=int]
     * Link Format - The format of the samples over the link.
       [key=linkFormat, default=CS16, type=string, options=(CS16, CS12)]
  Antennas: NONE, LNAH, LNAL_NC, LNAW
  Corrections: DC removal
  Full gain range: [-12, 61] dB
    TIA gain range: [0, 12] dB
    LNA gain range: [0, 30] dB
    PGA gain range: [-12, 19] dB
  Full freq range: [0, 3800] MHz
    RF freq range: [30, 3800] MHz
    BB freq range: [-10, 10] MHz
  Tune args:
     * LO Offset - Tune the LO with an offset and compensate with the baseband CORDIC.
       [key=OFFSET, units=Hz, default=0.0, type=float, range=[-1e+07, 1e+07]]
     * BB - Specify a specific value for this component or IGNORE to skip tuning it.
       [key=BB, units=Hz, default=DEFAULT, type=float, range=[-1e+07, 1e+07], options=(DEFAULT, IGNORE)]
  Sample rates: [0.1, 65] MSps
  Filter bandwidths: [1.4, 130] MHz
  Sensors: lo_locked
  Other Settings:
     * TSP DC Level - Digital DC level in LMS7002M TSP chain.
       [key=TSP_CONST, type=int, range=[0, 32767]]

----------------------------------------------------
-- TX Channel 0
----------------------------------------------------
  Full-duplex: YES
  Supports AGC: NO
  Stream formats: CF32, CS12, CS16
  Native format: CS16 [full-scale=2048]
  Stream args:
     * Buffer Length - The buffer transfer size over the link.
       [key=bufferLength, units=samples, default=0, type=int]
     * Link Format - The format of the samples over the link.
       [key=linkFormat, default=CS16, type=string, options=(CS16, CS12)]
  Antennas: NONE, BAND1, BAND2
  Full gain range: [-12, 64] dB
    PAD gain range: [0, 52] dB
    IAMP gain range: [-12, 12] dB
  Full freq range: [0, 3800] MHz
    RF freq range: [30, 3800] MHz
    BB freq range: [-10, 10] MHz
  Tune args:
     * LO Offset - Tune the LO with an offset and compensate with the baseband CORDIC.
       [key=OFFSET, units=Hz, default=0.0, type=float, range=[-1e+07, 1e+07]]
     * BB - Specify a specific value for this component or IGNORE to skip tuning it.
       [key=BB, units=Hz, default=DEFAULT, type=float, range=[-1e+07, 1e+07], options=(DEFAULT, IGNORE)]
  Sample rates: [0.1, 65] MSps
  Filter bandwidths: [5, 40], [50, 130] MHz
  Sensors: lo_locked
  Other Settings:
     * TSP DC Level - Digital DC level in LMS7002M TSP chain.
       [key=TSP_CONST, type=int, range=[0, 32767]]
```

It lists all the parameters available in LimeSDR Mini.

I have no idea on solving the

> [ERROR] SoapySSDPEndpoint::sendTo(udp://[ff02::c]:1900) = -1
> 
> sendto(udp://[ff02::c]:1900) [99: Cannot assign requested address]

issue yet. I will share if there is anything new. It is not a big deal and you can use the LimeSDR Mini as usual.

Done.

## Method Two

The second method is to build the software suite from the source.

The **advantage** is the software is more up-to-date. For example, the SoapySDR is 0.7.x right now on Github, while the PPA version is 0.6.x.

The **disadvantage** is that the softwares might be harder to maintain or uninstall.

**Update: this method can not make the LimeSDR mini work through SoapySDR on my computer. It only works via LimeSuite.**

### Step 1 - SoapySDR

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

It indicates that there is `no module found`. Now we need the Lime Suite.

### Step 2 - Lime Suite

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

Check the `SoapySDRUtil` info and probe:

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

Now we found the LimeSDR module via `lime`. The probe result is

```
SoapySDRUtil --probe
######################################################
##     Soapy SDR -- the SDR abstraction library     ##
######################################################

Probe device
[INFO] Make connection: 'LimeSDR Mini [USB 3.0] 1D3AC6D55F1263'
[INFO] Reference clock 40.00 MHz
[INFO] Device name: LimeSDR-Mini
[INFO] Reference: 40 MHz
[INFO] LMS7002M calibration values caching Disable
[1]    22136 segmentation fault (core dumped)  SoapySDRUtil --probe
```

Finally, I encounter this issue, **segmentation fault**. I have no idea how to solve it yet. I'll update this post if I make it.

# Other issue

## Use LimeSDR Mini in `srsLTE`

srsLTE supports **only the `pdsch` examples** for LimeSDR currently. They are still working on developing the other APIs.

There are two more steps to enable LimeSDR in srsTLE.

### Step 1 - Add library supports

Check [this mail list thread](http://www.softwareradiosystems.com/pipermail/srslte-users/2017-July/001000.html) to learn the basic idea.

-   If you are using the `apt` to install SoapySDR and LimeSuite, you need an extra package:
    
    ```sh
    sudo apt-get install libsoapysdr-dev
    ```
    
    This add the library in the `/usr/lib/x86_64-linux-gnu/`, where srsLTE tries to locate the libsoapysdr.
    
    Next, `cmake`, `make` and `make install` srsLTE again.

-   If you install SoapySDR and LimeSuite via **source build**, you may want to create a soft link so that the `libsoapysdr.so` is in the folder I mention above. I haven't tried this yet.

### Step 2 - Calibration

-   Open `LimeSuiteGUI` (in terminal).
-   Connect the device by `Options` -> `ConnectionSettings`.
-   Click "Default" on the top-right corner.
-   Click "Calibrate All" in the "Calibrations" tab.

### Step 3 - Run srsLTE `pdsch` examples

```sh
cd {your_srslte_dir}/build/lib/examples
./pdsch_ue -f 7315000000 -r 1234
```

The frequency should be set to the available LTE base station frequencies nearby. You need to know that first.

If you have other SDR device like bladrRF or USRP, you may first run `./cell_search` and find the available cells.

## Docker Image

I build a docker image with SoapySDR + LimeSuite + srsLTE + srsGUI. You may have a try.

See [lanternd/limesdr-mini - Docker Hub](https://hub.docker.com/r/lanternd/limesdr-mini/).
