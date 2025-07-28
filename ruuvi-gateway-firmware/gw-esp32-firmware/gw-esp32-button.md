# GW ESP32 Button

## Button functionality

ESP32 has two buttons, one is hardwired reset and one is input to GPIO.&#x20;

The input button has floating terminal to ESP32 and other terminal is grounded, i.e. ESP32 must activate the internal pull-up resistor and interrupts.

On button press, a timer is started to detect if the button press is a short press or a long press, and LED indicates that the button is pressed.

If the press is less than 5 seconds, the press is considered to be a short press, and the configuration hotspot is enabled once the button is released.&#x20;

If the press is longer than 5 seconds, all user settings on flash are erased, and the configuration hotspot is enabled once the button is released.&#x20;

{% hint style="info" %}
If Gateway is connected to the Internet via Ethernet cable, the default action is to connect to Ruuvi Network with default settings and turn the hotspot off. Disconnect Ethernet cable if that is not intentional.
{% endhint %}
