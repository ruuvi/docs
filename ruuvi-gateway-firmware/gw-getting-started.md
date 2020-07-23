---
description: 'Lifecycle: Alpha. Last updated 2020-07-23'
---

# GW Getting Started

These documentation pages describe the desired behaviour of Ruuvi Gateway, not what exactly works on the unit you have received as a developer or a beta tester. All comments and feedback are welcome, please join us at slack.ruuvi.com for discussion. 

On a high level, the ESP32 acts as the Internet interface and brains of the Gatway, while nRF52 provides BLE functionality. The ICs are connected by UART bus, and both ICs have a Ruuvi Connector for attaching extension boards. 

If you want to just use the gateway, [GW ESP32 Configuration](../gw-esp32-firmware/gw-esp32-configuration.md) page is a good place to start. Review also [GW ESP32 HTTP Client](../gw-esp32-firmware/gw-esp32-http-client.md) and [GW ESP 32 MQTT Client](../gw-esp32-firmware/gw-esp32-mqtt-client.md) pages for details on how data is sent to the Internet. 

As of summer 2020 the Gateway is under active development, so specification may change and regression bugs may occur, and everything is not implemented yet. Check [Releases](../releases/) page for latest binaries and their checklist to see the current status. 

Gateway code can be found at https://github.com/ruuvi/ruuvi.gateway\_esp.c and https://github.com/ruuvi/ruuvi.gateway\_nrf.c. If you notice new bugs or want to propose new features, you can open issues at GitHub or discuss them at Ruuvi Slack.



