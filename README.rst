**************
Mopidy-dam1021
**************

`Mopidy <http://www.mopidy.com/>`_ extension for controlling volume using a `dam1021 DAC <http://soekris.dk/dam1021.html>`_ device. 


Installation
============

Install by running::

    sudo pip install Mopidy-dam1021



Configuration
=============

The Mopidy-dam1021 extension is enabled by default. To disable it, add the following to ``mopidy.conf``::

    [dam1021]
    enabled = false

The dam1021 DAC must be connected to a serial port of the machine running Mopidy. This does not meant the both devices must be physically connected together using a serial cable. Although this is the most obvious configuration. Another option is to use network tunneling using `socat <http://www.dest-unreach.org/socat/>`_ or any other similar utility. Bear in mind system user on behalf of which Mopidy operates on must have proper access rights to a serial port. E.g. the following needs to be done on Raspian::

  # usermod -G dialout mopidy

To use the DAC to control volume, set the ``audio/mixer`` config
value in ``mopidy.conf`` to ``dam1021mixer``. You probably should add some
properties to the ``dam1021`` config section too.

The following properties are available:

- ``serial``: The serial device to use, defaults to ``/dev/ttyAMA0``. This must be set correctly for the mixer to work.

- ``volume_inf``: The DAC volume control utilizes idea of signal attenuation in a digital domain, where ``0`` means unaltered signal, ``-80`` - maximal attenuation, ``10`` - maximal gain. This property defines lower bound of volume levels available to the mixer. Usually you should operate between ``-80`` and ``0``. Using narrower margins translates to a finer volume control. Defaults to ``-80``. 

- ``volume_sup``: The upper bound of volume levels available to the mixer. See ``volume_inf``. Defaults to ``0``. 

- ``timeout``: Timeout value for any given operation on serial line, used by a lower level library. Expressed in milliseconds. Defaults to 2000.


Configuration example with all default values, suitable for Raspberry Pi users::

    [audio]
    mixer = dam1021mixer

Configuration example, if the DAC is available elsewhere::

    [audio]
    mixer = dam1021mixer

    [dam1021]
    port = /dev/ttyUSB0

Configuration example with a customized volume level range::

    [audio]
    mixer = dam1021mixer

    [dam1021]
    port = /dev/ttyUSB0
    volume_inf = -45
    volume_sup = -5

Bugs
====

Please use issue tracker for reporting.


Additional resources
====================

- `Source code <https://github.com/fortaa/mopidy-dam1021>`_
- `Dam1021 communication library <https://github.com/fortaa/dam1021>`_
- `Official DAC page <http://soekris.dk/dam1021.html>`_

