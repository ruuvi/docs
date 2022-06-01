---
description: >-
  Relaying of accumulated Bluetooth data (without timestamps) to HTTP/HTTPS
  server.
---

# HTTP: Data from Bluetooth-sensors without timestamps

```
{
  "$schema": "https://json-schema.org/draft/2019-09/schema",
  "$id": "http://ruuvi.com/schemas/ruuvi_http_data_without_timestamps.schema.json",
  "title": "Data from Bluetooth-sensors (without timestamps) relayed via HTTP/HTTPS",
  "type": "object",
  "required": [
    "data"
  ],
  "properties": {
    "data": {
      "title": "Data-object containing accumulated data from Bluetooth-sensors for relaying",
      "type": "object",
      "required": [
        "nonce",
        "gw_mac",
        "tags"
      ],
      "properties": {
        "coordinates": {
          "type": "string",
          "default": "",
          "title": "GPS-coordinates of Ruuvi Gateway (optional)",
          "examples": [
            ""
          ]
        },
        "nonce": {
          "type": "string",
          "title": "Nonce - sequentially incremented number for each message, the initial value of which is set randomly",
          "examples": [
            "2636366621"
          ]
        },
        "gw_mac": {
          "type": "string",
          "title": "MAC-address of Ruuvi Gateway",
          "examples": [
            "C8:25:2D:8E:9C:2C"
          ]
        },
        "tags": {
          "type": "object",
          "title": "Array of records with relayed messages from Bluetooth-sensors",
          "items": {
            "type": "object",
            "patternProperties": {
              "^([0-9A-Fa-f]{2}[:-]){5}([0-9A-Fa-f]{2})$": {
                "type": "object",
                "title": "MAC-address of Bluetooth-sensor",
                "required": [
                  "rssi",
                  "counter",
                  "data"
                ],
                "properties": {
                  "rssi": {
                    "type": "integer",
                    "title": "RSSI",
                    "examples": [
                      -71
                    ]
                  },
                  "counter": {
                    "type": "string",
                    "title": "Counter of messages from Bluetooth-sensors that were received by Gateway",
                    "examples": [
                      "363"
                    ]
                  },
                  "data": {
                    "type": "string",
                    "title": "Relayed message from Bluetooth-sensor in hex encoding",
                    "examples": [
                      "0201061BFF99040513C85714C7CC00240008041CAB76F41C3CC6A5B9E0AD06"
                    ]
                  }
                }
              }
            },
            "minItems": 0,
            "uniqueItems": true
          }
        }
      }
    }
  },
  "examples": [
    {
      "data": {
        "coordinates": "",
        "nonce": "2896361039",
        "gw_mac": "C8:25:2D:8E:9C:2C",
        "tags": {
          "E3:75:CF:37:4E:23": {
            "rssi": -50,
            "counter": "363",
            "data": "0201061BFF990405158A5B05C6810004004403DCAB767A45BDE375CF374E23"
          },
          "F4:1F:0C:28:CB:D6": {
            "rssi": -32,
            "counter": "365",
            "data": "0201061BFF990405166455D5C6DD0008FFF803F0ADB60F2A92F41F0C28CBD6"
          }
        }
      }
    }
  ]
}

```
