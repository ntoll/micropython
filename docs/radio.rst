Radio
*****

.. py:module:: radio

The ``radio`` module allows devices to work together via simple wireless
networks.

Functions
=========

.. py:function:: send(message)

    Sends a message, expressed as a string.

.. py:function:: receive()

    Receive the next incoming message on the message queue. Returns ``None`` if
    there are no pending messages.

.. py:function:: config(length=32, queue=3, channel=7, power=0, address=b'uBit\x00', data_rate=radio.MODE_1MHZ)

    Configures the various settings relating to the radio. The specified
    default values are sensible.

    The ``length`` defines the size, in bytes, of a message sent via the radio.
    It can be up to 256 (????? CHECK THIS from memory) bytes long.

    The ``queue`` specifies the number of messages that can be stored on the
    incoming message queue.

    The ``channel`` can be an integer value between 0 and 100 (inclusive) that
    defines an arbitrary "channel" to which the radio is tuned. Messages will
    be sent via this channel and only messages received via this channel will
    be put onto the incoming message queue. Each step is 1MHz wide, based at
    2400MHz.

    The ``power`` is an integer value between 0 and 7 to indicate the strength
    of signal used when broadcasting a message. The higher the value the
    stronger the signal, but the more power is consumed by the device.

    The ``address`` is an arbitrary name, expressed as bytes, that's used to
    filter incoming packets at the hardware level, keeping only those that
    match the address you set. The default used by other micro:bit related
    platforms is ``b'uBit\x00'``.

    The ``data_rate`` indicates the speed at which transmission (???) takes
    place. Can be one of: MODE_1MHZ, MODE_???? and MODE_???.

    If ``config`` is not called then the defaults described above are assumed.
    Since these are named arguments with sane defaults, re-setting is as simple
    as calling ``config()``.

.. py:function:: on()

    Turns the radio on. This needs to be explicitly called since the radio
    draws power and takes up memory that you may otherwise need.

.. py:function:: off()

    Turns off the radio, thus saving power and memory.

Examples
--------

.. include:: ../examples/radio.py
    :code: python
