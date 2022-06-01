---
description: >-
  This format is used for creating custom default configuration
  (gw_cfg_default.json), when the configuration is read or saved from/to Gateway
  by HTTP.
---

# Gateway configuration

```
{
  "$schema": "https://json-schema.org/draft/2019-09/schema",
  "$id": "http://ruuvi.com/schemas/ruuvi_gw_cfg.schema.json",
  "title": "Ruuvi gateway configuration",
  "type": "object",
  "required": [
  ],
  "properties": {
    "wifi_sta_config": {
      "title": "Wi-Fi credentials",
      "description": "Gateway will connect to the specified WiFi SSID if it's not empty. Note: 'use_eth' should be 'false'",
      "type": "object",
      "required": [
        "ssid",
        "password"
      ],
      "properties": {
        "ssid": {
          "type": "string",
          "title": "WiFi network name (SSID)",
          "examples": [
            "",
            "MyWiFi_123"
          ]
        },
        "password": {
          "type": "string",
          "title": "WiFi password",
          "examples": [
            "",
            "my_password"
          ]
        }
      },
      "examples": [
        {
          "ssid": "",
          "password": ""
        },
        {
          "ssid": "MyWiFi_123",
          "password": "my_password"
        }
      ]
    },
    "wifi_ap_config": {
      "title": "WiFi access point default settings",
      "type": "object",
      "required": [
        "password"
      ],
      "properties": {
        "password": {
          "type": "string",
          "default": "",
          "title": "Default password for connecting to RuuviGatewayXXXX access point",
          "examples": [
            "",
            "12345678"
          ]
        }
      }
    },
    "use_eth": {
      "title": "Network connection type: Ethernet/WiFi",
      "type": "boolean"
    },
    "eth_dhcp": {
      "title": "IP configuration mode (DHCP/manual) when connected via Ethernet",
      "type": "boolean",
      "default": true
    },
    "eth_static_ip": {
      "title": "Manual IP configuration: IP address",
      "type": "string"
    },
    "eth_netmask": {
      "title": "Manual IP configuration: Subnet mask",
      "type": "string"
    },
    "eth_gw": {
      "title": "Manual IP configuration: Network gateway IP address",
      "type": "string"
    },
    "eth_dns1": {
      "title": "Manual IP configuration: IP address of DNS server1",
      "type": "string"
    },
    "eth_dns2": {
      "title": "Manual IP configuration: IP address of DNS server2",
      "type": "string"
    },
    "remote_cfg_use": {
      "title": "Enable automatic downloading of Gateway configuration from a remote server",
      "type": "boolean",
      "default": false
    },
    "remote_cfg_url": {
      "title": "URL of the remote server for automatic Gateway configuration downloading",
      "type": "string"
    },
    "remote_cfg_auth_type": {
      "title": "HTTP authentication credentials for the remote server for automatic Gateway configuration downloading",
      "description": "It should not be empty if 'remote_cfg_use' is 'true'",
      "type": "string",
      "pattern": "^(|no|basic|bearer)$",
      "default": "",
      "examples": [
        "",
        "no",
        "basic",
        "bearer"
      ]
    },
    "remote_cfg_auth_bearer_token": {
      "title": "A token for HTTP bearer authentication for the remote server for automatic Gateway configuration downloading",
      "type": "string"
    },
    "remote_cfg_auth_basic_user": {
      "title": "Username for HTTP basic authentication for the remote server for automatic Gateway configuration downloading",
      "type": "string"
    },
    "remote_cfg_auth_basic_pass": {
      "title": "Password for HTTP basic authentication for the remote server for automatic Gateway configuration downloading",
      "type": "string"
    },
    "remote_cfg_refresh_interval_minutes": {
      "title": "Period for checking a new gateway configuration on the remote server (in minutes)",
      "type": "integer"
    },
    "use_http": {
      "title": "Enable HTTP relaying mode",
      "type": "boolean",
      "default": true
    },
    "http_url": {
      "title": "URL of the server to which the data collected from Bluetooth-sensors will be sent",
      "type": "string",
      "default": "https://network.ruuvi.com/record",
      "examples": [
        "https://network.ruuvi.com/record",
        "http://my_server123.com:8080/record"
      ]
    },
    "http_user": {
      "title": "Username for HTTP basic authentication for the server",
      "type": "string",
      "default": ""
    },
    "http_pass": {
      "title": "Password for HTTP basic authentication for the server",
      "type": "string",
      "default": ""
    },
    "use_http_stat": {
      "title": "Enable sending Gateway status to the HTTP-server",
      "type": "boolean",
      "default": true
    },
    "http_stat_url": {
      "title": "URL of the server to which the gateway status will be sent",
      "type": "string",
      "default": "https://network.ruuvi.com/status",
      "examples": [
        "https://network.ruuvi.com/status",
        "http://my_server123.com:8080/status"
      ]
    },
    "http_stat_user": {
      "title": "Username for HTTP basic authentication for the server",
      "type": "string",
      "default": ""
    },
    "http_stat_pass": {
      "title": "Password for HTTP basic authentication for the server",
      "type": "string",
      "default": ""
    },
    "use_mqtt": {
      "title": "Enable MQTT relaying mode",
      "type": "boolean",
      "default": false
    },
    "mqtt_transport": {
      "title": "MQTT transport type to use",
      "description": "TCP - MQTT over TCP, SSL - MQTT over SSL, WS - MQTT over WebSockets, WSS - MQTT over secure WebSockets",
      "type": "string",
      "pattern": "^(TCP|SSL|WS|WSS)$",
      "default": "TCP",
      "examples": [
        "TCP",
        "SSL",
        "WS",
        "WSS"
      ]
    },
    "mqtt_server": {
      "title": "MQTT server address",
      "type": "string",
      "examples": [
        "test.mosquitto.org"
      ]
    },
    "mqtt_port": {
      "title": "MQTT server port",
      "type": "integer",
      "default": 1883,
      "examples": [
        1883,
        8886,
        8080,
        8081
      ]
    },
    "mqtt_prefix": {
      "title": "MQTT topic prefix",
      "description": "Full MQTT topic is formed by joining the prefix and Bluetooth-sensor's MAC-address. If 'mqtt_prefix' is empty, then default prefix is used: 'ruuvi/<gateway_MAC_address>/'",
      "type": "string",
      "default": "",
      "examples": [
        "ruuvi/C8:25:2D:8E:9C:2C/"
      ]
    },
    "mqtt_client_id": {
      "title": "MQTT client ID",
      "description": "If 'mqtt_client_id' is empty, then default client ID is used: '<gateway_MAC_address>'",
      "type": "string",
      "default": "",
      "examples": [
        "",
        "C8:25:2D:8E:9C:2C",
        "my_mqtt_client1"
      ]
    },
    "mqtt_user": {
      "title": "User name for MQTT authentication",
      "type": "string",
      "default": ""
    },
    "mqtt_pass": {
      "title": "Password for MQTT authentication",
      "type": "string",
      "default": ""
    },
    "lan_auth_type": {
      "title": "Configuring the authentication type when accessing Gateway from LAN",
      "description": "'lan_auth_default' - Ruuvi-authentication with username 'Admin' and as a password the Unique ID is used (in format XX:XX:XX:XX:XX:XX:XX:XX) which is printed on the bottom of the Ruuvi Gateway. 'lan_auth_ruuvi' - Ruuvi-authentication, login/password should be specified in 'lan_auth_user' and 'lan_auth_pass'. 'lan_auth_deny' - deny access from LAN. 'lan_auth_allow' - allow access from LAN without a password. 'lan_auth_basic' - HTTP basic authentication, login/password should be specified in 'lan_auth_user' and 'lan_auth_pass'. 'lan_auth_digest' - HTTP digest authentication, login/password should be specified in 'lan_auth_user' and 'lan_auth_pass'.",
      "type": "string",
      "pattern": "^(lan_auth_default|lan_auth_ruuvi|lan_auth_deny|lan_auth_allow|lan_auth_basic|lan_auth_digest)$",
      "default": "lan_auth_default",
      "examples": [
        "lan_auth_default",
        "lan_auth_ruuvi",
        "lan_auth_deny",
        "lan_auth_allow",
        "lan_auth_basic",
        "lan_auth_digest"
      ]
    },
    "lan_auth_user": {
      "title": "Login for authentication when accessing from LAN",
      "type": "string",
      "default": "Admin",
      "examples": [
        "Admin"
      ]
    },
    "lan_auth_pass": {
      "title": "Password for authentication when accessing from LAN",
      "type": "string"
    },
    "lan_auth_api_key": {
      "title": "API key (token) for HTTP bearer authentication when accessing from LAN",
      "description": "If 'lan_auth_api_key' is empty, then bearer authentication is disabled.",
      "type": "string",
      "default": "",
      "examples": [
        "304uOrJMoCNEVaPaXswV9U1qRDPZFbl0V2x7OXHM5nw="
      ]
    },
    "auto_update_cycle": {
      "title": "Configure firmware auto-updating rules.",
      "description": "'regular' - check for updates 1-2 times a day according to the schedule, install new versions only 2 weeks after release. 'beta' - install new versions as soon as a new version is released. 'manual' - do not check for firmware updates and do not install updates automatically",
      "type": "string",
      "pattern": "^(regular|beta|manual)$",
      "default": "regular",
      "examples": [
        "regular",
        "beta",
        "manual"
      ]
    },
    "auto_update_weekdays_bitmask": {
      "title": "Configure firmware auto-updating schedule: specify weekdays",
      "description": "Bit-mask for weekdays: bit 0 - Sunday, bit 1 - Monday, ..., bit 6 - Saturday",
      "type": "integer",
      "default": 127,
      "examples": [
        1,
        3,
        127
      ]
    },
    "auto_update_interval_from": {
      "title": "Configure firmware auto-updating schedule: start time (local timezone)",
      "description": "0 - 00:00, 1 - 01:00, 2 - 02:00, ..., 23 - 23:00",
      "type": "integer",
      "default": 0,
      "examples": [
        0,
        1,
        23
      ]
    },
    "auto_update_interval_to": {
      "title": "Configure firmware auto-updating schedule: end time (local timezone)",
      "description": "1 - 01:00, 2 - 02:00, ..., 24 - 24:00",
      "type": "integer",
      "default": 24,
      "examples": [
        1,
        23,
        24
      ]
    },
    "auto_update_tz_offset_hours": {
      "title": "Configure firmware auto-updating schedule: local timezone offset (hours)",
      "type": "integer",
      "default": 3,
      "examples": [
        3
      ]
    },
    "ntp_use": {
      "title": "Enable time synchronization from NTP servers",
      "type": "boolean",
      "default": true
    },
    "ntp_use_dhcp": {
      "title": "Use DHCP to get the list of NTP servers",
      "type": "boolean",
      "default": false
    },
    "ntp_server1": {
      "title": "Address of NTP server 1 (used only if 'ntp_use_dhcp' is false).",
      "type": "string",
      "default": "time.google.com",
      "examples": [
        "time.google.com"
      ]
    },
    "ntp_server2": {
      "title": "Address of NTP server 2 (used only if 'ntp_use_dhcp' is false).",
      "type": "string",
      "default": "time.cloudflare.com",
      "examples": [
        "time.cloudflare.com"
      ]
    },
    "ntp_server3": {
      "title": "Address of NTP server 3 (used only if 'ntp_use_dhcp' is false).",
      "type": "string",
      "default": "time.nist.gov",
      "examples": [
        "time.nist.gov"
      ]
    },
    "ntp_server4": {
      "title": "Address of NTP server 4 (used only if 'ntp_use_dhcp' is false).",
      "type": "string",
      "default": "pool.ntp.org",
      "examples": [
        "pool.ntp.org"
      ]
    },
    "company_use_filtering": {
      "title": "Enable filtering messages from Bluetooth-sensors by company ID.",
      "type": "boolean",
      "default": true
    },
    "company_id": {
      "title": "Company ID for filtering messages from Bluetooth-sensors.",
      "type": "integer",
      "default": 1177,
      "examples": [
        1177
      ]
    },
    "scan_coded_phy": {
      "title": "Configure Bluetooth scanning: Use coded PHY (long range)",
      "type": "boolean",
      "default": false
    },
    "scan_1mbit_phy": {
      "title": "Configure Bluetooth scanning: Use Use 1 MBit/s PHY",
      "type": "boolean",
      "default": true
    },
    "scan_extended_payload": {
      "title": "Configure Bluetooth scanning: Use extended payload",
      "type": "boolean",
      "default": true
    },
    "scan_channel_37": {
      "title": "Configure Bluetooth scanning: Use channel 37",
      "type": "boolean",
      "default": true
    },
    "scan_channel_38": {
      "title": "Configure Bluetooth scanning: Use channel 38",
      "type": "boolean",
      "default": true
    },
    "scan_channel_39": {
      "title": "Configure Bluetooth scanning: Use channel 39",
      "type": "boolean",
      "default": true
    },
    "coordinates": {
      "title": "GPS-coordinates of the Gateway",
      "type": "string",
      "default": "",
      "examples": [
        ""
      ]
    }
  },
  "examples": [
    {
      "wifi_sta_config": {
        "ssid": "",
        "password": ""
      },
      "wifi_ap_config": {
        "password": ""
      },
      "use_eth": false,
      "eth_dhcp": true,
      "eth_static_ip": "",
      "eth_netmask": "",
      "eth_gw": "",
      "eth_dns1": "",
      "eth_dns2": "",
      "remote_cfg_use": false,
      "remote_cfg_url": "",
      "remote_cfg_auth_type": "no",
      "remote_cfg_auth_bearer_token": "",
      "remote_cfg_auth_basic_user": "",
      "remote_cfg_auth_basic_pass": "",
      "remote_cfg_refresh_interval_minutes": 0,
      "use_http": true,
      "http_url": "https://network.ruuvi.com/record",
      "http_user": "",
      "http_pass": "",
      "use_http_stat": true,
      "http_stat_url": "https://network.ruuvi.com/status",
      "http_stat_user": "",
      "http_stat_pass": "",
      "use_mqtt": false,
      "mqtt_transport": "TCP",
      "mqtt_server": "test.mosquitto.org",
      "mqtt_port": 1883,
      "mqtt_prefix": "",
      "mqtt_client_id": "",
      "mqtt_user": "",
      "mqtt_pass": "",
      "lan_auth_type": "lan_auth_default",
      "lan_auth_user": "Admin",
      "lan_auth_api_key": "",
      "auto_update_cycle": "regular",
      "auto_update_weekdays_bitmask": 127,
      "auto_update_interval_from": 0,
      "auto_update_interval_to": 24,
      "auto_update_tz_offset_hours": 3,
      "ntp_use": true,
      "ntp_use_dhcp": false,
      "ntp_server1": "time.google.com",
      "ntp_server2": "time.cloudflare.com",
      "ntp_server3": "time.nist.gov",
      "ntp_server4": "pool.ntp.org",
      "company_use_filtering": true,
      "company_id": 1177,
      "scan_coded_phy": false,
      "scan_1mbit_phy": true,
      "scan_extended_payload": true,
      "scan_channel_37": true,
      "scan_channel_38": true,
      "scan_channel_39": true,
      "coordinates": ""
    }
  ]
}

```
