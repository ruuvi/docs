---
description: 'Lifecycle: Alpha. Page updated 2020-09-22'
---

# Ruuvi Firmware 3.29.0

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
      <td style="text-align:left">Otso / RC11 Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag stays in bootloader mode if button &quot;B&quot; is pressed on boot.</td>
      <td
      style="text-align:left">Manually, hold down &quot;B&quot;, press and release &quot;R&quot;, release
        &quot;R&quot;.</td>
        <td style="text-align:left">
          <p>Otso / RC11</p>
          <p>Oleg / RC5</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag initializes watchdog.</td>
      <td style="text-align:left">Unit test test_main.c</td>
      <td style="text-align:left">
        <p>Otso / RC10</p>
        <p>Oleg / RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag turns RED LED on for self-test duration.</td>
      <td style="text-align:left">Manually, visual check</td>
      <td style="text-align:left">
        <p>Otso / RC11 Oleg /</p>
        <p>RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag runs self-tests to detect installed sensors.</td>
      <td style="text-align:left">Unit tests test_main.c test_app_sensor.c</td>
      <td style="text-align:left">
        <p>Otso /</p>
        <p>RC10</p>
        <p>Oleg / RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag erases settings stored to flash file system and reboots if flash file
        system cannot be initialized.</td>
      <td style="text-align:left">Unit test main.c, drivers/rt_flash.c</td>
      <td style="text-align:left">
        <p>Otso / RC10</p>
        <p>Oleg / RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag erases old log entries to prevent data with corrupted timestamps</td>
      <td
      style="text-align:left">Check app_log:app_log_init()</td>
        <td style="text-align:left">Otso / RC10 Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag turns GREEN LED on for one second if no errors were detected in self-test
        phase. Missing sensors are allowed.</td>
      <td style="text-align:left">Manually, visual check.</td>
      <td style="text-align:left">Otso / RC11 Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data
        is allowed, but every packet must be valid. Initial dataformat is RAWv2.</td>
      <td
      style="text-align:left">Unit test test_app_heartbeat.c. Check power profile manually.</td>
        <td
        style="text-align:left">Otso / RC11 Oleg / RC5</td>
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
| Action | How to test | Verified by |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
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
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. | Otso / RC11 Oleg / RC5 |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any.  | Otso / RC11 Oleg/ RC5 |
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
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. | Otso / RC11 .  Oleg / RC5 |
| Tag broadcasts at 100 ms interval for 60 seconds or until connected by GATT | Check the power profile after NFC read, connect with GATT | RC-11 does not pass, fast broadcast for 60 s or end of next connection. |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools | Otso / RC11 |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. | Otso / RC11           Oleg / RC5 |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. | Otso / RC11           Oleg / RC5 |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field | Otso / RC11          Oleg / RC5  |
| "dt" field has binary content | Check "dt" field | Otso / RC11  |
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
      <td style="text-align:left">Data is sent at 1285 ms interval by default.</td>
      <td style="text-align:left">Check power profile for TX spikes.</td>
      <td style="text-align:left">Otso / RC11 Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag accepts GATT connection and starts pushing data through NUS TX characteristic
        notifications.</td>
      <td style="text-align:left">Connect to tag with nRF Connect, register to GATT notifications.</td>
      <td
      style="text-align:left">
        <p>Otso / RC11</p>
        <p>Oleg / RC5</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">GATT server has Device Information Service with Manufacturer Name String,
        Model Number String Hardware Revision String and Firmware revision String.
        Serial Number String is not viewable unless configuration mode is on.</td>
      <td
      style="text-align:left">Connect to tag with nRF Connect, check fields manually.</td>
        <td style="text-align:left">Otso / RC11 Oleg/ RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Manufacturer Name String is &quot;Ruuvi Innovations Ltd&quot;</td>
      <td
      style="text-align:left">Manually</td>
        <td style="text-align:left">
          <p>Otso / RC11</p>
          <p>Oleg / RC5</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">Model Number String is &quot;RuuviTag B&quot;</td>
      <td style="text-align:left">Manually</td>
      <td style="text-align:left">
        <p>Otso / RC11</p>
        <p>Oleg / RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Serial Number String is viewable only in configuration mode and has the
        same ID as NFC scan.</td>
      <td style="text-align:left">Manually</td>
      <td style="text-align:left">Otso / RC11 Oleg/ RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Hardware revision string has text &quot;Check PCB&quot;</td>
      <td style="text-align:left">Manually</td>
      <td style="text-align:left">Otso / RC11 Oleg/ RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Firmware revision string has same version as NFC read</td>
      <td style="text-align:left">Manually</td>
      <td style="text-align:left">Otso / RC11 Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Environmental history log can be read by sending &quot;0x3A 3A 11 TIMESTAMP
        00000000&quot; to NUS RX characteristic. Timestamp is current time in seconds
        after Unix epoch, 4 bytes.</td>
      <td style="text-align:left">Manually, or with Ruuvi Station sync graphs button. For the test a debug
        version of firmware should be used, tag must be running at least for 1
        hour and there should be a data point each second for at least 1 hour.
        Entries do not have to be sorted by time, it is allowed to miss a sample
        roughly once per 10 seconds.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Environmental log history will send only data that has timestamp after
        request</td>
      <td style="text-align:left">Sync once with Ruuvi Station, check there is data. Sync again, check there
        is less data loaded.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag continues broadcasting data while connected by GATT.</td>
      <td style="text-align:left">Connect with one device, scan with other. Manually. Note: Some scanners
        will not report advertisements from connected devices, so 2 scanners are
        required.</td>
      <td style="text-align:left">Otso / RC11 Oleg/ RC5</td>
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
| Firmware 2.5.9 can be updated with SDK\_UPDATE package. | System tests in GitHub. | Otso / RC11 |
| Firmware can enter bootloader after update and another 3.x firmware can be flashed. | System tests in GitHub | RC11 requires manual test due to no mechanism to enter configuration mode without interaction. |
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
| Broadcasting, connectable | 28 µA @ 3.6 V, 29 µA @ 3.0 V, 33  µA @ 2.4 V | Otso / RC11 |
|  | 26.9 µA @ 3.6 V,  27.5 µA @ 3.0 V, 30.4  µA @ 2.4 V | Oleg / RC5 |
| Broadcasting, connected | 31 µA @ 3.6 V, 34 µA @ 3.0 V, 38  µA @ 2.4 V  | Otso / RC11 |
|  | 36.9 µA @ 3.6 V, 39.2 µA @ 3.0 V, 44.0 µA @ 2.4 V | Oleg / RC5 |
| Transferring logs. | 8.5 mA @ 3.6 V, 9.3 mA @ 3.0 V, 10.7  mA @ 2.4 V | Otso / RC10 |
|  | 8.2 mA @ 3.6 V, 8.8 mA @ 3.0 V, 9.6 mA @ 2.4 V | Oleg / RC5 |
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

