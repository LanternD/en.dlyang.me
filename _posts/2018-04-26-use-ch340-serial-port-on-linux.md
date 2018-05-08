---
layout: post
title: Use CH340-based USB Serial Converter on Linux in Python
description: CH340 is a chip that convert USB data to serial data. Of cause the method discuss here can be applied to other USB-serial converter chips, such as PL2303 etc. It is helpful when you want to do serial communication with your circuit board. Usually I write Python scripts to interact with serial devices.
permalink: /use-ch340-serial-port-on-linux/
categories: [blog]
tags: [USB, serial, command]
date: 2018-04-26 16:34:56
---

# Find the Device

In your terminal, run

```sh
lsusb
```

If your device is plugged, you can see an item about it. If not, make sure your circuit board is functioning well.

Next, run

```sh
dmesg | grep ttyUSB
```

Usually the name should be something like `ttyUSB0`.

# Change Your Permission

Use `chmod` to change device access permission.

```sh
sudo chmod 777 /dev/ttyUSBx
```

(replace the 'x' with your device number.)

# Try to Open the Serial Port in Python

In python script, use `pyserial` library to handle the serial devices.

```python
import pyserial

ser = serial.Serial('/dev/ttyUSB0', '9600', timeout=2)
ser.write('your command\r\n'.encode('ascii'))  # convert to ASCII before sending it
buf = ser.read(100)  # read 100 bytes

print(buf.decode('utf-8'))
```

Basically this is how it works.

Note: On Windows, the `/dev/ttyUSB0` string should usually be `COM0` etc. That's the difference.
