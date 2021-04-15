---
description: 'Lifecycle: Alpha. Last updated 2021-04-15'
---

# GW nRF52811 selftest

The nRF52811 on Ruuvi GW will run a self-test at boot to verify it is operational. The self-test will check that data can be received over Bluetooth and communication with ESP32 is working.

To test communication with the ESP32, nRF52 will query for scan parameters from ESP32 and wait for reply. Once scan parameters have been received, nRF52 will start scanning and if a matching advertisement has been received, the green LED will be turned on.

The green led will stay on as long as advertisements are received, if no new advertisements have been received within few scan cycles the watchdog will reboot the nRF52 which will query for scan parameters again and turn on the green led once a matching advertisement is received. 



