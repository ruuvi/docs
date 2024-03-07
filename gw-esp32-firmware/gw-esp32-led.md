---
description: 'Lifecycle: proposal'
---

# GW ESP32 LED

## LED Indications

The LED indications are listed by priority, the first matching condition is indicated.\
Indication code: the letter "R" means the red LED is on, the letter "G" means the green LED is on, and the letter "-" means the LEDs are off (by default, the step length is 100 ms).

| Gateway is rebooting                                                                         | <p>The step is 25 ms:</p><pre><code>"R-R-R-R-"
</code></pre><p>Red blinks with 50 ms period.</p>                                       |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| Bluetooth-coprocessor (nRF52) failure                                                        | Solid Red                                                                                                                              |
| Flashing Bluetooth-coprocessor (nRF52)                                                       | <pre><code>"R---------"
</code></pre><p>Red LED lights up for 100 ms every second.</p>                                                 |
| Configuration erasing has been completed (after a long press of the button)                  | <pre><code>"RR--RR--"
</code></pre><p>Red LED flashes with 400 ms period.</p>                                                          |
| Configuration hotspot is active.                                                             | <pre><code>"RRRRRRRRRRGGGGGGGGGG"
</code></pre><p>Red and green LEDs light up alternately for 1 second.</p>                            |
| Configuration hotspot is active and WPS (Wi-Fi Protected Setup) is active.                   | `"RRRRRRRRGRGGGGGGGGGG"`                                                                                                               |
| No internet connection or server returns an error code when trying to send data              | <pre><code>"R-R-R-R-R-"
</code></pre><p>Red LED lights up 5 times per second.</p>                                                      |
| No data from Bluetooth sensors                                                               | <pre><code>"G-G-G-G-G-"
</code></pre><p>Green LED lights up 5 times per second.</p>                                                    |
| No connection to all servers                                                                 | <pre><code>"RRRRR-----"
</code></pre><p>Red LED lights up for half a second every second.</p>                                          |
| No connection to some of the servers                                                         | <pre><code>"GGGGGGGGG-"
</code></pre><p>Green LED lights up continuously but goes out every second for a short interval of 100 ms.</p> |
| The data comes from the Bluetooth sensors and is successfully sent to all configured servers | Solid Green                                                                                                                            |
