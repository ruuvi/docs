---
description: 'Lifecycle: Beta. Last updated 2021-04-15'
---

# GW ESP32 Firmware

## First boot

On boot, ESP32 checks if there are settings configured in flash. If not, ESP32 will run series of selftests and report the selftest status as JSON through USB/UART converter onboard. Selftest is described in details on it's own [page](gw-esp32-selftest.md), most users can ignore the selftest. 

After selftest ESP32 doesn't wait for anything and it starts a [WiFi hotspot](gw-esp32-wifi-hotspot.md) for configuration. Once the gateway has valid configuration and internet connection, the hotspot is turned off. 

## Future boots

On future boots, the settings are loaded from flash and applied automatically. 



