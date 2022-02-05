uartremote.py -- Robust comminiation over UART
=================================================

This class implements methods that help to set up robust communication between instances running MicroPython which are connected over a serial link.

This is a class used to communicate via REPL or some kind of RPC command loop with other devices over a UART interface.

Example of code running on the master::

    from machine import I2S
    from machine import Pin

    # ESP32
    sck_pin = Pin(14)   # Serial clock output
    ws_pin = Pin(13)    # Word clock output
    sd_pin = Pin(12)    # Serial data output

    or

    # PyBoards
    sck_pin = Pin("Y6")   # Serial clock output
    ws_pin = Pin("Y5")    # Word clock output
    sd_pin = Pin("Y8")    # Serial data output

    audio_out = I2S(2,
                    sck=sck_pin, ws=ws_pin, sd=sd_pin,
                    mode=I2S.TX,
                    bits=16,
                    format=I2S.MONO,
                    rate=44100,
                    ibuf=20000)

    audio_in = I2S(2,
                   sck=sck_pin, ws=ws_pin, sd=sd_pin,
                   mode=I2S.RX,
                   bits=32,
                   format=I2S.STEREO,
                   rate=22050,
                   ibuf=20000)

Example of code running on the slave::

    from machine import I2S
    from machine import Pin

    # ESP32
    sck_pin = Pin(14)   # Serial clock output
    ws_pin = Pin(13)    # Word clock output
    sd_pin = Pin(12)    # Serial data output

    or

    # PyBoards
    sck_pin = Pin("Y6")   # Serial clock output
    ws_pin = Pin("Y5")    # Word clock output
    sd_pin = Pin("Y8")    # Serial data output

Constructor
-----------

.. class:: UartRemote(port=0,baudrate=115200,timeout=1500,debug=False,rx_pin=18,tx_pin=19)

   Construct a UartRemote object on the port given by:

   - ``port`` identifies a port for using the UART.

   ``port`` is board specific:

     - SPIKE: port = : has one I2S bus with id=2.
     - ESP8266: port = 0.
     - ESP32: Use 1 for UART1.

   The followinf keyword-only parameters are supported:

     - ``sck`` is a pin object for the serial clock line
     - ``ws`` is a pin object for the word select line
     - ``sd`` is a pin object for the serial data line
     - ``mode`` specifies receive or transmit
     - ``bits`` specifies sample size (bits), 16 or 32
     - ``format`` specifies channel format, STEREO or MONO
     - ``rate`` specifies audio sampling rate (samples/s)
     - ``ibuf`` specifies internal buffer length (bytes)
   
     - ``port`` is the hardware uart port used to by `UartRemote` class
     - ``baudrate`` is the baudraste at which the UART communicates, defaults to 115200
     - ``timeout`` is the timeout (in ms) for waiting for data coming in on the UART, default to 1500
     - ``debug`` is a Bollean flag to generate debug output, default to False


     - ``rx_pin`` is the : The pin on which the UART will receive information, default to 18
     - ``tx_pin`` is the pin on which the UART will receive information, default to 19
    
   
Methods
-------

.. method:: I2S.init(sck, ...)

  see Constructor for argument descriptions

.. method:: I2S.deinit()

  Deinitialize the I2S bus

.. method::  I2S.readinto(buf)

  Read audio samples into the buffer specified by ``buf``.  ``buf`` must support the buffer protocol, such as bytearray or array.
  "buf" byte ordering is little-endian.  For Stereo format, left channel sample precedes right channel sample. For Mono format,
  the left channel sample data is used.
  Returns number of bytes read

.. method::  I2S.write(buf)

  Write audio samples contained in ``buf``. ``buf`` must support the buffer protocol, such as bytearray or array.
  "buf" byte ordering is little-endian.  For Stereo format, left channel sample precedes right channel sample. For Mono format,
  the sample data is written to both the right and left channels.
  Returns number of bytes written
