---
description: Immediate relaying of Bluetooth data (without timestamps) to MQTT server.
---

# MQTT: Data from Bluetooth-sensors without timestamps

```
{
  "$schema": "https://json-schema.org/draft/2019-09/schema",
  "$id": "http://ruuvi.com/schemas/ruuvi_mqtt_data_without_timestamps.schema.json",
  "title": "Data from Bluetooth-sensors (without timestamps) relayed via MQTT",
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
    "cnt": {
      "title": "Counter of messages from Bluetooth-sensors that were received by Gateway",
      "type": "string",
      "examples": [
        "338"
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
      "rssi": -25,
      "aoa": [],
      "cnt": "338",
      "data": "0201061BFF990405166455D5C6DE0008FFF403F0AE760F2A8BF41F0C28CBD6",
      "coords": ""
    }
  ]
}

```
