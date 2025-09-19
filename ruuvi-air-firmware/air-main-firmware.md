---
noIndex: true
---

# Air Main Firmware

The main Ruuvi Air application. Ruuvi Air firmware initializes the sensors onboard and starts to advertise the sensor data. Additionally, the Ruuvi Air logs the environmental data for 10 days at 5 minute interval. This stored data persists across short power offs, but data can be logged only while device is powered.

The boot up takes \~6 seconds to start blinking the main led in blue, and around 10 seconds from that before device is ready to measure. The device calibration will improve over the first hour of operation and the accuracy specification of datasheet is matched within one hour.&#x20;

Additionally the Ruuvi Air will learn and adapt to it's environment, this adaptation process takes one week. To ensure most accurate results, the environment needs clean air at least once in a rolling one week period - e.g. through ventilation of home or office left empty for the weekend.&#x20;

The device LED will indicate the air quality through it's color. The main led brightness can be adjusted with short press of the device button, the brightness cycles in medium-low-off-bright-medium cycle.&#x20;

Firmware updates can be done in Ruuvi Station app. It is possible to enter dedicated firmware loader by pressing and holding the button for 5 seconds - once main led turns off the press is complete.&#x20;

If the entire device is stuck, a factory reset is possible by pressing and holding the button for 15 seconds. When factory reset is started, bottom leds will blink alternately green-red and button can be released.&#x20;

<figure><img src="../.gitbook/assets/Air Main flow.png" alt=""><figcaption></figcaption></figure>

Ruuvi Air code is available at [https://github.com/ruuvi/ruuvi.air.main](https://github.com/ruuvi/ruuvi.air.main)
