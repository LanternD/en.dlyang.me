---
layout: post
title: [DEBUG LOG] SAM G53 Cannot Transmit Data to PC through EDBG UART
description: A small bug that wastes me an afternoon and a whole night! EDBG is a embedded debug port that helps to debug or depoly the code. It has a virtual serial COM port that can support data communication between MCU and the host PC. I assume that this is known if you are going to read this post.
permalink: /sam-g53-uart-cannot-transmit-data-to-pc-through-edbg-uart/
categories: [blog]
tags: [SAM G53, UART, EDBG, debug, MCU]
date: 2018-05-09 23:42:19 
---

# Bug Description

As said above, I spend lots of time dealing with it. However, the solution is so simple.

The bug is like this. I created a project (let me called it Project X) in Atmel Studio 7, running on the **SAM G53 Xplained Pro evaluation kit**, and did some stepper motor control service. However, no matter what I send using `uart_write(UART0, data_byte)`, the PC just couldn't get it. I opened an old project, with similar stepper motor control code. And the UART communication works so well!

Actually, the UART worked smoothly in any other projects except the Project X. I did be able to read the data flow using a oscilloscope if the data is transmitted successfully. The Project X UART0 TX port only had HIGH voltage level.

Clearly there is some small difference between the projects that led to this bug.

# Failed Solutions

Most of the time I spent was on locating the problem. Fixing the bug is not that time consuming though. I tried several methods and none of them worked.

## Change CPU Clock

The first thing I noticed is that the clock in Project X was 480,005,120 Hz, while the others were 49,152,000 Hz. I changed the multiple factor in `config/conf_clock.h` (line 74).

```c
#define CONFIG_PLL0_MUL             1500 //before: 1465
```

(32768 \* 1500 = 49152000, 36768 \* 1465 = 48005120)

This only has minor affects on the actually baudrate. It is not the root cause.

## Internal Test Loop

SAM G53 offers an internal loop test method to debug the UART port. (File: Atmel-11240\_32-bit-Cortex-M4-Microcontroller\_SAM-G53\_Datasheet.pdf, [link](http://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-11240-32-bit-Cortex-M4-Microcontroller-SAM-G53_Datasheet.pdf), around Page 750, Figure 32-14, Section 32.5.8 Test Modes).

This allows you test the UART port in miscellaneous ways.

If you are going to enable one of the test mode, add the following code after the UART initialization function.

```c
UART0->UART_MR = UART0->UART_MR | UART_MR_CHMODE_LOCAL_LOOPBACK;
```

Macros for the other two modes can be found in `componet_uart.h`.

I could received the data byte that I sent through the TX port, however my computer still couldn't get it.

## Configure the GPIO

This was actually where the bug located. But I still made some mistakes before I found the real solution.

The `UART0` uses `PA09` pin as the TX, I initialized the pin as following:

```c
ioport_set_pin_mode(EXT3_PIN_13, IOPORT_MODE_MUX_A);
ioport_set_pin_dir(EXT3_PIN_13, IOPORT_DIR_OUTPUT);
```

Didn't work.

# Solution

When I run the initialization code step by step, I found the missing part. I missed a macro in line 105 of file `/ASF/sam/boards/samg53_xplained_pro/board_init.c`. There is a board UART console initialization code:

```c
#if defined (CONF_BOARD_UART_CONSOLE)
  /* Configure UART pins */
  ioport_set_port_peripheral_mode(PINS_UART0_PORT, PINS_UART0,
      PINS_UART0_FLAGS);
#endif
```

Here is the final solution. Add the following code to whichever header file you like, while `config/conf_board.h` is preferred.

```c
/** Enable Com Port. */
#define CONF_BOARD_UART_CONSOLE
```

Thanks for watching.
