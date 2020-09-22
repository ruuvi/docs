---
description: 'Lifecycle: Alpha. Page updated 2020-09-22'
---

# Ruuvi Firmware 3.29.0

## Test checklist

### Power-on

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | System test "DFU test" |  |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R", release "R". | Otso / RC3 |
| Tag initializes watchdog. | Unit test test\_main.c | Otso / RC3  |
| Tag turns RED LED on for self-test duration. | Manually, visual check | Otso / RC3 |
| Tag runs self-tests to detect installed sensors. | Unit tests test\_main.c test\_app\_sensor.c | Otso / RC3 |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | Unit test main.c, drivers/rt\_flash.c | Otso / RC3 |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. | RC3 does not pass: Green led always on, 500 ms  |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2. | Unit test test\_app\_heartbeat.c. Check power profile manually. | RC-3 does not pass: 380 ms \(also interval is 100 ms + delay 0 ... 10 ms\) |
| All data fields of advertisement are valid RAWv2 values. | Manually, check that Ruuvi Station Android displays temperature, humidity, pressure, acceleration, voltage. Check MAC address, TX power +4, and measurement sequence counter bytes with nRF Connect captured data. | Otso / RC3 |
| After reset GATT profile is in secure mode with no DFU service or serial number readable. | Connect to GATT after boot, verify that DFU service is not listed and DIS doesn't list Serial Number characteristic. | Otso / RC3 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
|  |  |
| :--- | :--- |
|  |  |
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

Integration tests are run on debug-variants of firmware. They print test results on RTT terminal as JSON.

{% tabs %}
{% tab title="RuuviTag B+" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
|  |  |
| :--- | :--- |
|  |  |
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
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. | Otso / RC3 |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any.  | RC3 Does not pass.  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
|  |  |
| :--- | :--- |
|  |  |
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
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and configure settings via GATT. Check that configuration fails on next connection. Check that configuration is diabled after timeout | Otso / RC3 |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools | Otso / RC3 |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. | Otso / RC3 |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field. | Otso / RC3 |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field | Otso / RC3 \(note: has -rc3\) |
| "dt" field has binary content | Check "dt" field. | Otso / RC3 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
|  |  |
| :--- | :--- |
|  |  |
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
| Data is sent at 1285 ms interval by default. | Check power profile for TX spikes. | Otso / RC3 |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications. | Connect to tag with nRF Connect, register to GATT notifications. | Otso / RC3 |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually. | Otso / RC3 |
| Manufacturer Name String is "Ruuvi Innovations Ltd" | Manually | Otso / RC3 |
| Model Number String is "RuuviTag B" | Manually | Otso / RC3 |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan. | Manually | Otso / RC3 |
| Hardware revision string has text "Check PCB" | Manually | Otso / RC3 |
| Firmware revision string has same version as NFC read | Manually | Otso / RC3 |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes. | Manually, or with Ruuvi Station iOS sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 2 and there should be data point for each second up to max number of samples. |  |
| Tag continues broadcasting data while connected by GATT. | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required. | Otso / RC3 |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
|  |  |
| :--- | :--- |
|  |  |
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
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub |  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
|  |  |
| :--- | :--- |
|  |  |
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
| Broadcasting, connected |  |  |
| Transferring logs. |  |  |
{% endtab %}

{% tab title="RuuviTag B Basic" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="RuuviTag B+SHTC" %}
|  |  |
| :--- | :--- |
|  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
|  |  |
| :--- | :--- |
|  |  |
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

