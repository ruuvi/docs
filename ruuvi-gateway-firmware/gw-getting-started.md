---
description: 'Lifecycle: Beta. Last updated 2021-04-16'
---

# GW Getting Started

## Quickstart

1. Turn on Ruuvi Gateway by powering it with USB-C.

   - Quickest start: Connect Gateway to your router with Ethernet cable and you're done.

   - Note that Ethernet cable must not be connected before configuration is complete if you do not want to use default settings.

2. Start configuration by connecting to Ruuvi Gateway XXXX with Wi-Fi - password "12345678".
3. If browser doesn't open automatically, type 10.10.0.1 to the address bar.
4. Configure RuuviGateway according to guidance, preferred settings, and connect to a local WiFi or connect Ethernet cable.
5. Gateway is now ready to be used and sending data to Ruuvi Network or your own cloud.

## Leds

Ruuvi Gateway has 4 LEDs: Green, Red, Ethernet green and Ethernet yellow. 

Green LED blinks when a BLE packet matching filters is received.  Red LED blinks as follows:

* 5 times / second: Problem with Internet connection.
* 2 times / second: Ready to enter configuration mode, release button.
* 1 time / second: Internal update, wait until blinking stops. This may take up to 10 minutes.
* 1 time / 2 seconds: Configuration mode, connect to Gateway WiFi hotspot to configure.

Ethernet Yellow turns on when a cable connection is detected and blinks on data transfer. Green led turns on if Gateway operates at faster 100 MBit / s speed instead of legacy 10 MBit / s. Most modern routers will have the green led on at all times. 

## Button

A short press of button re-enables gateway configuration. A long press \(5 seconds +\) of the button is a factory reset which erases all configured settigns and enables configuration WiFi. Please note that Ethernet cable must be disconnected to enter configuration mode.

For more details, [GW ESP32 Configuration](../gw-esp32-firmware/gw-esp32-configuration.md) page is a good place to start. If you're interested in using Ruuvi Gateway with your own server, review [GW ESP32 HTTP Client](../gw-esp32-firmware/gw-esp32-http-client.md) and [GW ESP 32 MQTT Client](../gw-esp32-firmware/gw-esp32-mqtt-client.md) pages for details on how data is sent to the Internet. 

## Using the Gateway with your own server

If you want to use the Gateway with your own server, you can connect via MQTT or HTTP\(s\). The data formats are detailed in pages TODO TODO

## Using the Gateway with Ruuvi Station app



