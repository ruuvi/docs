---
description: 'Lifecycle: Beta. Page updated 2021-03-12'
---

# Ruuvi Firmware 3.30.X

## Test checklist

### Power-on

{% tabs %}
{% tab title="RuuviTag B+" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left">Action</th>
      <th style="text-align:left">How to test</th>
      <th style="text-align:left">Verified by</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Tag stays in bootloader mode / begins DFU if application commanded tag
        into DFU mode.</td>
      <td style="text-align:left">Manually, enter configuration mode by &quot;B&quot; and command tag into
        bootloader with nRF Connect</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag stays in bootloader mode if button &quot;B&quot; is pressed on boot.</td>
      <td
      style="text-align:left">Manually, hold down &quot;B&quot;, press and release &quot;R&quot;.</td>
        <td
        style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag initializes watchdog.</td>
      <td style="text-align:left">Unit test test_main.c</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag turns RED LED on for self-test duration.</td>
      <td style="text-align:left">Manually, visual check</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag runs self-tests to detect installed sensors.</td>
      <td style="text-align:left">Unit tests test_main.c test_app_sensor.c</td>
      <td style="text-align:left">
        <p></p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag erases settings stored to flash file system and reboots if flash file
        system cannot be initialized.</td>
      <td style="text-align:left">Unit test main.c, drivers/rt_flash.c</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag erases old log entries to prevent data with corrupted timestamps</td>
      <td
      style="text-align:left">Check app_log:app_log_init()</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag turns GREEN LED on for one second if no errors were detected in self-test
        phase. Missing sensors are allowed.</td>
      <td style="text-align:left">Manually, visual check.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data
        is allowed, but every packet must be valid. Initial dataformat is RAWv2.</td>
      <td
      style="text-align:left">Unit test test_app_heartbeat.c. Check power profile manually.</td>
        <td
        style="text-align:left"></td>
    </tr>
  </tbody>
</table>
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
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | Manually, enter configuration mode by "B" and command tag into bootloader with nRF Connect | Oleg / RC5 |
|  |  |  |
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
| Library tests: p2p, rms, variance, ringbuffer | Pass\* | |
| Peripheral tests: power, timer, scheduler, flash | Pass\* | |
| Sensor tests: BME280, LIS2DH12 | Pass\*\* | |
| BLE tests: Advertising, GATT | Pass |  |
| GATT Throughput, 1 MBit / s | 25 700 B / s | |
| GATT Throughput, 2 MBit / s | 20 800 B / s | |
| NFC Test | Pass | |
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

{% file src="../../../.gitbook/assets/3.29.3-integration\_test\_result.log" caption="3.29.3 Integration test log" %}

Note: \* First test didn't print all the RTT logs, verified separately \*\* LIS2DH12 interrupt test fails due to driver test problem, doesn't affect release. DUT includes SHTC3. 



### Button

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. | |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any.  | |
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
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. | |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT | Check the power profile after NFC read, connect with GATT | 3.29.3-RC1 does not pass, fast broadcast for 60 s or end of next connection. |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools | |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. | |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. | |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field | |
| "dt" field has binary content | Check "dt" field | |
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

{% file src="../../../.gitbook/assets/ruuvi-0233-201009-1208.csv" caption="Read log" %}

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Data is sent at 1285 ms interval by default. | Check power profile for TX spikes. | |
| Tag accepts GATT connection and starts pushing data through NUS TX characteristic notifications. | Connect to tag with nRF Connect, register to GATT notifications. | |
| GATT server has Device Information Service with Manufacturer Name String, Model Number String Hardware Revision String and Firmware revision String. Serial Number String is not viewable unless configuration mode is on. | Connect to tag with nRF Connect, check fields manually. | |
| Manufacturer Name String is "Ruuvi Innovations Ltd" | Manually | |
| Model Number String is "RuuviTag B" | Manually | |
| Serial Number String is viewable only in configuration mode and has the same ID as NFC scan. | Manually | |
| Hardware revision string has text "Check PCB" | Manually | |
| Firmware revision string has same version as NFC read | Manually | |
| Environmental history log can be read by sending "0x3A 3A 11 TIMESTAMP 00000000" to NUS RX characteristic. Timestamp is current time in seconds after Unix epoch, 4 bytes.  | Manually, or with Ruuvi Station sync graphs button. For the test a debug version of firmware should be used, tag must be running at least for 1 hour and there should be a data point each second for at least 1 hour. Entries do not have to be sorted by time, it is allowed to miss a sample roughly once per 10 seconds. | |
| Environmental log history will send only data that has timestamp after request | Sync once with Ruuvi Station, check there is data. Sync again, check there is less data loaded. | |
| Tag continues broadcasting data while connected by GATT. | Connect with one device, scan with other. Manually. Note: Some scanners will not report advertisements from connected devices, so 2 scanners are required. | |
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
| Firmware 2.5.9 can be updated with SDK\_UPDATE package. | System tests in GitHub. | |
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub | Note: requires manual test due to no mechanism to enter configuration mode without interaction. |
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
| Broadcasting, connectable | 26 µA @ 3.6 V, 27 µA @ 3.0 V, 29  µA @ 2.4 V | |
|  | 26.9 µA @ 3.6 V,  27.5 µA @ 3.0 V, 30.4  µA @ 2.4 V | Oleg / 3.29.0-RC5 |
| Broadcasting, connected | 34 µA @ 3.6 V, 36 µA @ 3.0 V, 40  µA @ 2.4 V  | |
|  | 36.9 µA @ 3.6 V, 39.2 µA @ 3.0 V, 44.0 µA @ 2.4 V | Oleg / 3.29.0-RC5 |
| Transferring logs. | 8.9 mA @ 3.6 V, 9.7 mA @ 3.0 V, 10.9  mA @ 2.4 V | |
|  | 8.2 mA @ 3.6 V, 8.8 mA @ 3.0 V, 9.6 mA @ 2.4 V | Oleg / 3.29.0-RC5 |
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
| Broadcasting, connected |  |  |
| Transferring logs. |  |  |
{% endtab %}

{% tab title="\"Kalervo\"" %}
| State | Value | Verified by |
| :--- | :--- | :--- |
| Broadcasting, connectable |  |  |
| Broadcasting, connected |  |  |
| Transferring logs. |  |  |
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

