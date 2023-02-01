---
description: Data format describing Gateway operation status
---

# HTTP: Gateway status

The JSON data format description is provided in JSON schema format ([https://json-schema.org](https://json-schema.org)), which provides clear human- and machine-readable documentation with examples:

```json
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
    "RESET_REASON",
    "RESET_CNT",
    "RESET_INFO",
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
    "RESET_REASON": {
      "title": "ESP32 reset reason",
      "type": "string",
      "examples": [
        "POWER_ON",
        "SW",
        "PANIC",
        "INT_WDT",
        "TASK_WDT",
        "WDT",
        "BROWNOUT"
      ]
    },
    "RESET_CNT": {
      "title": "Number of restarts after power on",
      "type": "string",
      "examples": [
        "1",
        "2",
        "10"
      ]
    },
    "RESET_INFO": {
      "title": "A description of the cause of the software-caused reboot",
      "type": "string",
      "examples": [
        "",
        "Reset by software: Network watchdog",
        "Reset by software: Low memory",
        "Reset by software: Restart the system after firmware update (failed)",
        "Reset by software: Restart the system after firmware update (auto-updating failed)",
        "Reset by software: Restart the system after firmware update (manual updating via WiFi hotspot failed)",
        "Reset by software: Restart the system after firmware update (manual updating via LAN failed)",
        "Reset by software: Restart the system after firmware update (completed successfully)",
        "Reset by software: Restart the system after firmware update (auto-updating completed successfully)",
        "Reset by software: Restart the system after firmware update (manual updating via WiFi hotspot completed successfully",
        "Reset by software: Restart the system after firmware update (manual updating via LAN completed successfully)",
        "Reset by software: Rollback firmware",
        "Reset by software: The CONFIGURE button has been released - restart system",
        "Reset by software: System restart is activated by the Configure button",
        "Reset by panic: Guru Meditation Error: Core  0 panic'ed (InstrFetchProhibited). Exception was unhandled.\r\n\r\nCore  0 register dump:\r\nPC      : 0xffffffff  PS      : 0x00060930  A0      : 0x800e9948  A1      : 0x3ffc22a0  \r\nA2      : 0xffffffff  A3      : 0x3ffafe48  A4      : 0x3ffafe48  A5      : 0x3ffc2344  \r\nA6      : 0x000000a5  A7      : 0x00060023  A8      : 0x800e93c3  A9      : 0x3ffb98a8  \r\nA10     : 0x00000000  A11     : 0x3f40ddb0  A12     : 0x3f40d814  A13     : 0xf6e515dd  \r\nA14     : 0x3ffc2250  A15     : 0x3ffafe48  SAR     : 0x00000004  EXCCAUSE: 0x00000014  \r\nEXCVADDR: 0xfffffffc  LBEG    : 0x400014fd  LEND    : 0x4000150d  LCOUNT  : 0xfffffffe  \r\n\r\nBacktrace:0x7ffffffc:0x3ffc22a0 0x400e9945:0x3ffc22f0 0x400e9a24:0x3ffc2330 0x400d8f24:0x3ffc2370 0x400d55db:0x3ffc23c0 0x4008ae1e:0x3ffc23f0\r\n\r\n\r\nELF file SHA256: f993cfd8dbfd7c9c\r\n\r\nRebooting...\r\n"
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
      "RESET_REASON": "POWER_ON",
      "RESET_CNT":    "1",
      "RESET_INFO":   "",
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
    },
    {
      "DEVICE_ADDR":  "C8:25:2D:8E:9C:2C",
      "ESP_FW":       "v1.12.4-26-g42d064a-dirty",
      "NRF_FW":       "v1.0.0",
      "UPTIME":       "11",
      "NONCE":        "3375691106",
      "CONNECTION":   "ETHERNET",
      "NUM_CONN_LOST":        "0",
      "RESET_REASON": "PANIC",
      "RESET_CNT":    "3",
      "RESET_INFO":   "Reset by panic: Guru Meditation Error: Core  0 panic'ed (InstrFetchProhibited). Exception was unhandled.\r\n\r\nCore  0 register dump:\r\nPC      : 0xffffffff  PS      : 0x00060930  A0      : 0x800e9948  A1      : 0x3ffc22a0  \r\nA2      : 0xffffffff  A3      : 0x3ffafe48  A4      : 0x3ffafe48  A5      : 0x3ffc2344  \r\nA6      : 0x000000a5  A7      : 0x00060023  A8      : 0x800e93c3  A9      : 0x3ffb98a8  \r\nA10     : 0x00000000  A11     : 0x3f40ddb0  A12     : 0x3f40d814  A13     : 0xf6e515dd  \r\nA14     : 0x3ffc2250  A15     : 0x3ffafe48  SAR     : 0x00000004  EXCCAUSE: 0x00000014  \r\nEXCVADDR: 0xfffffffc  LBEG    : 0x400014fd  LEND    : 0x4000150d  LCOUNT  : 0xfffffffe  \r\n\r\nBacktrace:0x7ffffffc:0x3ffc22a0 0x400e9945:0x3ffc22f0 0x400e9a24:0x3ffc2330 0x400d8f24:0x3ffc2370 0x400d55db:0x3ffc23c0 0x4008ae1e:0x3ffc23f0\r\n\r\n\r\nELF file SHA256: f993cfd8dbfd7c9c\r\n\r\nRebooting...\r\n",
      "SENSORS_SEEN": "0",
      "ACTIVE_SENSORS":       [],
      "INACTIVE_SENSORS":     []
    },
    {
      "DEVICE_ADDR":  "C8:25:2D:8E:9C:2C",
      "ESP_FW":       "v1.12.4-27-g65c58ac-dirty",
      "NRF_FW":       "v1.0.0",
      "UPTIME":       "10",
      "NONCE":        "1537622823",
      "CONNECTION":   "ETHERNET",
      "NUM_CONN_LOST":        "0",
      "RESET_REASON": "SW",
      "RESET_CNT":    "2",
      "RESET_INFO":   "Reset by software: Low memory",
      "SENSORS_SEEN": "0",
      "ACTIVE_SENSORS":       [],
      "INACTIVE_SENSORS":     []
    }
  ]
}

```
