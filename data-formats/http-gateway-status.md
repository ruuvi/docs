---
description: Data format describing Gateway operation status
---

# HTTP: Gateway status

```
{
  "$schema": "https://json-schema.org/draft/2019-09/schema",
  "$id": "http://ruuvi.com/schemas/ruuvi_http_stat.schema.json",
  "title": "Status of Gateway",
  "type": "object",
  "required": [
    "DEVICE_ADDR",
    "ESP_FW",
    "NRF_FW",
    "UPTIME",
    "NONCE",
    "CONNECTION",
    "NUM_CONN_LOST",
    "SENSORS_SEEN",
    "ACTIVE_SENSORS",
    "INACTIVE_SENSORS"
  ],
  "properties": {
    "DEVICE_ADDR": {
      "title": "MAC-address of Gateway",
      "type": "string",
      "examples": [
        "C8:25:2D:8E:9C:2C"
      ]
    },
    "ESP_FW": {
      "title": "Firmware version of Gateway",
      "type": "string",
      "examples": [
        "v1.11.2"
      ]
    },
    "NRF_FW": {
      "title": "Firmware version of NRF52 co-processor",
      "type": "string",
      "examples": [
        "v0.7.2"
      ]
    },
    "UPTIME": {
      "title": "Gateway uptime counter (seconds)",
      "type": "string",
      "examples": [
        "11"
      ]
    },
    "NONCE": {
      "title": "Nonce - sequentially incremented number for each message, the initial value of which is set randomly",
      "type": "string",
      "examples": [
        "2821115890"
      ]
    },
    "CONNECTION": {
      "title": "Network connection type",
      "type": "string",
      "pattern": "^(WIFI|ETHERNET)$",
      "examples": [
        "WIFI",
        "ETH"
      ]
    },
    "NUM_CONN_LOST": {
      "title": "Network connection loss counter",
      "type": "string",
      "examples": [
        "0"
      ]
    },
    "SENSORS_SEEN": {
      "title": "Number of Bluetooth-sensors this Gateway has seen",
      "type": "string",
      "examples": [
        "4"
      ]
    },
    "ACTIVE_SENSORS": {
      "type": "array",
      "title": "List of active Bluetooth-sensors",
      "items": {
        "type": "object",
        "title": "Status of active Bluetooth-sensor",
        "required": [
          "MAC",
          "COUNTER"
        ],
        "properties": {
          "MAC": {
            "title": "MAC-address of Bluetooth-sensor",
            "type": "string",
            "pattern": "^([0-9A-Fa-f]{2}[:-]){5}([0-9A-Fa-f]{2})$",
            "examples": [
              "E3:75:CF:37:4E:23",
              "C6:A5:B9:E0:AD:06"
            ]
          },
          "COUNTER": {
            "title": "Counter of messages, received from this Bluetooth-sensor",
            "type": "string",
            "examples": [
              "5"
            ]
          }
        }
      },
      "examples": [
        [],
        [
          {
            "MAC": "E3:75:CF:37:4E:23",
            "COUNTER": "5"
          },
          {
            "MAC": "C6:A5:B9:E0:AD:06",
            "COUNTER": "4"
          }
        ]
      ]
    },
    "INACTIVE_SENSORS": {
      "title": "List of inactive Bluetooth-sensors",
      "type": "array",
      "items": {
        "title": "MAC-address of inactive Bluetooth-sensor",
        "type": "string",
        "pattern": "^([0-9A-Fa-f]{2}[:-]){5}([0-9A-Fa-f]{2})$",
        "examples": [
          "F4:C6:46:2C:3E:B4"
        ]
      },
      "examples": [
        [],
        [
          "F4:1F:0C:28:CB:D6"
        ],
        [
          "F4:1F:0C:28:CB:D6",
          "F4:C6:46:2C:3E:B4"
        ]
      ]
    }
  },
  "examples": [
    {
      "DEVICE_ADDR": "C8:25:2D:8E:9C:2C",
      "ESP_FW": "v1.11.2",
      "NRF_FW": "v0.7.2",
      "UPTIME": "11",
      "NONCE": "2821115890",
      "CONNECTION": "WIFI",
      "NUM_CONN_LOST": "0",
      "SENSORS_SEEN": "4",
      "ACTIVE_SENSORS": [
        {
          "MAC": "E3:75:CF:37:4E:23",
          "COUNTER": "5"
        },
        {
          "MAC": "C6:A5:B9:E0:AD:06",
          "COUNTER": "4"
        }
      ],
      "INACTIVE_SENSORS": [
        "F4:1F:0C:28:CB:D6",
        "F4:C6:46:2C:3E:B4"
      ]
    }
  ]
}

```
