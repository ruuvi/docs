---
description: 'Lifecycle: proposal'
---

# GW ESP32 LED

{% hint style="info" %}
Ruuvi GW A1 doesn not have LED controlled by ESP32, so this section isn't valid for A1 hardware.
{% endhint %}

## LED Indications

The LED indications are listed by priority, the first matching condition is indicated.

| State | Indication | Lifecycle | Since version |
| :--- | :--- | :--- | :--- |
| Button is pressed. | LED blinks at 50 % duty cycle, 2 Hz interval. | Beta | 1.0 |
| Configuration hotspot is active. | LED blinks at 50 % duty cycle, 0.5 Hz interval. | Beta | 1.0 |
| Configuration hotspot is not active, no internet connection or server returns error code when trying to send data. | LED blinks at 50% duty cycle, 5 Hz interval. | Beta | 1.0 |
| Data is sent normally | LED is on at 100 % of time. | Beta | 1.0 |

## Test checklist

| Event | Test | CI / Manual |
| :--- | :--- | :--- |
| Button press indication. | Button press indication is activated if gateway was in normal operation mode. | Manual |
| Configuration hotspot active indication. | Do a short press while gateway was in normal mode to activate hotspot. Observe new indication. | Manual |
| Error indication. | Connect gateway to internet with Ethernet cable, remove Ethernet, observe error indication. | Manual |
| Normal state indication. | Connect gateway to the Internet with Ethernet cable, observe normal state indication.  | Manual |

