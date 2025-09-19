# Table of contents

* [Ruuvi Developer Documentation](README.md)

## Ruuvi Hardware

* [RuuviTag B](ruuvi-hardware/ruuvitag-b.md)
* [RuuviTag Pro](ruuvi-hardware/ruuvitag-pro.md)
* [Ruuvi Gateway](ruuvi-hardware/ruuvi-gateway.md)
* [Ruuvi DevShield](ruuvi-hardware/ruuvi-devshield.md)
* [Ruuvi Connector Kit](ruuvi-hardware/ruuvi-connector-kit.md)
* [TMP 117 External Sensor](ruuvi-hardware/tmp-117-external-sensor.md)

## Ruuvi Connector System

* [Introduction](ruuvi-connector-system/introduction.md)
* [Expansion boards](ruuvi-connector-system/expansion-boards.md)
* [Cables](ruuvi-connector-system/cables.md)
* [Connectors](ruuvi-connector-system/connectors.md)

## RuuviTag Firmware <a href="#ruuvi-firmware" id="ruuvi-firmware"></a>

* [1.2.12](ruuvi-firmware/1.2.12.md)
* [2.5.9](ruuvi-firmware/2.5.9.md)
* [3.X](ruuvi-firmware/3.x/README.md)
  * [3.x Sensors](ruuvi-firmware/3.x/3.x-sensors.md)
  * [3.x Heartbeat](ruuvi-firmware/3.x/3.x-heartbeat.md)
* [Device Firmware Update (DFU)](ruuvi-firmware/device-firmware-update-dfu.md)

## Ruuvi Air Firmware

* [Air 1st Stage Bootloader](ruuvi-air-firmware/air-1st-stage-bootloader.md)
* [Air 2nd Stage Bootloader](ruuvi-air-firmware/air-2nd-stage-bootloader.md)
* [Air Firmware Loader](ruuvi-air-firmware/air-firmware-loader.md)
* [Air Main Firmware](ruuvi-air-firmware/air-main-firmware.md)
* [Ruuvi Indoor Air Quality Score (IAQS)](ruuvi-air-firmware/ruuvi-indoor-air-quality-score-iaqs.md)

## Ruuvi Gateway Firmware

* [GW Getting Started](ruuvi-gateway-firmware/gw-getting-started.md)
* [GW Web-UI](gateway-html-pages/README.md)
  * [Greeting window](ruuvi-gateway-firmware/gateway-web-ui/greeting-window.md)
  * [Internet connection settings](ruuvi-gateway-firmware/gateway-web-ui/internet-connection-settings/README.md)
    * [Connection via Wi-Fi](ruuvi-gateway-firmware/gateway-web-ui/internet-connection-settings/connection-via-wi-fi.md)
    * [Connection via Ethernet](ruuvi-gateway-firmware/gateway-web-ui/internet-connection-settings/connection-via-ethernet.md)
  * [Software update](ruuvi-gateway-firmware/gateway-web-ui/software-update.md)
  * [Automatic configuration download](ruuvi-gateway-firmware/gateway-web-ui/automatic-configuration-download.md)
  * [Automatic updates](ruuvi-gateway-firmware/gateway-web-ui/automatic-updates.md)
  * [Access Settings from LAN](ruuvi-gateway-firmware/gateway-web-ui/access-settings-from-lan.md)
  * [Cloud Options](ruuvi-gateway-firmware/gateway-web-ui/cloud-options/README.md)
    * [Backend: HTTP(s)](ruuvi-gateway-firmware/gateway-web-ui/cloud-options/backend-http-s.md)
    * [Backend: MQTT(s)](ruuvi-gateway-firmware/gateway-web-ui/cloud-options/backend-mqtt-s.md)
    * [Backend: Statistics](ruuvi-gateway-firmware/gateway-web-ui/cloud-options/backend-statistics.md)
  * [Time Synchronisation Options](ruuvi-gateway-firmware/gateway-web-ui/time-synchronisation-options.md)
  * [Bluetooth Scanning Settings](ruuvi-gateway-firmware/gateway-web-ui/bluetooth-scanning-settings.md)
  * [Configuration completion](ruuvi-gateway-firmware/gateway-web-ui/configuration-completion.md)
  * [Authentication when accessing from LAN](gateway-html-pages/auth.html.md)
* [GW nRF52811 Firmware](ruuvi-gateway-firmware/gw-nrf52-firmware/README.md)
  * [GW nRF52811 selftest](ruuvi-gateway-firmware/gw-nrf52-firmware/gw-nrf52811-selftest.md)
  * [GW nRF52811 scanning](ruuvi-gateway-firmware/gw-nrf52-firmware/gw-nrf52811-scanning.md)
  * [GW nRF52811 repeating](ruuvi-gateway-firmware/gw-nrf52-firmware/gw-nrf52811-repeating.md)
  * [GW nRF52811 UART communication](ruuvi-gateway-firmware/gw-nrf52-firmware/gw-nrf52811-uart-communication.md)
* [GW ESP32 Firmware](ruuvi-gateway-firmware/gw-esp32-firmware/README.md)
  * [GW ESP32 WiFi Hotspot](ruuvi-gateway-firmware/gw-esp32-firmware/gw-esp32-wifi-hotspot.md)
  * [GW ESP32 Button](ruuvi-gateway-firmware/gw-esp32-firmware/gw-esp32-button.md)
  * [GW ESP32 LED](ruuvi-gateway-firmware/gw-esp32-firmware/gw-esp32-led.md)
  * [GW ESP32 HTTP Client](ruuvi-gateway-firmware/gw-esp32-firmware/gw-esp32-http-client.md)
  * [GW ESP32 MQTT client](ruuvi-gateway-firmware/gw-esp32-firmware/gw-esp32-mqtt-client.md)
* [GW Data formats](ruuvi-gateway-firmware/data-formats/README.md)
  * [HTTP: Time-stamped data from Bluetooth-sensors](ruuvi-gateway-firmware/data-formats/http-time-stamped-data-from-bluetooth-sensors.md)
  * [HTTP: Data from Bluetooth-sensors without timestamps](ruuvi-gateway-firmware/data-formats/http-data-from-bluetooth-sensors-without-timestamps.md)
  * [MQTT: Time-stamped data from Bluetooth-sensors](ruuvi-gateway-firmware/data-formats/mqtt-time-stamped-data-from-bluetooth-sensors.md)
  * [MQTT: Data from Bluetooth-sensors without timestamps](ruuvi-gateway-firmware/data-formats/mqtt-data-from-bluetooth-sensors-without-timestamps.md)
  * [HTTP GET /history (with timestamps) and decoding](ruuvi-gateway-firmware/data-formats/http-get-history-with-timestamps-and-decoding.md)
  * [HTTP: Gateway status](ruuvi-gateway-firmware/data-formats/http-gateway-status.md)
  * [Gateway configuration](ruuvi-gateway-firmware/data-formats/gateway-configuration.md)
* [GW Examples](ruuvi-gateway-firmware/examples/README.md)
  * [Polling mode](ruuvi-gateway-firmware/examples/polling-mode.md)
  * [Poll endpoint "/metrics"](ruuvi-gateway-firmware/examples/poll-endpoint-metrics.md)
  * [Configuration update via API](ruuvi-gateway-firmware/examples/configuration-update-via-api.md)
  * [Firmware update via API](ruuvi-gateway-firmware/examples/firmware-update-via-api.md)
  * [Configuration download from a remote server via API](ruuvi-gateway-firmware/examples/configuration-download-from-a-remote-server-via-api.md)
  * [MQTT examples](ruuvi-gateway-firmware/examples/mqtt-examples.md)
  * [Home Assistant](ruuvi-gateway-firmware/examples/home-assistant.md)
  * [MQTT+AWS IoT Core](ruuvi-gateway-firmware/examples/mqtt+aws-iot-core.md)
* [GW open ports / services](ruuvi-gateway-firmware/gw-open-ports-services.md)
* [GW Install custom firmware](ruuvi-gateway-firmware/gw-install-custom-firmware.md)

## Communicate with RuuviTag devices via Bluetooth <a href="#communication" id="communication"></a>

* [Bluetooth advertisements](communication/bluetooth-advertisements/README.md)
  * [Data format 3 (RAWv1)](communication/bluetooth-advertisements/data-format-3-rawv1.md)
  * [Data format 4 (URL)](communication/bluetooth-advertisements/data-format-4-url.md)
  * [Data format 5 (RAWv2)](communication/bluetooth-advertisements/data-format-5-rawv2.md)
  * [Data format C5 (Cut-RAWv2)](communication/bluetooth-advertisements/data-format-c5-rawv2.md)
  * [Data format 6 ](communication/bluetooth-advertisements/data-format-6.md)
  * [Data format 8 (Encrypted environmental)](communication/bluetooth-advertisements/data-format-8-encrypted-environmental.md)
  * [Data format E1 (Extended v1)](communication/bluetooth-advertisements/data-format-e1.md)
* [Bluetooth connection](communication/bluetooth-connection/README.md)
  * [DIS (Device Information Service)](communication/bluetooth-connection/device-information-service-dis.md)
  * [NUS (Nordic UART Service)](communication/bluetooth-connection/nordic-uart-service-nus/README.md)
    * [Heartbeat transmissions](communication/bluetooth-connection/nordic-uart-service-nus/heartbeat-transmissions.md)
    * [Read logged history](communication/bluetooth-connection/nordic-uart-service-nus/log-read.md)
* [Real Time Transfer (RTT)](communication/development-real-time-transfer.md)

## Communicate with Ruuvi Cloud

* [Ruuvi Cloud](communicate-with-ruuvi-cloud/cloud/README.md)
  * [User API](communicate-with-ruuvi-cloud/cloud/user-api.md)
  * [Gateway API](communicate-with-ruuvi-cloud/cloud/gateway-api.md)
  * [Internal API](communicate-with-ruuvi-cloud/cloud/internal-api.md)
  * [Alerts](communicate-with-ruuvi-cloud/cloud/alerts.md)
  * [Cloud stored app settings](communicate-with-ruuvi-cloud/cloud/cloud-stored-app-settings.md)

## Ruuvi Community projects

* [Integrations](ruuvi-community-projects/integrations.md)
