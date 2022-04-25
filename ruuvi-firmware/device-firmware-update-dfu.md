---
description: 'Lifecycle: In production'
---

# Device Firmware Update (DFU)

There are two different options on how to update RuuviTag firmware.

### OTA (Over the Air)

### **Ruuvi firmware version 1.x, 2.x**&#x20;

Ruuvitag firmware version up until 2.x are built on top of Nordic SDK 12.3 / Softdevice s132 v3.1.1. The bootloader on these RuuviTags uses debug-mode which skips hardware and firmware version checks.&#x20;

The keyfile to sign the RuuviTag updates is published in [ruuvitag\_fw](https://github.com/ruuvi/ruuvitag\_fw/tree/master/keys) repository.

| Command to generate DFU package for RuuviTags up to firmware version 2                                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `nrfutil pkg generate --debug-mode --application _build/ruuvi_firmware.hex --hw-version 3 --sd-req 0x91 --key-file ~/git/ruuvitag_fw/keys/ruuvi_open_private.pem ruuvi_firmware_dfu.zip` |

To upload package to RuuviTag, press button "B" and tap "R" to reset  the tag. Bootloader checks if button "B" is pressed at boot and enters the bootloader mode.&#x20;

### **Ruuvi firmware version 3.x**&#x20;

Ruuvi firmware 3 builds on SDK15.3 and Softdevice s132 v6.1.1. There are special edition RuuviTags with nRF52811 that do not have bootloader at all due to size constraints.

The bootloader is a production version and it enforces version checks. On RuuviTag B1 ... B7.1 the hardware version is 0xB0, regardless of which sensors are installed.&#x20;

| Command to generate DFU package for RuuviTags with firmware version 3                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `nrfutil pkg generate --application _build/nrf52832_xxaa.hex --application-version 1 --hw-version 0xB0 --sd-req 0xB7 --key-file ruuvi_open_private.pem ${BINNAME}_dfu_app.zip` |

In bootloader mode the tag advertises itself with name "RuuviBoot"  and it provides [BLE DFU Service](https://infocenter.nordicsemi.com/topic/com.nordic.infocenter.sdk5.v12.3.0/group\_\_nrf\_\_ble\_\_dfu.html?cp=7\_5\_8\_6\_8\_4\_0). Nordic Semiconductor provides libraries for [iOS](https://github.com/NordicSemiconductor/IOS-Pods-DFU-Library) and [Android](https://github.com/NordicSemiconductor/Android-DFU-Library) to interface with the service.

### SWD (Serial Wire Debug)

If you're developing your own firmware or need to flash hunderds or more of RuuviTags, you should consider using a wired programmer for higher programming speed. To create your own hex image for flashing, you need 4 parts:

* Softdevice
* Bootloader
* Bootloader settings
* Application

The softdevice is given by Nordic Semiconductor or other company which provides the radio protocol.&#x20;

You can use Ruuvi's bootloader available at [https://github.com/ruuvi/ruuvi.nrf5\_sdk15\_bootloader.c](https://github.com/ruuvi/ruuvi.nrf5\_sdk15\_bootloader.c), but you should at least change the public key used for verifying the firmware images to ensure that you can keep the full control of your tags.&#x20;

Settings are generated with nrfutil, which is part of [Nordic Command Line Tools](https://www.nordicsemi.com/Software-and-tools/Development-Tools/nRF-Command-Line-Tools). You'll also need nrfjprog and mergehex from the command line tool package.

Application is the .hex file you have created.&#x20;

| Commands to generate application settings and merge them into one package                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `nrfutil settings generate --family NRF52 --application _build/nrf52832_xxaa.hex --application-version 1 --bootloader-version 1 --bl-settings-version 1 settings.hex` |
| `mergehex -m ../../../../nRF5_SDK_15.3.0_59ac345/components/softdevice/s132/hex/s132_nrf52_6.1.1_softdevice.hex $BOOTLOADER settings.hex -o sbc.hex`                  |
| `mergehex -m sbc.hex _build/nrf52832_xxaa.hex -o packet.hex`                                                                                                          |

| Commands to flash the package to RuuviTag |
| ----------------------------------------- |
| `nrfjprog --eraseall`                     |
| `nrfjprog --program packet.hex`           |
| `nrfjprog --reset`                        |

If your firmware is secret or you wish to avoid duplications by users, you should enable the read protection bit .

`nrfjprog -f nrf52 --rbp ALL`

If you have enabled the read protection, you must run `nrfjprog --recover` to use the programming interface again. This completely erases the tag.

**Always power cycle the tag after using a wired programmer. Otherwise the debug interface might remain active and consume excess current.**&#x20;
