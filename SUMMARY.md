# Table of contents

* [Ruuvi Developer Documentation](README.md)

## Ruuvi Hardware

* [RuuviTag B](ruuvi-hardware/ruuvitag-b.md)
* [Ruuvi Gateway](ruuvi-hardware/ruuvi-gateway.md)

## Ruuvi Firmware

* [1.2.12](ruuvi-firmware/1.2.12.md)
* [2.5.9](ruuvi-firmware/2.5.9.md)
* [3.X](ruuvi-firmware/3.x/README.md)
  * [3.x Sensors](ruuvi-firmware/3.x/3.x-sensors.md)
  * [3.x Heartbeat](ruuvi-firmware/3.x/3.x-heartbeat.md)
  * [Releases](ruuvi-firmware/3.x/releases/README.md)
    * [Ruuvi Firmware 3.29.0](ruuvi-firmware/3.x/releases/ruuvi-firmware-3.29.0.md)
* [Device Firmware Update \(DFU\)](ruuvi-firmware/device-firmware-update-dfu.md)

## Ruuvi Gateway Firmware

* [GW nRF52811 Firmware](ruuvi-gateway-firmware/gw-nrf52-firmware/README.md)
  * [GW nRF52811 selftest](ruuvi-gateway-firmware/gw-nrf52-firmware/gw-nrf52811-selftest.md)
  * [GW nRF52811 scanning](ruuvi-gateway-firmware/gw-nrf52-firmware/gw-nrf52811-scanning.md)
  * [GW nRF52811 repeating](ruuvi-gateway-firmware/gw-nrf52-firmware/gw-nrf52811-repeating.md)
  * [GW nRF52811 UART communication](ruuvi-gateway-firmware/gw-nrf52-firmware/gw-nrf52811-uart-communication.md)

---

* [GW ESP32 Firmware](gw-esp32-firmware/README.md)
  * [GW ESP32 Selftest](gw-esp32-firmware/gw-esp32-selftest.md)
  * [GW ESP32 WiFi Hotspot](gw-esp32-firmware/gw-esp32-wifi-hotspot.md)
  * [GW ESP32 Configuration](gw-esp32-firmware/gw-esp32-configuration.md)
  * [GW ESP32 Button](gw-esp32-firmware/gw-esp32-button.md)
  * [GW ESP32 LED](gw-esp32-firmware/gw-esp32-led.md)
  * [GW ESP32 MQTT client](gw-esp32-firmware/gw-esp32-mqtt-client.md)

## Ruuvi Connector System

* [Introduction](ruuvi-connector-system/introduction.md)
* [Expansion boards](ruuvi-connector-system/expansion-boards.md)
* [Cables](ruuvi-connector-system/cables.md)
* [Connectors](ruuvi-connector-system/connectors.md)

## Communicate with Ruuvi devices <a id="communication"></a>

* [Bluetooth advertisements](communication/bluetooth-advertisements/README.md)
  * [Data format 3 \(RAWv1\)](communication/bluetooth-advertisements/data-format-3-rawv1.md)
  * [Data format 4 \(URL\)](communication/bluetooth-advertisements/data-format-4-url.md)
  * [Data format 5 \(RAWv2\)](communication/bluetooth-advertisements/data-format-5-rawv2.md)
  * [Data format 8 \(Encrypted environmental\)](communication/bluetooth-advertisements/data-format-8-encrypted-environmental.md)
* [Bluetooth connection](communication/bluetooth-connection/README.md)
  * [DIS \(Device Information Service\)](communication/bluetooth-connection/device-information-service-dis.md)
  * [NUS \(Nordic UART Service\)](communication/bluetooth-connection/nordic-uart-service-nus/README.md)
    * [Heartbeat transmissions](communication/bluetooth-connection/nordic-uart-service-nus/heartbeat-transmissions.md)
    * [Read logged history](communication/bluetooth-connection/nordic-uart-service-nus/log-read.md)
* [Ruuvi Network](communication/ruuvi-network/README.md)
  * [Backends](communication/ruuvi-network/backends/README.md)
    * [AWS Amplify](communication/ruuvi-network/backends/amplify.md)
    * [Kaltiot](communication/ruuvi-network/backends/kaltiot-1/README.md)
      * [Kaltiot Smart Tracker Public REST API](communication/ruuvi-network/backends/kaltiot-1/kaltiot.md)
    * [WhereOS](communication/ruuvi-network/backends/whereos.md)
  * [Gateways](communication/ruuvi-network/gateways.md)
* [Naming conventions](communication/units-and-naming-conventions.md)
* [Real Time Transfer \(RTT\)](communication/development-real-time-transfer.md)

