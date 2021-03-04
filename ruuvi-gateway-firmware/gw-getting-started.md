---
description: 'Lifecycle: Alpha. Last updated 2021-03-04'
---

# GW Getting Started

## Quickstart

1. Turn on Ruuvi Gateway by powering it with USB-C.

     - Quickest start: Connect Gateway to your router with Ethernet cable and  you're done

2. Start configuration by connecting to Ruuvi Gateway XXXX with Wi-Fi - password "12345678".
3. If browser doesn't open automatically, type 10.10.0.1 to the address bar.
4. Configure RuuviGateway according to guidance, preferred settings, and connect to local Wi-Fi.
5. Gateway is now ready to be used and sending data to Ruuvi Network or your own cloud.

For more details, [GW ESP32 Configuration](../gw-esp32-firmware/gw-esp32-configuration.md) page is a good place to start. If you're interested in using Ruuvi Gateway with your own server, review [GW ESP32 HTTP Client](../gw-esp32-firmware/gw-esp32-http-client.md) and [GW ESP 32 MQTT Client](../gw-esp32-firmware/gw-esp32-mqtt-client.md) pages for details on how data is sent to the Internet. 

All comments and feedback are welcome, please join us at slack.ruuvi.com for discussion. 

On a high level, the ESP32 acts as the Internet interface and brains of the Gatway, while nRF52 provides BLE functionality. The ICs are connected by UART bus, and both ICs have a Ruuvi Connector for attaching extension boards. 

As of spring 2021 the Gateway is under active development, so specification may change, regression bugs may occur and everything is not implemented yet. Check Releases page for latest binaries and their checklist to see the current status. 

Gateway code can be found at https://github.com/ruuvi/ruuvi.gateway\_esp.c and https://github.com/ruuvi/ruuvi.gateway\_nrf.c. If you notice new bugs or want to propose new features, you can open issues at GitHub or discuss them at Ruuvi Slack.



