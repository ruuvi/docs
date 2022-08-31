---
description: 'Lifecycle: Beta. Last updated 2021-04-16'
---

# GW Getting Started

## Quickstart

1.  Turn on Ruuvi Gateway by powering it with USB-C.

    \- Quickest start: Connect Gateway to your router with Ethernet cable, wait one minute, and you're done.

    \- Note that Ethernet cable must not be connected before configuration is complete if you do not want to use default settings.
2. Start configuration by connecting to WiFi hotspot RuuviGatewayXXXX.
3. If the browser doesn't open automatically, type 10.10.0.1 to the address bar.
4. Configure RuuviGateway according to guidance and preferred settings, and connect to a local WiFi or connect Ethernet cable.
5. Gateway is now ready to be used and sending data to Ruuvi Cloud or your own cloud.

## LEDs

Ruuvi Gateway has 4 LEDs: Green, Red, Ethernet green, and Ethernet yellow.&#x20;

The green LED is on when receiving data from the Bluetooth sensors is working properly. &#x20;

Red LED blinks as follows:

* 5 times/second: Problem with the Internet connection.
* 2 times/second: Reset to factory settings complete, you can release the button to enter configuration mode.
* 1 time/second: Internal firmware update. Wait until the blinking stops. This may take up to 10 minutes.
* 1 time per 2 seconds: Configuration mode, connect to the Gateway's WiFi hotspot to configure.

Ethernet Yellow turns on when a cable connection is detected and blinks on data transfer. Green led turns on if Gateway operates at a faster 100 MBit/s speed instead of legacy 10 MBit/s. Most modern routers will have the green led on at all times.&#x20;

## Button

A short press of the button re-enables the gateway's configuration mode.&#x20;

A long press (7 seconds +) of the button is a factory reset which erases all configured settings and enables configuration mode (activates Wi-Fi hotspot).

For more details, [GW ESP32 Configuration](../gateway-html-pages/gw-esp32-configuration.md) page is a good place to start. If you're interested in using Ruuvi Gateway with your own server, review [GW ESP32 HTTP Client](../gw-esp32-firmware/gw-esp32-http-client.md) and [GW ESP 32 MQTT Client](../gw-esp32-firmware/gw-esp32-mqtt-client.md) pages for details on how data is sent to the Internet.&#x20;

## Using the Gateway with your own server

If you want to use the Gateway with your own server, you can connect via MQTT or HTTP(s). The data formats are detailed in pages TODO TODO

## Using the Gateway with Ruuvi Station app

Please check the [Ruuvi Station instruction page](https://docs.ruuvi.com/ruuvi-station-app/use-with-ruuvi-gateway-ruuvi-network).

