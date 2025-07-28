---
description: >-
  Relaying of accumulated time-stamped data from Bluetooth-sensors to HTTP/HTTPS
  server.
---

# HTTP: Time-stamped data from Bluetooth-sensors

The JSON data format description is provided in JSON schema format ([https://json-schema.org](https://json-schema.org)), which provides clear human- and machine-readable documentation with examples.

The format of relayed messages is described here [https://docs.ruuvi.com/communication/bluetooth-advertisements](https://docs.ruuvi.com/communication/bluetooth-advertisements)

```json
{
  "$schema": "https://json-schema.org/draft/2019-09/schema",
  "$id": "http://ruuvi.com/schemas/ruuvi_http_data_with_timestamps.schema.json",
  "title": "Time-stamped data from Bluetooth-sensors relayed via HTTP/HTTPS",
  "type": "object",
  "required": [
    "data"
  ],
  "properties": {
    "data": {
      "title": "Data-object containing accumulated data from Bluetooth-sensors for relaying",
      "type": "object",
      "required": [
        "timestamp",
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
        "timestamp": {
          "type": "string",
          "title": "Timestamp (Unix-time) when the accumulated messages from Bluetooth-sensors was relayed by Gateway",
          "examples": [
            "1653633988"
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
                  "timestamp",
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
                  "timestamp": {
                    "type": "string",
                    "title": "Timestamp (Unix-time) when the message from Bluetooth-sensor was received by Gateway",
                    "examples": [
                      "1653633986"
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
        "timestamp": "1653633988",
        "nonce": "2636366621",
        "gw_mac": "C8:25:2D:8E:9C:2C",
        "tags": {
          "C6:A5:B9:E0:AD:06": {
            "rssi": -71,
            "timestamp": "1653633986",
            "data": "0201061BFF99040513C85714C7CC00240008041CAB76F41C3CC6A5B9E0AD06"
          },
          "E3:75:CF:37:4E:23": {
            "rssi": -72,
            "timestamp": "1653633986",
            "data": "0201061BFF99040514565D7CC7850008003C03E4A9F6741CC3E375CF374E23"
          }
        }
      }
    }
  ]
}

```
