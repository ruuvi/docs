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
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect |  |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". |  |
| Tag initializes watchdog. | Check application initialization code |  |
| Tag turns RED LED on for self-test duration. | Manually, visual check |  |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c |  |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c |  |
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) |  |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. |  |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. |  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect |  |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". |  |
| Tag initializes watchdog. | Check application initialization code |  |
| Tag turns RED LED on for self-test duration. | Manually, visual check |  |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c |  |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c |  |
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) |  |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. |  |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect |  |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". |  |
| Tag initializes watchdog. | Unit test test\_main.c |  |
| Tag turns RED LED on for self-test duration. | Manually, visual check |  |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c |  |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c |  |
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) |  |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. |  |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. |  |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect |  |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". |  |
| Tag initializes watchdog. | Unit test test\_main.c |  |
| Tag turns RED LED on for self-test duration. | Manually, visual check |  |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c |  |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c |  |
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) |  |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. |  |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. |  |
{% endtab %}

{% tab title="RuuviTag B8+TMP117" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect | Nikita / Custom Firmware |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R". | Nikita / Custom Firmware |
| Tag initializes watchdog. | Unit test test\_main.c | Nikita / Custom Firmware |
| Tag turns RED LED on for self-test duration. | Manually, visual check | Fail |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c | Nikita / Custom Firmware |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c | Nikita / Flash Disabled |
| Tag erases old log entries to prevent data with corrupted timestamps | Check app\_log:app\_log\_init\(\) | Nikita / Flash Disabled |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. | Nikita / Custom Firmware |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. | Nikita / Custom Firmware |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Not Applicable |  |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Not applicable |  |
| Tag initializes watchdog. | Check application initialization code | Nikita / Custom Firmware |
| Tag turns RED LED on for self-test duration. | Manually, visual check | Fail |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c | Nikita / Custom Firmware |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Not Applicable. | |
| Tag erases old log entries to prevent data with corrupted timestamps | Not Applicable |  |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. | Nikita / Custom Firmware |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. | Nikita / Custom Firmware|
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
| Library tests: p2p, rms, variance, ringbuffer |  |  |
| Peripheral tests: power, timer, scheduler, flash |  |  |
| Sensor tests: BME280, LIS2DH12 |  |  |
| BLE tests: Advertising, GATT |  |  |
| GATT Throughput, 1 MBit / s |  |  |
| GATT Throughput, 2 MBit / s |  |  |
| NFC Test |  |  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Item | Result | Verified by |
| :--- | :--- | :--- |
| Library tests: p2p, rms, variance, ringbuffer |  |  |
| Peripheral tests: power, timer, scheduler, flash |  |  |
| Sensor tests: SHTCX, BME280, LIS2DH12 |  |  |
| BLE tests: Advertising, GATT |  |  |
| GATT Throughput, 1 MBit / s |  |  |
| GATT Throughput, 2 MBit / s |  |  |
| NFC Test |  |  |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Item | Result | Verified by |
| :--- | :--- | :--- |
| Library tests: p2p, rms, variance, ringbuffer |  |  |
| Peripheral tests: power, timer, scheduler, flash |  |  |
| Sensor tests: DPS310, SHTCX, LIS2DH12 nRF52 |  |  |
| BLE tests: Advertising, GATT |  |  |
| GATT Throughput, 1 MBit / s |  |  |
| GATT Throughput, 2 MBit / s |  |  |
| NFC Test |  |  |
{% endtab %}

{% tab title="RuuviTag B8+TMP117" %}
| Item | Result | Verified by |
| :--- | :--- | :--- |
| Library tests: p2p, rms, variance, ringbuffer | Pass | Nikita / Custom Firmware |
| Peripheral tests: power, timer, scheduler | Pass | Nikita / Custom Firmware |
| Sensor tests: TMP117, DPS310, DPS310, LIS2DH12, nRF52 | Pass | Nikita / Custom Firmware |
| BLE tests: Advertising, GATT | Disabled | Nikita / Custom Firmware |
| GATT Throughput, 1 MBit / s | Disabled | Nikita / Custom Firmware |
| GATT Throughput, 2 MBit / s | Disabled | Nikita / Custom Firmware |
| NFC Test | Disabled | Nikita / Custom Firmware |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Item | Result | Verified by |
| :--- | :--- | :--- |
| Not Applicable |  |  |
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

\* TMP117 has a race condition in single sample, nRF52 fails configuration integration test, LIS2DH12 fails interrupt test

### Button

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. | |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any. | |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. |  |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any. |  |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. |  |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any. |  |
{% endtab %}

{% tab title="RuuviTag B8+TMP117" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. | Nikita / GATT Disabled |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any. | Nikita / Flash Disabled  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Not Applicable |  |  |
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
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. |  |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT | Check the power profile after NFC read, connect with GATT |  |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools |  |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. |  |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. |  |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field |  |
| "dt" field has binary content | Check "dt" field |  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. |  |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT | Check the power profile after NFC read, connect with GATT |  |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools |  |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. |  |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. |  |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field |  |
| "dt" field has binary content | Check "dt" field |  |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. | Nikita / NFC Disabled |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT | Check the power profile after NFC read, connect with GATT | Nikita / NFC Disabled |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools | Nikita / NFC Disabled |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. | Nikita / NFC Disabled |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. | Nikita / NFC Disabled |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field | Nikita / NFC Disabled |
| "dt" field has binary content | Check "dt" field | Nikita / NFC Disabled |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Not Applicable |  |  |
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
| Data is sent at 1285 ms interval by default. | Check power profile for TX spikes. |  |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications. | Connect to tag with nRF Connect, register to GATT notifications. |  |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually. |  |
| Manufacturer Name String is "Ruuvi Innovations Ltd" | Manually |  |
| Model Number String is "RuuviTag B" | Manually |  |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan. | Manually |  |
| Hardware revision string has text "Check PCB" | Manually |  |
| Firmware revision string has same version as NFC read | Manually |  |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes. | Manually, or with Ruuvi Station sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 1 hour and there should be a data point each second for at least 1 hour. Entries do not have to be sorted by time, it is allowed to miss a sample roughly once per 10 seconds. |  |
| Environmental log history will send only data that has timestamp after request | Sync once with Ruuvi Station, check there is data. Sync again, check there is less data loaded. |  |
| Tag continues broadcasting data while connected by GATT. | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required. |  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Data is sent at 1285 ms interval by default. | Check power profile for TX spikes. |  |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications. | Connect to tag with nRF Connect, register to GATT notifications. |  |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually. |  |
| Manufacturer Name String is "Ruuvi Innovations Ltd" | Manually |  |
| Model Number String is "RuuviTag B" | Manually |  |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan. | Manually |  |
| Hardware revision string has text "Check PCB" | Manually |  |
| Firmware revision string has same version as NFC read | Manually |  |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes. | Manually, or with Ruuvi Station sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 1 hour and there should be a data point each second for at least 1 hour. Entries do not have to be sorted by time, it is allowed to miss a sample roughly once per 10 seconds. |  |
| Environmental log history will send only data that has timestamp after request | Sync once with Ruuvi Station, check there is data. Sync again, check there is less data loaded. |  |
| Tag continues broadcasting data while connected by GATT. | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required. |  |
{% endtab %}

{% tab title="RuuviTag B8" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Data is sent at 9900 ms interval by default. | Check power profile for TX spikes. | Nikita / Custom Firmware |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications. | Connect to tag with nRF Connect, register to GATT notifications. | Nikita / GATT Disabled |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually. | Nikita / GATT Disabled |
| Manufacturer Name String is "Ruuvi Innovations Ltd" | Manually | Nikita / Custom Firmware |
| Model Number String is "RuuviTag B" | Manually | Nikita / GATT Disabled |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan. | Manually | Nikita / GATT Disabled |
| Hardware revision string has text "Check PCB" | Manually | Nikita / GATT Disabled |
| Firmware revision string has same version as NFC read | Manually | Nikita / GATT Disabled |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes. | Manually, or with Ruuvi Station sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 1 hour and there should be a data point each second for at least 1 hour. Entries do not have to be sorted by time, it is allowed to miss a sample roughly once per 10 seconds. | Nikita / GATT Disabled |
| Environmental log history will send only data that has timestamp after request | Sync once with Ruuvi Station, check there is data. Sync again, check there is less data loaded. | Nikita / GATT Disabled |
| Tag continues broadcasting data while connected by GATT. | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required. | Nikita / GATT Disabled |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Data is sent at 9900 ms interval by default. | Check power profile for TX spikes. | Nikita / Custom Firmware |
| GATT tests are not applicable. |  |  |
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
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub | Note: requires manual test due to no mechanism to enter configuration mode without interaction.  |
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

{% tab title="RuuviTag B8+TMP117" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Firmware 2.5.9 can be updated with SDK\_UPDATE package. | System tests in GitHub. |  |
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub | Note: requires manual test due to no mechanism to enter configuration mode without interaction. |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Not Applicable |  |  |
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
| Broadcasting, connectable |  |  |
|  |  |  |
| Broadcasting, connected |  |  |
|  |  |  |
| Transferring logs. |  |  |
|  |  |  |
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
| Broadcasting, connectable |  |  |
|  |  |  |
| Broadcasting, connected |  |  |
|  |  |  |
| Transferring logs. |  |  |
|  |  |  |
{% endtab %}

{% tab title="RuuviTag B8" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, connectable, default |  |  |
| Broadcasting, connectable, longlife |  |  |
{% endtab %}

{% tab title="RuuviTag B8+TMP117" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, nonconnectable, default | 26.5 µA @ 3.6 V, 25.6 µA @ 3.0 V, 25.5 µA @ 2.4 V | Nikita / Custom Firmware |
| Broadcasting, connectable, longlife |  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, default | 8.9 µA @ 3.6 V, 8.3 µA @ 3.0 V, 8.2 uA µA @ 2.4 V | Nikita / Custom Firmware |
| Broadcasting, longlife |  |  |
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

