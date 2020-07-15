---
description: 'Lifecycle: Alpha. Page updated 2020-07-15'
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
      <td style="text-align:left">System test &quot;DFU test&quot;.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag stays in bootloader mode if button &quot;B&quot; is pressed on boot.</td>
      <td
      style="text-align:left">Manually, hold down &quot;B&quot;, press and release &quot;R&quot;, release
        &quot;R&quot;.</td>
        <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag initializes watchdog.</td>
      <td style="text-align:left">
        <p>Unit test</p>
        <p><em>test_main.c</em>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag turns RED LED on for self-test duration.</td>
      <td style="text-align:left">Manually, visual check</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag runs self-tests to detect installed sensors.</td>
      <td style="text-align:left">
        <p>Unit tests</p>
        <p><em>test_main.c test_app_sensor.c</em>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">Tag erases settings stored to flash file system and reboots if flash file
        system cannot be initialized.</td>
      <td style="text-align:left">TODO</td>
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
      style="text-align:left">Unit test <em>test_app_heartbeat.c. </em>Check power profile manually.</td>
        <td
        style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">All data fields of advertisement are valid RAWv2 values.</td>
      <td style="text-align:left">Manually, check Ruuvi Station Android displays temperature, humidity,
        pressure, acceleration, voltage. Check MAC address, TX power +4, and measurement
        sequence counter bytes with nRF Connect captured data.</td>
      <td style="text-align:left"></td>
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

### Button
