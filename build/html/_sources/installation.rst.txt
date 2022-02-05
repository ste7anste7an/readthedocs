.. currentmodule:: installation
.. _installation:

Installation
============


Micropython
-----------

Uniform library that works on standard MicroPython platforms, including the EV3 and the Spike. See further platforms in the [microPython](MicroPython/README.md) directory.

Arduino
-------

The same UartRemote library is also implemented for `Arduino <https://github.com/antonvh/UartRemote/tree/master/Arduino/UartRemote>`_.


ESP32
-----

remote module loading via REPL [details here](/ibraries/UartRemote/MicroPython/ESP32/README.md)

LEGO SPIKE Prime and Robot Inventor 51515
-----------------------------------------

Copy the `installer <https://github.com/antonvh/UartRemote/blob/master/MicroPython/SPIKE/install_uartremote.py>`_ in an empty project inside the LEGO app and run the script once. You can discard the script afterwards. Alternativly you can use rshell, below. files in the /projects folder are not removed.

LEGO EV3
--------
Copy `uartremote.py` into your project directory or library directory for `uartremote import *`. this also is the same for using in python3 on desktopOS

ESP8266 with rshell
-------------------

on ESP82 Copy the `ESP8266 library <https://github.com/antonvh/UartRemote/blob/master/MicroPython/ESP8266>`_ to the board with webREPL or rshell.

Copy the plain .py file or the compiled library .mpy into your device
- You can get rshell via: `pip3 install rshell`
- If you have a *single device* this will connect: `rshell -p $(ls /dev/tty.usb*) -b 115200 --editor nano`
- ...otherwise find your device with: `ls /dev/tty.usb*` 
- use your *own* desired modem/serial: `rshell -p /dev/tty.usbserial-141230 -b 115200 --editor nano`
- Your device is now mounted in rshell> as /pyboard
- Use rshell's cp To copy the library >`cp Libraries/UartRemote/MicroPython/uartremote.py /pyboard/`

Alternativly: you can use some IDE's for GUI File managment, such as `ThonnyIDE <https://thonny.org>`_ (win/osx/raspi) or `Mu IDE <https://codewith.mu>`_ if you cannot use rshell command line.

You can edit ``/pyboard/boot.py`` while you're at it, to configure your `wifi connection <https://github.com/antonvh/LMS-uart-esp/wiki/Connecting-via-webrepl>`_ for LEGO/STM32 using a `breakout board <https://antonsmindstorms.com/?s=wifi>`_. 