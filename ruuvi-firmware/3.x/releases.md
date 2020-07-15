---
description: 'Lifecycle: Alpha. Updated 2020-07-15'
---

# Releases

Releases are verified against the checklist below. This checklist is copied into a new release. 

## Test checklist

### Power-on

{% tabs %}
{% tab title="RuuviTag B+" %}
| Action | How to test | Verified by |
| :--- | :--- | :--- |
| Tag stays in bootloader mode / begins DFU if application commanded tag into DFU mode. | System test "DFU test". |  |
| Tag stays in bootloader mode if button "B" is pressed on boot. | Manually, hold down "B", press and release "R", release "R". |  |
| Tag initializes watchdog. | Unit test test\_main.c |  |
| Tag turns RED LED on for self-test duration. | Manually, visual check |  |
| Tag runs self-tests to detect installed sensors.  | Unit tests test\_main.c test\_app\_sensor.c |  |
| Tag erases settings stored to flash file system and reboots if flash file system cannot be initialized. | TODO |  |
| Tag turns GREEN LED on for one second if no errors were detected in self-test phase. Missing sensors are allowed. | Manually, visual check. |  |
| Tag advertises at 100 ms interval for 5 seconds at boot. Duplicate data is allowed, but every packet must be valid. Initial dataformat is RAWv2.  | Unit test test\_app\_heartbeat.c. __Check power profile manually. |  |
| All data fields of advertisement are valid RAWv2 values.  | Manually, check that Ruuvi Station Android displays temperature, humidity, pressure, acceleration, voltage. Check MAC address, TX power +4, and measurement sequence counter bytes with nRF Connect captured data. |  |
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







