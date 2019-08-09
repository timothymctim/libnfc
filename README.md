Free/Libre Near Field Communication (NFC) library
=================================================
`libnfc` historical contributors:

* Copyright (C) 2009      Roel Verdult
* Copyright (C) 2009-2013 Romuald Conty
* Copyright (C) 2010-2012 Romain Tartière
* Copyright (C) 2010-2013 Philippe Teuwen
* Copyright (C) 2012-2013 Ludovic Rousseau

Additional contributors:
* See AUTHORS file

General Information
===================

This is a fork of the `libnfc` library that should work with the SCL3711 NFC reader/writer to write to cheap
UUID writable MIFARE Classic cards.
For more information about `libnfc` please see the original [repository](https://github.com/nfc-tools/libnfc).

Sources
=======

* https://github.com/nfc-tools/libnfc
* https://gist.github.com/alphazo/3303282
* http://nfc-tools.org/index.php/Libnfc

Installation
============

Make sure you’ve installed all dependencies to build `libnfc`.
For example, on Debian, run `sudo apt build-dep libnfc-bin`.

Build from source
-----------------

```
autoreconf -vis
./configure
make
```

Set udev rules
--------------

```
sudo cp contrib/udev/42-pn53x.rules /lib/udev/rules.d/
```

Blacklist `pn533`
-----------------
Since Linux kernel version 3.1, two kernel-modules must not be loaded in order
to use `libnfc`: "nfc" and "pn533".
To prevent kernel from loading automatically these modules, you can blacklist
them in a modprobe conf file. This file is provided within libnfc archive:

```
sudo cp contrib/linux/blacklist-libnfc.conf /etc/modprobe.d/blacklist-libnfc.conf
```

Usage
=====

```
./utils/nfc-list # check if the dongle can be found
./utils/nfc-mfclassic r a dump.mfd # dump the card
./utils/nfc-mfclassic w a dump.mfd # write the dumped file
```

Troubleshooting
===============

Binaries
--------
If the tools fail to work properly, try installing
[`libnfc`](https://packages.debian.org/search?keywords=libnfc) from the Debian repository for the tools that
don’t need to be patched (patching is only required to directly write to block `0x00`, containing the UUID).

SCL3711
-------
Libnfc cannot be used concurrently with the PCSC proprietary driver of SCL3711.
Two possible solutions:
* Either you don't install SCL3711 driver at all
* Or you stop the PCSC daemon when you want to use libnfc-based tools

Blacklist
---------
It might also be necessary to blacklist `pn533_usb`:

```
sudo modprobe -r pn533_usb
```

Proprietary Notes
=================

* FeliCa is s registered trademark of the Sony Corporation.
* MIFARE is a trademark of NXP Semiconductors.
* Jewel Topaz is a trademark of Innovision Research & Technology.
* All other trademarks are the property of their respective owners.
