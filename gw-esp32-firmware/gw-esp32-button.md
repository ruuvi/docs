---
description: 'Lifecycle: Alpha'
---

# GW ESP32 Button

## Button functionality

ESP32 has two buttons, one is hardwired reset and one is input to GPIO. 

The input button has floating terminal to ESP32 and other terminal is grounded, i.e. ESP32 must activate internal pull-up resistor and sens interrupts.

On button press, a timer is started to detect if the button press is a short press or a long press and led indicates that button is pressed.

If the press is longer than 1 seconds, the press is considered to be a short press and configuration hotspot is enabled once button is released. 

If the press is longer than 5 seconds, all user settings on flash are erased and configuration hotspot is enabled once button is released. 

| Event | Action | Lifecycle | Since version |
| :--- | :--- | :--- | :--- |
| Button press | Indicate button press, start timer | Beta | 1.0 |
| Button released | Stop button press indication, stop timer | Beta | 1.0 |
| Timer &gt; 1 s | Re-enable configuration hotspot | Beta | 1.0 |
| Timer &gt; 5 s | Erase settings stored to flash | Beta | 1.0 |

{% hint style="info" %}
If Gateway is connected to Internet via Ethernet cable, the default action is to connect to Ruuvi Network with default settings and turn hotspot off. Disconnect Ethernet cable if that is not intentional.
{% endhint %}

## Test checklist

| Event | Test | CI / Manual |
| :--- | :--- | :--- |
| Button is pressed | LED indicates button press | Manual |
| Button is released | LEDs indicate state after press | Manual |
| Timer has &gt; 1 s value | Configuration hotspot is activated, settings in flash remain | Manual |
| Timer has &gt; 5 s value | Configuration hotspot is activated, settins in flash are erased  | Manual |

