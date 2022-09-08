---
description: 'Lifecycle: proposal'
---

# GW ESP32 LED

## LED Indications

The LED indications are listed by priority, the first matching condition is indicated.

| Button is pressed.                                                               | Red LED blinks at 50 % duty cycle, 2 Hz interval, Green LED is on.   |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Erase configuration completed (after long button press)                          | Red LED blinks at 50 % duty cycle, 2 Hz interval, Green LED is off.  |
| Configuration hotspot is active.                                                 | Red LED blinks at 50 % duty cycle, 0.5 Hz interval, Green LED is on. |
| No internet connection or server returns an error code when trying to send data. | Red LED blinks at 50% duty cycle, 5 Hz interval, Green LED is on.    |
| Data is sent normally                                                            | Green LED is on 100% of the time, Red LED is off.                    |

## Test checklist

| Event                                    | Test                                                                                           | CI / Manual |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------- | ----------- |
| Button press indication.                 | Button press indication is activated if gateway was in normal operation mode.                  | Manual      |
| Configuration hotspot active indication. | Do a short press while gateway was in normal mode to activate hotspot. Observe new indication. | Manual      |
| Error indication.                        | Connect gateway to internet with Ethernet cable, remove Ethernet, observe error indication.    | Manual      |
| Normal state indication.                 | Connect gateway to the Internet with Ethernet cable, observe normal state indication.          | Manual      |
