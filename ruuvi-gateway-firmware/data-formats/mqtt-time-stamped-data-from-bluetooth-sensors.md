---
description: Immediate relaying of Bluetooth data (with timestamps) to MQTT server.
---

# MQTT: Time-stamped data from Bluetooth-sensors

The JSON data format description is provided in JSON schema format ([https://json-schema.org](https://json-schema.org)), which provides clear human- and machine-readable documentation with examples.

The format of relayed messages is described here [https://docs.ruuvi.com/communication/bluetooth-advertisements](https://docs.ruuvi.com/communication/bluetooth-advertisements)

```json
{
  "$schema": "https://json-schema.org/draft/2019-09/schema",
  "$id": "http://ruuvi.com/schemas/ruuvi_mqtt_data_with_timestamps.schema.json",
  "title": "Time-stamped data from Bluetooth-sensors relayed via MQTT",
  "type": "object",
  "required": [
    "data"
  ],
  "properties": {
    "gw_mac": {
      "title": "MAC-address of Ruuvi Gateway",
      "type": "string",
      "pattern": "^([0-9A-Fa-f]{2}[:-]){5}([0-9A-Fa-f]{2})$",
      "examples": [
        "C8:25:2D:8E:9C:2C"
      ]
    },
    "rssi": {
      "title": "RSSI",
      "type": "integer",
      "examples": [
        -26
      ]
    },
    "aoa": {
      "title": "???",
      "type": "array",
      "default": [],
      "items": {},
      "examples": [
        []
      ]
    },
    "gwts": {
      "title": "Timestamp (Unix-time) when the message from Bluetooth-sensor was relayed by Gateway",
      "type": "string",
      "examples": [
        "1653668027"
      ]
    },
    "ts": {
      "title": "Timestamp (Unix-time) when the message from Bluetooth-sensor was received by Gateway",
      "type": "string",
      "examples": [
        "1653668027"
      ]
    },
    "data": {
      "title": "Relayed message from Bluetooth-sensor in hex encoding",
      "type": "string",
      "examples": [
        "0201061BFF99040515AE4C6DC6D7000CFFF803F4ADB6AD697FF41F0C28CBD6"
      ]
    },
    "coords": {
      "title": "GPS-coordinates of Ruuvi Gateway (optional)",
      "type": "string",
      "examples": [
        ""
      ]
    }
  },
  "examples": [
    {
      "gw_mac": "C8:25:2D:8E:9C:2C",
      "rssi": -26,
      "aoa": [],
      "gwts": "1653668027",
      "ts": "1653668027",
      "data": "0201061BFF99040515AE4C6DC6D7000CFFF803F4ADB6AD697FF41F0C28CBD6",
      "coords": ""
    }
  ]
}

```
