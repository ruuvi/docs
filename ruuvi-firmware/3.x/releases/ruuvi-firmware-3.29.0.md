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
      <td style="text-align:left">Otso / Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag stays in bootloader mode if button &quot;B&quot; is pressed on boot.</td>
      <td
      style="text-align:left">Manually, hold down &quot;B&quot;, press and release &quot;R&quot;, release
        &quot;R&quot;.</td>
        <td style="text-align:left">
          <p>Otso /</p>
          <p>Oleg / RC5</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag initializes watchdog.</td>
      <td style="text-align:left">Unit test test_main.c</td>
      <td style="text-align:left">
        <p>Otso /</p>
        <p>Oleg / RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag turns RED LED on for self-test duration.</td>
      <td style="text-align:left">Manually, visual check</td>
      <td style="text-align:left">
        <p>Otso / Oleg /</p>
        <p>RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag runs self-tests to detect installed sensors.</td>
      <td style="text-align:left">Unit tests test_main.c test_app_sensor.c</td>
      <td style="text-align:left">
        <p>Otso /</p>
        <p>Oleg / RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag erases settings stored to flash file system and reboots if flash file
        system cannot be initialized.</td>
      <td style="text-align:left">Unit test main.c, drivers/rt_flash.c</td>
      <td style="text-align:left">
        <p>Otso /</p>
        <p>Oleg / /RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Tag erases old log entries to prevent data with corrupted timestamps</td>
      <td
      style="text-align:left">Check app_log:app_log_init()</td>
        <td style="text-align:left">Otso / Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag turns GREEN LED on for one second if no errors were detected in self-test
        phase. Missing sensors are allowed.</td>
      <td style="text-align:left">Manually, visual check.</td>
      <td style="text-align:left">Otso / Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data
        is allowed, but every packet must be valid. Initial dataformat is RAWv2.</td>
      <td
      style="text-align:left">Unit test test_app_heartbeat.c. Check power profile manually.</td>
        <td
        style="text-align:left">Oleg / RC5</td>
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

Integration tests are run on debug-variants of firmware. They print test results on RTT terminal as JSON.

{% file src="../../../.gitbook/assets/ruuvitag\_b\_armgcc\_ruuvifw\_test\_v3.29.0-rc5\_full.log" caption="First test" %}

{% file src="../../../.gitbook/assets/ruuvitag\_b\_armgcc\_ruuvifw\_test\_v3.29.0-rc5\_full\_2.log" caption="Second test" %}

{% file src="../../../.gitbook/assets/ruuvitag\_b\_armgcc\_ruuvifw\_test\_v3.29.0-rc5\_full\_3.log" caption="Third test" %}

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| First test | Flash debug firmware. Power on. Run JLinkRTTViewerExe. No throughput test. No NFC test. Test result in attach. | RC 5 does not pass with : "overflow\_fpu\_errors":"FPU OFC Error", "ruuvi\_nrf5\_sdk15\_log.c:68 WARNING: NULL", LIS2DH12: "interrupts":"fail", app\_heartbeat.c:113 WARNING: NO\_MEM |
| Second test | Flash debug firmware. Power on. Run JLinkRTTViewerExe. No throughput test. No NFC test. Test result in attach. | RC 5 does not pass with :"overflow\_fpu\_errors":"FPU OFC Error", variance:"nan\_"timeout", app\_heartbeat.c:113 WARNING: NO\_MEM |
| Third test | Flash debug firmware. Power on. Run JLinkRTTViewerExe. Throughput Android test. NFS iOS test. Test result in attach. | Throughput ble\_gatt\_1\_mbit pass: 3117.499 bps;  Throughput ble\_gatt\_2\_mbit pass\(not supported by Android\): 3140.704 bps; NFC read write failed. RC 5 does not pass with : "overflow\_fpu\_errors":"FPU OFC Error", "ruuvi\_nrf5\_sdk15\_log.c:68 WARNING: NULL", LIS2DH12: "interrupts":"fail", app\_heartbeat.c:113 WARNING: NO\_MEM |
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
| Short press enters configuration mode. | Press button "B", check that red led blinks and DFU service is available, serial number is readable over GATT. | Otso / Oleg / RC5 |
| Long press erases flash settings and logs, enters bootloader. | Hold button "B", check that tag enters bootloader. Try reading logs, check there's not a lot of elements if any.  | Otso / Oleg/ RC5 |
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
| NFC read enables configuration until next GATT connection or timeout. | Apply a NFC field and enter bootloader via GATT. Check that bootloader service is disabled after timeout. | Otso / Oleg / RC5 |
| NFC has 4 UTF-8 text fields: "ad", "id", "sw", "dt". Fields can be in any order. | Read the tag with e.g. NFC Tools | RC 5 does not pass, "dt"-&gt;"da" |
| "ad" field has text "MAC: " and upper-case, ':' separated MAC address, as reported by BLE scanner. | Check "ad" field and compare to BLE scanner results. | Otso / Oleg / RC5 |
| "id" field has text "ID: " and upper-case, ':' separated unique identifier, 8 bytes. | Check "id" field, compare to serial number read over GATT. | Otso / Oleg / RC5 |
| "sw" field has text "SW: " and a firmware revision string. | Check "sw" field | Otso / Oleg / RC5 \(note: has -rc5\) |
| "dt" field has binary content | Check "dt" field | RC5 does not pass "dt"-&gt;"da" |
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
      <td style="text-align:left">Otso / Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag accepts GATT connection and starts pushing data through NUS TX characteristic
        notifications.</td>
      <td style="text-align:left">Connect to tag with nRF Connect, register to GATT notifications.</td>
      <td
      style="text-align:left">
        <p>Otso /</p>
        <p>Oleg / RC5</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">GATT server has Device Information Service with Manufacturer Name String,
        Model Number String Hardware Revision String and Firmware revision String.
        Serial Number String is not viewable unless configuration mode is on.</td>
      <td
      style="text-align:left">Connect to tag with nRF Connect, check fields manually.</td>
        <td style="text-align:left">Otso / Oleg/ RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Manufacturer Name String is &quot;Ruuvi Innovations Ltd&quot;</td>
      <td
      style="text-align:left">Manually</td>
        <td style="text-align:left">
          <p>Otso /</p>
          <p>Oleg / RC5</p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left">Model Number String is &quot;RuuviTag B&quot;</td>
      <td style="text-align:left">Manually</td>
      <td style="text-align:left">
        <p>Otso /</p>
        <p>Oleg / RC5</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Serial Number String is viewable only in configuration mode and has the
        same ID as NFC scan.</td>
      <td style="text-align:left">Manually</td>
      <td style="text-align:left">Otso / Oleg/ RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Hardware revision string has text &quot;Check PCB&quot;</td>
      <td style="text-align:left">Manually</td>
      <td style="text-align:left">Otso / Oleg/ RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Firmware revision string has same version as NFC read</td>
      <td style="text-align:left">Manually</td>
      <td style="text-align:left">Otso / Oleg / RC5</td>
    </tr>
    <tr>
      <td style="text-align:left">Environmental history log can be read by sending &quot;0x3A 3A 11 TIMESTAMP
        00000000&quot; to NUS RX characteristic. Timestamp is current time in seconds
        after Unix epoch, 4 bytes. Read log file in attach.</td>
      <td style="text-align:left">Manually, or with Ruuvi Station iOS sync graphs button. For the test a
        debug version of firmware should be used, tag must be running at least
        for 20 minutes and there should be a data point each second for at least
        500 seconds. Entries do not have to be sorted by time.</td>
      <td style="text-align:left">RC 5 does not pass. Missing log every 10-11 seconds.</td>
    </tr>
    <tr>
      <td style="text-align:left">Tag continues broadcasting data while connected by GATT.</td>
      <td style="text-align:left">Connect with one device, scan with other. Manually. Note: Some scanners
        will not report advertisements from connected devices, so 2 scanners are
        required.</td>
      <td style="text-align:left">Otso / Oleg/ RC5</td>
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
| Firmware 2.5.9 can be updated with SDK\_UPDATE package. | System tests in GitHub. | Otso / RC5 |
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
| Broadcasting, connectable | 27 µA @ 3.6 V =&gt; 97 µW, 29 µA @ 3.0 V =&gt; 86 µW, 30  µA @ 2.4 V =&gt; 72 µW | Otso / RC5 |
|  | 26.9 µA @ 3.6 V,  27.5 µA @ 3.0 V, 30.4  µA @ 2.4 V | Oleg / RC5 |
| Broadcasting, connected | 38 µA @ 3.6 V =&gt; XX µW, 40 µA @ 3.0 V =&gt; 120 µW, 46  µA @ 2.4 V =&gt; 120 µW | Otso / RC5 |
|  | 36.9 µA @ 3.6 V, 39.2 µA @ 3.0 V, 44.0 µA @ 2.4 V | Oleg / RC5 |
| Transferring logs. | 8 mA @ 3.6 V =&gt; 29 mW, 8.7 mA @ 3.0 V =&gt; 26.1 mW, 9.5  mA @ 2.4 V =&gt; 22.8 µW | Otso / RC5 |
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

