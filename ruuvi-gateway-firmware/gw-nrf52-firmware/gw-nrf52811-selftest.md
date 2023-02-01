---
description: 'Lifecycle: Alpha. Last updated 2021-04-15'
---

# GW nRF52811 selftest

The nRF52811 on Ruuvi GW will run a self-test at boot to verify it is operational. The self-test will check that data can be received over Bluetooth and the communication with ESP32 is working.

To test communication with the ESP32, nRF52 will query for scan parameters from ESP32 and wait for a reply. Once scan parameters have been received, nRF52 will start scanning.

If no new advertisements have been received within a few scan cycles, the watchdog reboots the nRF52, which requests the scan parameters again.

