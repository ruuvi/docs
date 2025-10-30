# Air Firmware Loader

The firmware loader is a self-contained minimal program which allows for receiving firmware update images over the air. The received images are stored in flash memory and after a reboot the second stage bootloader validates and installs the image.&#x20;

Generally the firmware loader should not be used in normal operation of Ruuvi Air, it is a backup option for recovery update in case a firmware update breaks the main application somehow.&#x20;

If both main application and firmware loader are broken, a factory reset can be executed by holding down button on Ruuvi Air for at least 15 seconds. After factory reset, the device is back to initial state and can receive the updates.&#x20;

The source code is available at [https://github.com/ruuvi/ruuvi.air.fw\_loader](https://github.com/ruuvi/ruuvi.air.fw_loader)

