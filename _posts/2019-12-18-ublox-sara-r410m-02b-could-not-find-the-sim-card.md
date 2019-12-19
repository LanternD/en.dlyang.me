---
layout: post
title: FIXED > uBlox SARA-R410M-02B Could not Find the SIM Card
description: I had a problem that the module failed to find the SIM card. This seems to be a common problem for this chip.
permalink: /ublox-sara-r410m-02b-could-not-find-the-sim-card/
categories: [blog]
tags: [ublox, hack, debug, hardware]
date: 2019-12-18 21:49:56
---

# Behavior

-   The module can be accessed via USB. The AT commands got delivered and replied.
-   The VSIM card has no power, which is supposed to be 1.8 V.
-   Got error with SIM card related commands:
    
    > AT+CNUM
    > 
    > +CME ERROR: SIM PIN required
    > 
    > AT+CCID?
    > 
    > +CME ERROR: SIM failure
    > 
    > AT+CSQ
    > 
    > +CSQ: 99,99
    > 
    > AT+CPIN?
    > 
    > +CME ERROR: SIM not inserted

# Related Posts

Here are similar posts about it:

-   [Sim Card not detected NB-IOT SARA N280-02B-00](https://portal.u-blox.com/s/question/0D52p00008HKDZoCAP/sim-card-not-detected-nbiot-sara-n28002b00)
-   [Network Connectivity Issue with SARA R410M-02B](https://portal.u-blox.com/s/question/0D52p00008nvKcn/network-connectivity-issue-with-sara-r410m02b)
-   [NB MKR 1500 - modem testing](https://forum.arduino.cc/index.php?topic=597738.15)

Seems it is a common problem.

# Reason

This was a hardware connection problem. I found that the `SIM_RST` pin and the `SIM_IO` short-circuited. Quite simple, right?

If you got a similar problem, check them with a multimeter first.

# I have to say

The key point of this post is, I would like to criticize the LGA footprint design of the module. If you look at the footprint document, you will find that the space between each pin is just too small. If you solder this module like me in a modified toast oven, probably you will get this problem. The best practice is to follow the instructions Section 3.3 in "SARA-R4\_SysIntegrManual\_(UBX-16029218)". You need a precisely controlled environment for its soldering process.

I sincerely hope that uBlox can design the footprint in a more robustly way. Anyway, the module is not cheap, and reworking nullifies all the warranty (as suggested by the manual).

# How to Resolve

If you have a failure in using the module, melt it down from the circuit, clean it up, and try again. Another suggestion is to use a smaller pad to replace the original ones. And you may want to extend the pad to the outside of the module courtyard.

# Bonus

The uBlox SARA-R410M-02B uses a different pin assignment for the UART interface. The `TXD` (Pin 12) is actually for **reception** on the SARA module, and the `RXD` (Pin 13) is the transmitting pin. I haven't noticed this on my version 1.0 board, then I had to make an updated version.
