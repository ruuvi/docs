---
description: 'Lifecycle: Beta. Page updated 2021-03-25'
---

# Ruuvi Firmware 3.30.X

## Test checklist

### Power-on

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect | Nikita / v3.30-RC6 |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". | Nikita / v3.30-RC6 |
| Tag initializes watchdog. | Check application initialization code |  |
| Tag turns RED LED on for self-test duration. | Manually, visual check | Nikita / v3.30-RC6 |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c | Nikita / v3.30-RC6 |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c | Nikita / v3.30-RC6 |
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) | Nikita / v3.30-RC6 |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. | Nikita / v3.30-RC6 |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. | Nikita / v3.30-RC6 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect | Nikita / v3.30-RC6 (B+)|
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". | Nikita / v3.30-RC6 (B+)|
| Tag initializes watchdog. | Check application initialization code | Nikita / v3.30-RC6 (B+)|
| Tag turns RED LED on for self-test duration. | Manually, visual check | Nikita / v3.30-RC6 (B+)|
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c | Nikita / v3.30-RC6 (B+)|
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c | Nikita / v3.30-RC6 (B+)|
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) | Nikita / v3.30-RC6 (B+)|
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. | Nikita / v3.30-RC6 (B+)|
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. | Nikita / v3.30-RC6 (B+)|
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action  | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect | Tested on B+ |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". | Tested on B+ |
| Tag initializes watchdog. | Unit test test\_main.c | Tested on B+ |
| Tag turns RED LED on for self-test duration. | Manually, visual check | Tested on B+ |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c | Tested on B+ |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c | Tested on B+ |
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) | Tested on B+ |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. | Tested on B+ |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. | Tested on B+ |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action  | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect | Tested on B+ |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". | Tested on B+ |
| Tag initializes watchdog. | Unit test test\_main.c | Tested on B+ |
| Tag turns RED LED on for self-test duration. | Manually, visual check | Tested on B+ |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c | Tested on B+ |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c | Tested on B+ |
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) | Tested on B+ |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. | Tested on B+ |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. | Tested on B+ |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Not Applicable | |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Not applicable | |
| Tag initializes watchdog. | Check application initialization code | Nikita / v3.30-RC6 |
| Tag turns RED LED on for self-test duration. | Manually, visual check | Nikita / v3.30-RC6 |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c | Nikita / v3.30-RC6 |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Not Applicable. | |
| Tag erases old log entries to prevent data with corrupted timestamps | Not Applicable | |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. | Otso / v3.30-RC7 (B+)|
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. | Otso / v3.30-RC7 |
{% endtab %}

{% tab title="\"Kaarle\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Keijo\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}
{% endtabs %}

### Integration test

Integration tests are run on debug-variants of firmware. They print test results on RTT terminal as JSON. One nRF52 devkit is programmed with `nus_throughput_sdapp.hex` and rebooted before test. The devkit will connect to device under test to run the throughput values. RF signal quality is important for the throughput tests, so boards must not be touched during the BLE throughput test. NFC test is run by copying the NFC tag back to itself with a reader app, for example NFC Tools.

{% tabs %}
{% tab title="RuuviTag B+" %}
| Item | Result | Verified by |
| :--- | :--- | :--- |
| Library tests: p2p, rms, variance, ringbuffer | Pass | Nikita / v3.30-RC6 |
| Peripheral tests: power, timer, scheduler, flash | Pass | Nikita / v3.30-RC6 |
| Sensor tests: BME280, LIS2DH12 | Pass | Nikita / v3.30-RC6 |
| BLE tests: Advertising, GATT | Pass | Nikita / v3.30-RC6 |
| GATT Throughput, 1 MBit / s | 27 500 B / s | Nikita / v3.30-RC6 |
| GATT Throughput, 2 MBit / s | 37 300 B / s | Nikita / v3.30-RC6 |
| NFC Test | Pass | Nikita / v3.30-RC6 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Item | Result | Verified by |
| :--- | :--- | :--- |
| Library tests: p2p, rms, variance, ringbuffer | Pass | Tested on B+ |
| Peripheral tests: power, timer, scheduler, flash | Pass | Tested on B+ |
| Sensor tests: SHTCX, BME280, LIS2DH12 | Pass | Nikita / v3.30-RC6 |
| BLE tests: Advertising, GATT | Pass | Tested on B+ |
| GATT Throughput, 1 MBit / s | 27 400 B/s | Nikita / v3.30-RC6 |
| GATT Throughput, 2 MBit / s | 37 300 B/s | Nikita / v3.30-RC6 |
| NFC Test | Tested on B+ | Tested on B+ |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Item | Result | Verified by |
| :--- | :--- | :--- |
| Library tests: p2p, rms, variance, ringbuffer |  | |
| Peripheral tests: power, timer, scheduler, flash |  | |
| Sensor tests: DPS310, SHTCX, LIS2DH12 nRF52 |  |  |
| BLE tests: Advertising, GATT |  | |
| GATT Throughput, 1 MBit / s | | |
| GATT Throughput, 2 MBit / s | | |
| NFC Test |  | |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Item | Result | Verified by |
| :--- | :--- | :--- |
|  Not Applicable |  |
{% endtab %}

{% tab title="\"Kaarle\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Keijo\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}
{% endtabs %}

### Button

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. | Nikita / v3.30-RC6 |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any. | Nikita / v3.30-RC6 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. | Tested on B+ |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any. | Tested on B+ |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. |  |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any. | |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
|  Not Applicable |  |
{% endtab %}

{% tab title="\"Kaarle\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Keijo\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}
{% endtabs %}

### NFC

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. | Nikita / v3.30-RC6 |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT | Check the power profile after NFC read, connect with GATT | Nikita / v3.30-RC6 |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools | Nikita / v3.30-RC6 |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. | Nikita / v3.30-RC6 |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. | Nikita / v3.30-RC6 |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field | Nikita / v3.30-RC6 |
| "dt" field has binary content | Check "dt" field | Nikita / v3.30-RC6 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. | Tested on B+ |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT | Check the power profile after NFC read, connect with GATT | Tested on B+ |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools | Tested on B+ |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. | Tested on B+ |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. | Tested on B+ |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field | Tested on B+ |
| "dt" field has binary content | Check "dt" field | Tested on B+ |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. | Tested on B+ |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT | Check the power profile after NFC read, connect with GATT | Tested on B+ |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools | Tested on B+ |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. | Tested on B+ |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. | Tested on B+ |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field | Tested on B+ |
| "dt" field has binary content | Check "dt" field | Tested on B+ |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
|  Not Applicable |  |
{% endtab %}

{% tab title="\"Kaarle\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Keijo\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}
{% endtabs %}

### Usage

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Data is sent at 1285 ms interval by default. | Check power profile for TX spikes. | Nikita / v3.30-RC6 |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications. | Connect to tag with nRF Connect, register to GATT notifications. | Nikita / v3.30-RC6 |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually. | Nikita / v3.30-RC6 |
| Manufacturer Name String is "Ruuvi Innovations Ltd" | Manually | Nikita / v3.30-RC6 |
| Model Number String is "RuuviTag B" | Manually | Nikita / v3.30-RC6 |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan. | Manually | Nikita / v3.30-RC6 |
| Hardware revision string has text "Check PCB" | Manually | Nikita / v3.30-RC6 |
| Firmware revision string has same version as NFC read | Manually | Nikita / v3.30-RC6 |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes. | Manually, or with Ruuvi Station sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 1 hour and there should be a data point each second for at least 1 hour. Entries do not have to be sorted by time, it is allowed to miss a sample roughly once per 10 seconds. |  |
| Environmental log history will send only data that has timestamp after request | Sync once with Ruuvi Station, check there is data. Sync again, check there is less data loaded. | Nikita / v3.30-RC6 |
| Tag continues broadcasting data while connected by GATT. | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required. | Nikita / v3.30-RC6 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Data is sent at 1285 ms interval by default. | Check power profile for TX spikes. | Tested on B+ |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications. | Connect to tag with nRF Connect, register to GATT notifications. | Tested on B+ |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually. | Tested on B+ |
| Manufacturer Name String is "Ruuvi Innovations Ltd" | Manually | Tested on B+ |
| Model Number String is "RuuviTag B" | Manually | Tested on B+ |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan. | Manually | Tested on B+ |
| Hardware revision string has text "Check PCB" | Manually | Tested on B+ |
| Firmware revision string has same version as NFC read | Manually | Tested on B+ |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes. | Manually, or with Ruuvi Station sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 1 hour and there should be a data point each second for at least 1 hour. Entries do not have to be sorted by time, it is allowed to miss a sample roughly once per 10 seconds. | Tested on B+ |
| Environmental log history will send only data that has timestamp after request | Sync once with Ruuvi Station, check there is data. Sync again, check there is less data loaded. | Tested on B+ |
| Tag continues broadcasting data while connected by GATT. | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required. | Tested on B+ |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Data is sent at 1285 ms interval by default. | Check power profile for TX spikes. | Tested on B+ |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications. | Connect to tag with nRF Connect, register to GATT notifications. | Tested on B+ |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually. | Tested on B+ |
| Manufacturer Name String is "Ruuvi Innovations Ltd" | Manually | Tested on B+ |
| Model Number String is "RuuviTag B" | Manually | Tested on B+ |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan. | Manually | Tested on B+ |
| Hardware revision string has text "Check PCB" | Manually | Tested on B+ |
| Firmware revision string has same version as NFC read | Manually | Tested on B+ |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes. | Manually, or with Ruuvi Station sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 1 hour and there should be a data point each second for at least 1 hour. Entries do not have to be sorted by time, it is allowed to miss a sample roughly once per 10 seconds. | Tested on B+ |
| Environmental log history will send only data that has timestamp after request | Sync once with Ruuvi Station, check there is data. Sync again, check there is less data loaded. | Tested on B+ |
| Tag continues broadcasting data while connected by GATT. | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required. | Tested on B+ |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Data is sent at 1285 ms interval by default. | Check power profile for TX spikes. | Otso / 3.30-RC7 |
| GATT tests are not applicable. | | |
{% endtab %}

{% tab title="\"Kaarle\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Keijo\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}
{% endtabs %}

### Firmware updates

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Firmware 2.5.9 can be updated with SDK\_UPDATE package. | System tests in GitHub. |  |
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub | Note: requires manual test due to no mechanism to enter configuration mode without interaction. |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Firmware 2.5.9 can be updated with SDK\_UPDATE package. | System tests in GitHub. |  |
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub | Note: requires manual test due to no mechanism to enter configuration mode without interaction. |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Firmware 2.5.9 can be updated with SDK\_UPDATE package. | System tests in GitHub. |  |
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub | Note: requires manual test due to no mechanism to enter configuration mode without interaction. |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
|  Not Applicable |  |
{% endtab %}

{% tab title="\"Kaarle\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Keijo\"" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}
{% endtabs %}

### Power consumption

Power consumption is tested with Nordic Power Profiler kit at 2.4, 3.0 and 3.6 V voltages.

{% tabs %}
{% tab title="RuuviTag B+" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, connectable | 26 µA @ 3.6 V, 25 µA @ 3.0 V, 25 µA @ 2.4 V | Nikita / v3.30-RC6 |
|  | 24.5 µA @ 3.6 V, 26 µA @ 3.0 V, 28.1  µA @ 2.4 V | Nikita / v3.30-RC7 |
| Broadcasting, connected | 34 µA @ 3.6 V, 34 µA @ 3.0 V, 40 µA @ 2.4 V | Nikita / v3.30-RC6 |
|  | 36.7 µA @ 3.6 V, 35.7 µA @ 3.0 V, 40.3  µA @ 2.4 V | Nikita / v3.30-RC7 |
| Transferring logs. | 10 mA @ 3.6 V, 10.7 mA @ 3.0 V, 14.3 mA @ 2.4 V | Nikita / v3.30-RC6 |
|  | 9.6 mA @ 3.6 V, 10.9 mA @ 3.0 V, 15.5  mA @ 2.4 V | Nikita / v3.30-RC7 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, connectable |  |  |
| Broadcasting, connected |  |  |
| Transferring logs. |  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, connectable | 25 µA @ 3.6 V, 28 µA @ 3.0 V, 32 µA @ 2.4 V | Nikita / v3.30-RC6 |
|  | 28.3 µA @ 3.6 V, 28.3 µA @ 3.0 V, 31.6 µA @ 2.4 V | Nikita / v3.30-RC7 |
| Broadcasting, connected | 35 µA @ 3.6 V, 36 µA @ 3.0 V, 42 µA @ 2.4 V | Nikita / v3.30-RC6 |
|  | 36.2 µA @ 3.6 V, 39.3 µA @ 3.0 V, 44.7 µA @ 2.4 V | Nikita / v3.30-RC7 |
| Transferring logs. | 10.5 mA @ 3.6 V, 12.5 mA @ 3.0 V, 15.4 mA @ 2.4 V | Nikita / v3.30-RC6 |
|  | 10.5 mA @ 3.6 V, 12.4 mA @ 3.0 V, 15.3 mA @ 2.4 V | Nikita / v3.30-RC7 |
{% endtab %}

{% tab title="RuuviTag B8" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, connectable, default  | 31 µA @ 3.6 V, 33 µA @ 3.0 V, 34 uA µA @ 2.4 V | Otso / 3.30-RC7 |
| Broadcasting, connectable, longlife | 14 µA @ 3.6 V, 13 µA @ 3.0 V, 13 uA µA @ 2.4 V | Otso / 3.30-RC7 |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, default  | 38 µA @ 3.6 V, 42 µA @ 3.0 V, 47 uA µA @ 2.4 V | Otso / 3.30-RC7 |
| Broadcasting, longlife | 12 µA @ 3.6 V, 13 µA @ 3.0 V, 14 uA µA @ 2.4 V | Otso / 3.30-RC7 |
{% endtab %}

{% tab title="\"Kaarle\"" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, connectable |  |  |
| Broadcasting, connected |  |  |
| Transferring logs. |  |  |
{% endtab %}

{% tab title="\"Keijo\"" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, connectable |  |  |
| Broadcasting, connected |  |  |
| Transferring logs. |  |  |
{% endtab %}
{% endtabs %}

