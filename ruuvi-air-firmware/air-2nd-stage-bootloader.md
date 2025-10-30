# Air 2nd Stage Bootloader

The Ruuvi Air second stage bootloader is based on [MCUboot](https://docs.mcuboot.com/) and it handles cryptographic security of installed firmware images as well as validates any updates to be installed.&#x20;

There are two slots for second stage bootloader, which allows for updating the second stage over the air without risking bricking the OTA update capablity. The first stage is responsible for selecting the instance to run.

The second stage bootloader is responsible for installing update to main application or firmware loading application as well as selecting which one to start.&#x20;

The source code is available at [https://github.com/ruuvi/ruuvi.air.mcuboot](https://github.com/ruuvi/ruuvi.air.mcuboot)

