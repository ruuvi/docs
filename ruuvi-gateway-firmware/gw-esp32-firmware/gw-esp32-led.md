---
description: 'Lifecycle: proposal'
---

# GW ESP32 LED

## LED Indications

The LED indications are listed by priority, the first matching condition is indicated.\
Indication code: the letter "R" means the red LED is on, the letter "G" means the green LED is on, and the letter "-" means the LEDs are off (by default, the step length is 100 ms).

<table data-header-hidden><thead><tr><th>State</th><th>Indication</th></tr></thead><tbody><tr><td>Gateway is rebooting</td><td><p>The step is 25 ms:</p><pre><code>"R-R-R-R-"
</code></pre><p>Red blinks with 50 ms period.</p></td></tr><tr><td>Bluetooth-coprocessor (nRF52) failure</td><td>Solid Red</td></tr><tr><td>Flashing Bluetooth-coprocessor (nRF52)</td><td><pre><code>"R---------"
</code></pre><p>Red LED lights up for 100 ms every second.</p></td></tr><tr><td>Configuration erasing has been completed (after a long press of the button)</td><td><pre><code>"RR--RR--"
</code></pre><p>Red LED flashes with 400 ms period.</p></td></tr><tr><td>Configuration hotspot is active.</td><td><pre><code>"RRRRRRRRRRGGGGGGGGGG"
</code></pre><p>Red and green LEDs light up alternately for 1 second.</p></td></tr><tr><td>Configuration hotspot is active and WPS (Wi-Fi Protected Setup) is active.</td><td><code>"RRRRRRRRGRGGGGGGGGGG"</code></td></tr><tr><td>No internet connection or server returns an error code when trying to send data</td><td><pre><code>"R-R-R-R-R-"
</code></pre><p>Red LED lights up 5 times per second.</p></td></tr><tr><td>No data from Bluetooth sensors</td><td><pre><code>"G-G-G-G-G-"
</code></pre><p>Green LED lights up 5 times per second.</p></td></tr><tr><td>No connection to all servers</td><td><pre><code>"RRRRR-----"
</code></pre><p>Red LED lights up for half a second every second.</p></td></tr><tr><td>No connection to some of the servers</td><td><pre><code>"GGGGGGGGG-"
</code></pre><p>Green LED lights up continuously but goes out every second for a short interval of 100 ms.</p></td></tr><tr><td>The data comes from the Bluetooth sensors and is successfully sent to all configured servers</td><td>Solid Green</td></tr></tbody></table>
