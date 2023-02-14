# MQTT examples

Here is an example of MQTT configuration on the Ruuvi Gateway:

<figure><img src="../.gitbook/assets/image (1) (2).png" alt=""><figcaption></figcaption></figure>

Here are sample commands to subscribe an MQTT client to notifications from the Ruuvi Gateway:

* Subscribe to service messages from this Gateway:\
  `mosquitto_sub -h test.mosquitto.org -p 1883 -t "ruuvi/AA:BB:CC:DD:EE:FF/gw_status" -v`
* Subscribe to service messages from any Gateway:\
  `mosquitto_sub -h test.mosquitto.org -p 1883 -t "ruuvi/#/gw_status" -v`
* Subscribe to messages from a Bluetooth sensor with the MAC:\
  `mosquitto_sub -h test.mosquitto.org -p 1883 -t "ruuvi/#/<TAG_MAC>/#" -v`
* Subscribe to messages from any Bluetooth sensor that this Gateway receives:\
  `mosquitto_sub -h test.mosquitto.org -p 1883 -t "ruuvi/AA:BB:CC:DD:EE:FF/#/#" -v`
* Subscribe to all messages:\
  `mosquitto_sub -h test.mosquitto.org -p 1883 -t "ruuvi/#" -v`\
