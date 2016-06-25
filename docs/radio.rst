Radio
*****

.. py:module:: radio

The ``radio`` module allows devices to work together via simple wireless
networks.

Functions
=========

.. py:function:: send(message)

    Sends a message, expressed as a string or bytes.

.. py:function:: recv_bytes()

    Receive the next incoming message on the message queue. Returns ``None`` if
    there are no pending messages. Messages are returned as bytes.

.. py:function:: receive(fail=False)

    Works in exactly the same way as ``recv_bytes`` but messages are expressed
    as strings. If the optional ``fail`` argument is ``True``, a ``ValueError``
    is raised if the incoming message cannot be converted to a string. If the
    ``fail`` argument is ``False`` (the default) such messages and associated
    exceptions are silently ignored.

.. py:function:: config(length=32, queue=3, channel=7, power=0, address=b'uBit\x00', data_rate=radio.RADIO_MODE_MODE_Nrf_1Mbit)

    Configures the various settings relating to the radio. The specified
    default values are sensible.

    The ``length`` defines the size, in bytes, of a message sent via the radio.
    It can be up to 256 (????? CHECK THIS from memory) bytes long.

    The ``queue`` specifies the number of messages that can be stored on the
    incoming message queue. If there are no spaces left on the queue for
    incoming messages, then the incoming message is dropped.

    The ``channel`` can be an integer value from 0 to 100 (inclusive) that
    defines an arbitrary "channel" to which the radio is tuned. Messages will
    be sent via this channel and only messages received via this channel will
    be put onto the incoming message queue. Each step is 1MHz wide, based at
    2400MHz.

    The ``power`` is an integer value from 0 to 7 (inclusive) to indicate the
    strength of signal used when broadcasting a message. The higher the value
    the stronger the signal, but the more power is consumed by the device.

    The ``address`` is an arbitrary name, expressed as bytes, that's used to
    filter incoming packets at the hardware level, keeping only those that
    match the address you set. The default used by other micro:bit related
    platforms is ``b'uBit\x00'``. It must be exactly 5 bytes in length.

    The ``data_rate`` indicates the speed at which transmission takes
    place. Can be one of: ``RADIO_MODE_MODE_Nrf_1Mbit``,
    ``RADIO_MODE_MODE_Nrf_2Mbit`` or ``RADIO_MODE_MODE_Nrf_250Kbit``.

    If ``config`` is not called then the defaults described above are assumed.
    Since these are named arguments with sane defaults, re-setting is as simple
    as calling ``config()``. Calling with a subset of the named arguments
    (for example, ``config(power=3)`` will cause all the other settings to
    default their values.

.. py:function:: on()

    Turns the radio on. This needs to be explicitly called since the radio
    draws power and takes up memory that you may otherwise need.

.. py:function:: off()

    Turns off the radio, thus saving power and memory.

Examples
--------

.. include:: ../examples/radio.py
    :code: python
