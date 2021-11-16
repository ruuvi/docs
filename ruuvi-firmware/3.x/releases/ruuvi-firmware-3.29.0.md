---
description: 'Lifecycle: Beta. Page updated 2020-12-16'
---

# Ruuvi Firmware 3.29.X

## Test checklist

### Power-on

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action                                                                                                                                           | How to test                                                                                | Verified by                |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | -------------------------- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode.                                                            | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect | Otso / 3.29.3-RC1          |
| Tag stays in bootloader mode if button "B" is pressed on boot.                                                                                   | Manually, hold down "B", press and release "R".                                            | Otso / 3.29.3-RC1          |
| Tag initializes watchdog.                                                                                                                        | Unit test test\_main.c                                                                     | Otso / 3.29.0              |
| Tag turns RED LED on for self-test duration.                                                                                                     | Manually, visual check                                                                     | Otso / 3.29.3-RC1          |
| Tag runs self-tests to detect installed sensors.                                                                                                 | Unit tests test\_main.c test\_app\_sensor.c                                                | <p>Otso /</p><p>3.29.0</p> |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized.                                          | Unit test main.c, drivers/rt\_flash.c                                                      | Otso / 3.29.3-RC1          |
| Tag erases old log entries to prevent data with corrupted timestamps                                                                             | Check app\_log:app\_log\_init()                                                            | Otso / 3.29.3-RC1          |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed.                                | Manually, visual check.                                                                    | Otso / 3.29.3-RC1          |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually.                            | Otso / 3.29.3-RC1          |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kalervo"" %}
| Action                                                                                | How to test                                                                                | Verified by |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ----------- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect | Oleg / RC5  |
|                                                                                       |                                                                                            |             |
{% endtab %}

{% tab title=""Kaarle"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Keijo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}
{% endtabs %}

### Integration test

Integration tests are run on debug-variants of firmware. They print test results on RTT terminal as JSON. One nRF52 devkit is programmed with `nus_throughput_sdapp.hex` and rebooted before test. The devkit will connect to device under test to run the throughput values. RF signal quality is important for the throughput tests, so boards must not be touched during the BLE throughput test. NFC test is run by copying the NFC tag back to itself with a reader app, for example NFC Tools.

{% tabs %}
{% tab title="RuuviTag B+" %}
| Item                                             | Result       | Verified by       |
| ------------------------------------------------ | ------------ | ----------------- |
| Library tests: p2p, rms, variance, ringbuffer    | Pass\*       | Otso / 3.29.3-RC1 |
| Peripheral tests: power, timer, scheduler, flash | Pass\*       | Otso / 3.29.3-RC1 |
| Sensor tests: BME280, LIS2DH12                   | Pass\*\*     | Otso / 3.29.3-RC1 |
| BLE tests: Advertising, GATT                     | Pass         | Otso / 3.29.3-RC1 |
| GATT Throughput, 1 MBit / s                      | 25 700 B / s | Otso / 3.29.3-RC1 |
| GATT Throughput, 2 MBit / s                      | 20 800 B / s | Otso / 3.29.3-RC1 |
| NFC Test                                         | Pass         | Otso / 3.29.3-RC1 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kalervo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kaarle"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Keijo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}
{% endtabs %}

{% file src="../../../.gitbook/assets/3.29.3-integration_test_result.log" %}
3.29.3 Integration test log
{% endfile %}

Note: \* First test didn't print all the RTT logs, verified separately \*\* LIS2DH12 interrupt test fails due to driver test problem, doesn't affect release. DUT includes SHTC3.&#x20;



### Button

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action                                                        | How to test                                                                                                       | Verified by       |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ----------------- |
| Short press enters configuration mode.                        | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT.    | Otso / 3.29.3-RC1 |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any.  | Otso / 3.29.3-RC1 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kalervo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kaarle"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Keijo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}
{% endtabs %}

### NFC

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action                                                                                             | How to test                                                                                               | Verified by                                                                  |
| -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| NFC read enables configuration until next GATT connection or timeout.                              | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. | Otso / 3.29.3-RC1                                                            |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT                        | Check the power profile after NFC read, connect with GATT                                                 | 3.29.3-RC1 does not pass, fast broadcast for 60 s or end of next connection. |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order.                   | Read the tag with e.g. NFC Tools                                                                          | Otso / 3.29.3-RC1                                                            |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results.                                                      | Otso / 3.29.3-RC1                                                            |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes.               | Check "id" field, compare to serial number read over GATT.                                                | Otso / 3.29.3-RC1                                                            |
| "sw" field has text "SW: " and a firmware revision string.                                         | Check "sw" field                                                                                          | Otso / 3.29.3-RC1                                                            |
| "dt" field has binary content                                                                      | Check "dt" field                                                                                          | Otso / 3.29.3-RC1                                                            |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kalervo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kaarle"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Keijo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}
{% endtabs %}



### Usage

{% file src="../../../.gitbook/assets/ruuvi-0233-201009-1208.csv" %}
Read log
{% endfile %}

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action                                                                                                                                                                                                                     | How to test                                                                                                                                                                                                                                                                                                                  | Verified by        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| Data is sent at 1285 ms interval by default.                                                                                                                                                                               | Check power profile for TX spikes.                                                                                                                                                                                                                                                                                           | Otso / 3.29.3-RC1  |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications.                                                                                                                           | Connect to tag with nRF Connect, register to GATT notifications.                                                                                                                                                                                                                                                             | Otso / 3.29.3-RC1  |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually.                                                                                                                                                                                                                                                                      | Otso /  3.29.3-RC1 |
| Manufacturer Name String is "Ruuvi Innovations Ltd"                                                                                                                                                                        | Manually                                                                                                                                                                                                                                                                                                                     | Otso / 3.29.3-RC1  |
| Model Number String is "RuuviTag B"                                                                                                                                                                                        | Manually                                                                                                                                                                                                                                                                                                                     | Otso / 3.29.3-RC1  |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan.                                                                                                                               | Manually                                                                                                                                                                                                                                                                                                                     | Otso / 3.29.3-RC1  |
| Hardware revision string has text "Check PCB"                                                                                                                                                                              | Manually                                                                                                                                                                                                                                                                                                                     | Otso / 3.29.3-RC1  |
| Firmware revision string has same version as NFC read                                                                                                                                                                      | Manually                                                                                                                                                                                                                                                                                                                     | Otso / 3.29.3-RC1  |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes.                                                 | Manually, or with Ruuvi Station sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 1 hour and there should be a data point each second for at least 1 hour. Entries do not have to be sorted by time, it is allowed to miss a sample roughly once per 10 seconds. | Otso / 3.29.3-RC1  |
| Environmental log history will send only data that has timestamp after request                                                                                                                                             | Sync once with Ruuvi Station, check there is data. Sync again, check there is less data loaded.                                                                                                                                                                                                                              | Otso / 3.29.3-RC1  |
| Tag continues broadcasting data while connected by GATT.                                                                                                                                                                   | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required.                                                                                                                                                                   | Otso / 3.29.3-RC1  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kalervo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kaarle"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Keijo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}
{% endtabs %}

### Firmware updates

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action                                                                              | How to test             | Verified by                                                                                                       |
| ----------------------------------------------------------------------------------- | ----------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Firmware 2.5.9 can be updated with SDK\_UPDATE package.                             | System tests in GitHub. | Otso / 3.29.3-RC1                                                                                                 |
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub  | Otso / 3.29.3-RC1 Note: requires manual test due to no mechanism to enter configuration mode without interaction. |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kalervo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Kaarle"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}

{% tab title=""Keijo"" %}
|   |   |
| - | - |
|   |   |
{% endtab %}
{% endtabs %}

### Power consumption

Power consumption is tested with Nordic Power Profiler kit at 2.4, 3.0 and 3.6 V voltages.

{% tabs %}
{% tab title="RuuviTag B+" %}
| State                     | Value                                               | Verified by        |
| ------------------------- | --------------------------------------------------- | ------------------ |
| Broadcasting, connectable | 26 µA @ 3.6 V, 27 µA @ 3.0 V, 29  µA @ 2.4 V        | Otso / 3.29.3-RC1  |
|                           | 26.9 µA @ 3.6 V,  27.5 µA @ 3.0 V, 30.4  µA @ 2.4 V | Oleg / 3.29.0-RC5  |
| Broadcasting, connected   | 34 µA @ 3.6 V, 36 µA @ 3.0 V, 40  µA @ 2.4 V        | Otso /  3.29.3-RC1 |
|                           | 36.9 µA @ 3.6 V, 39.2 µA @ 3.0 V, 44.0 µA @ 2.4 V   | Oleg / 3.29.0-RC5  |
| Transferring logs.        | 8.9 mA @ 3.6 V, 9.7 mA @ 3.0 V, 10.9  mA @ 2.4 V    | Otso / 3.29.3-RC1  |
|                           | 8.2 mA @ 3.6 V, 8.8 mA @ 3.0 V, 9.6 mA @ 2.4 V      | Oleg / 3.29.0-RC5  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
| State                     | Value | Verified by |
| ------------------------- | ----- | ----------- |
| Broadcasting, connectable |       |             |
| Broadcasting, connected   |       |             |
| Transferring logs.        |       |             |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
| State                     | Value | Verified by |
| ------------------------- | ----- | ----------- |
| Broadcasting, connectable |       |             |
| Broadcasting, connected   |       |             |
| Transferring logs.        |       |             |
{% endtab %}

{% tab title=""Kalervo"" %}
| State                     | Value | Verified by |
| ------------------------- | ----- | ----------- |
| Broadcasting, connectable |       |             |
| Broadcasting, connected   |       |             |
| Transferring logs.        |       |             |
{% endtab %}

{% tab title=""Kaarle"" %}
| State                     | Value | Verified by |
| ------------------------- | ----- | ----------- |
| Broadcasting, connectable |       |             |
| Broadcasting, connected   |       |             |
| Transferring logs.        |       |             |
{% endtab %}

{% tab title=""Keijo"" %}
| State                     | Value | Verified by |
| ------------------------- | ----- | ----------- |
| Broadcasting, connectable |       |             |
| Broadcasting, connected   |       |             |
| Transferring logs.        |       |             |
{% endtab %}
{% endtabs %}
