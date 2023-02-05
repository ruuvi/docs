# GW ESP32 WiFi Hotspot

The Gateway provides a WiFi hotspot for configuration. The hotspot has SSID with the name "**Configure Ruuvi Gateway ABCD**" where ABCD is the last 2 bytes of the gateway WiFi MAC address. No password is required to connect to the gateway's hotspot.&#x20;

The WiFi hotspot is only active if the gateway is not configured or within one minute after pressing the Configuration button. After the configuration of the gateway is complete, WiFi credentials are stored to flash and the hotspot is turned off. If the Internet connection is lost later, connection loss is indicated by "Red LED" but the hotspot is not turned back on unless the user enters configuration mode by pressing the Configuration button.

The gateway can be partially reconfigured over LAN (network configuration can't be changed in this case). Also following pages are available through LAN connection: /metrics and /history.

{% hint style="info" %}
If Ethernet cable is connected to an unconfigured gateway, then after one minute the gateway will automatically be set to the default configuration with Ethernet connection mode and the Wi-Fi hotspot will be deactivated. After that, the user can activate the hotspot with a short press on the "Configure" button or reset the configuration with a long press on the "Configure" button.
{% endhint %}

## API

The gateway is reachable at http://10.10.0.1 once a client has connected to the hotspot.&#x20;

### Encrypted data format

Sensitive data (containing passwords) is transmitted in encrypted form. The format for transmitting encrypted data is as follows (JSON):

| Attribute name | Description                                             |
| -------------- | ------------------------------------------------------- |
| **encrypted**  | Encrypted data, encoded as **Base64**                   |
| **iv**         | AES-256 initialization vector, encoded as **Base64**    |
| **hash**       | SHA-256 hash of unencrypted data, encoded as **Base64** |

Example of encrypted data:

{% code overflow="wrap" %}
```json
{"encrypted":"hbLi8K0CHELrvI0/4gO7n3E5KY5wtbmUSwM67oY6ZhzZNPIGBhHLE8CYeDuVL+FiU/K5vAO1EC+uEm/gw4LkaSE1sZbsGUGyDFelnEOlhQYQf6rGxlQYu+9xrzPhUv97tezkrPPesSy0tgea3QAmuQRPX628X0AP0OxUxE4kBh8guYKIXPYOf9EH0fUskvt/98B8p630mu66miiQfsONsxFWVX7GcUN5u1soYKdZXd9HQGVACEgl6oZ2Vxqf4JmtNgdsmWxYTmIOi1ySq4DtqtL5vfdzN1BMep0cHkgGAeMBQt6i9H5mhBZ8PnJzjvFcuolwsRG3rQTX9wRCXikjag==","iv":"I+CylR3OlmEWr127RC084w==","hash":"ADUJpequznSV9HyqkMLrj2NPhViJQa6YDdbkEDExajk="}
```
{% endcode %}

The data is encrypted using **AES-256-CBC**. **ECDH** protocol is used to establish a shared secret between the client and the Gateway, then **SHA-256** hash is calculated for the shared secret to generate AES encryption key.

To establish a shared secret, the client must perform **`GET`**` ``/ruuvi.json` request and pass its public encryption key in the HTTP header "**ruuvi\_ecdh\_pub\_key**" (Base64 encoded):

```
GET /ruuvi.json?_=1661226324528 HTTP/1.1
Host: 10.10.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:103.0) Gecko/20100101 Firefox/103.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
ruuvi_ecdh_pub_key: BPtMzls7i0PyOu75EPzw2OaTJscwGnrnOW7mK58pfJ6Egg9/tV5cJFVz6euHGp7x4ZXj5s0hTiotrtE0qJLczMA=
X-Requested-With: XMLHttpRequest
Connection: keep-alive
Referer: http://10.10.0.1/
```

In response, the Gateway returns its public encryption key in the HTTP header "**ruuvi\_ecdh\_pub\_key**" (Base64 encoded):

```
HTTP/1.1 200 OK
Server: Ruuvi Gateway
Date: Tue, 23 Aug 2022 03:45:27 GMT
Content-type: application/json; charset=utf-8
Content-Length: 1514
ruuvi_ecdh_pub_key: BGJXeeiqH7JPCdO3wRZgSdrcJb2EtSAVUQwr/RfeJmGxIrXuw8mTW2517RCn8pgfBwDnRWCnL9JYdvQkbf+goZQ=
Cache-Control: no-store, no-cache, must-revalidate, max-age=0
Pragma: no-cache
```

The client needs to compute a shared secret using its private encryption key and the Gateway's public key, then calculate SHA-256 for the shared secret to get the AES encryption key (_**AES\_K**_).

To encrypt the data before sending it, the client must randomly generate a 16-byte initialization vector (_**IV**_) for AES encryption, then encrypt the data using parameters _**IV**_ and _**AES\_K**_. The data is validated using a SHA-256 hash, which is passed as part of JSON. All values in JSON are encoded by Base64.

To decrypt the data received from the Gateway, the client needs to decode all values in JSON from Base64 encoding, then get the _**IV**_ from the "**iv**" attribute of the received JSON. After that, decrypt the data in the "**encrypted**" attribute using the _**IV**_ and _**AES\_K**_. And finally, calculate the SHA-256 hash for the decrypted data and check if it matches the "**hash**" attribute in JSON.



These API calls are available:

{% swagger method="get" path="" baseUrl="http://10.10.0.1/ruuvi.json" summary="Requesting gateway configuration and performing encryption keys exchange" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="header" name="ruuvi_ecdh_pub_key" required="true" %}
The client's public encryption key in Base64 encoding.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Encrypted gateway configuration." %}
The Gateway's public encryption key is passed in HTTP header "**ruuvi\_ecdh\_pub\_key**" in Base64 encoding. The data is sent in an encrypted form (see [#undefined](gw-esp32-wifi-hotspot.md#undefined "mention")).&#x20;

Here is unencrypted data:

```json
{
        "fw_ver":       "v1.12.2",
        "nrf52_fw_ver": "v0.7.2",
        "gw_mac":       "C8:25:2D:8E:9C:2C",
        "wifi_sta_config":      {
                "ssid": ""
        },
        "wifi_ap_config":       {
                "channel":      1
        },
        "use_eth":      true,
        "eth_dhcp":     true,
        "eth_static_ip":        "",
        "eth_netmask":  "",
        "eth_gw":       "",
        "eth_dns1":     "",
        "eth_dns2":     "",
        "remote_cfg_use":       false,
        "remote_cfg_url":       "",
        "remote_cfg_auth_type": "no",
        "remote_cfg_refresh_interval_minutes":  0,
        "use_http":     true,
        "http_url":     "https://network.ruuvi.com/record",
        "http_user":    "",
        "use_http_stat":        true,
        "http_stat_url":        "https://network.ruuvi.com/status",
        "http_stat_user":       "",
        "use_mqtt":     false,
        "mqtt_transport":       "TCP",
        "mqtt_server":  "test.mosquitto.org",
        "mqtt_port":    1883,
        "mqtt_prefix":  "ruuvi/C8:25:2D:8E:9C:2C/",
        "mqtt_client_id":       "C8:25:2D:8E:9C:2C",
        "mqtt_user":    "",
        "lan_auth_type":        "lan_auth_default",
        "lan_auth_user":        "Admin",
        "lan_auth_api_key_use": false,
        "auto_update_cycle":    "regular",
        "auto_update_weekdays_bitmask": 127,
        "auto_update_interval_from":    0,
        "auto_update_interval_to":      24,
        "auto_update_tz_offset_hours":  3,
        "ntp_use":      true,
        "ntp_use_dhcp": false,
        "ntp_server1":  "time.google.com",
        "ntp_server2":  "time.cloudflare.com",
        "ntp_server3":  "time.nist.gov",
        "ntp_server4":  "pool.ntp.org",
        "company_id":   1177,
        "company_use_filtering":        true,
        "scan_coded_phy":       false,
        "scan_1mbit_phy":       true,
        "scan_extended_payload":        true,
        "scan_channel_37":      true,
        "scan_channel_38":      true,
        "scan_channel_39":      true,
        "coordinates":  ""
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="" baseUrl="http://10.10.0.1/ruuvi.json" summary="Save network configuration" %}
{% swagger-description %}
The same endpoint "/ruuvi.json" is used for saving the network configuration and gateway configuration. If the passed JSON data contains the "use\_eth" attribute, then the network part of the configuration will be updated. Otherwise, the gateway configuration will be set.

The data must be sent in an encrypted form (see [#encrypted-data-format](gw-esp32-wifi-hotspot.md#encrypted-data-format "mention")). Here is the unencrypted data:&#x20;
{% endswagger-description %}

{% swagger-parameter in="body" name="use_eth" type="Bool" required="true" %}
Use Ethernet if True, otherwise use Wi-Fi
{% endswagger-parameter %}

{% swagger-parameter in="body" name="eth_dhcp" type="Bool" %}
Use DHCP for Ethernet connection
{% endswagger-parameter %}

{% swagger-parameter in="body" name="eth_static_ip" %}
Static IP address (when Ethernet is used and DHCP disabled)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="eth_netmask" %}
Netmask (when Ethernet is used and DHCP disabled)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="eth_gw" %}
IP address of gateway (when Ethernet is used and DHCP disabled)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="eth_dns1" %}
IP address of DNS1 (when Ethernet is used and DHCP disabled)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="eth_dns2" %}
IP address of DNS2 (when Ethernet is used and DHCP disabled)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="wifi_ap_config" type="Object" %}
Set parameters for Wi-Fi AP. The attribute "channel" allows configuring the Wi-Fi channel.
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

Example:

```json
{"use_eth":true,"eth_dhcp":true}
```

Example:

```json
{"use_eth":false,"wifi_ap_config":{"channel":11}}
```

{% swagger method="post" path="" baseUrl="http://10.10.0.1/ruuvi.json" summary="Save gateway configuration" %}
{% swagger-description %}
The same endpoint "/ruuvi.json" is used for saving the network configuration and gateway configuration. If the passed JSON data contains the "use\_eth" attribute, then the network part of the configuration will be updated. Otherwise, the gateway configuration will be set.

The data must be sent in an encrypted form (see [#encrypted-data-format](gw-esp32-wifi-hotspot.md#encrypted-data-format "mention")). Here is the unencrypted data:&#x20;
{% endswagger-description %}

{% swagger-parameter in="body" name="remote_cfg_use" type="Bool" %}
If true, then download the configuration from the remote server, specified in "

**remote_cfg_url**

"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="remote_cfg_url" %}
URL of the remote server to download the configuration
{% endswagger-parameter %}

{% swagger-parameter in="body" name="remote_cfg_auth_type" %}
Authentication type: "no", "basic" or "bearer"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="remote_cfg_auth_basic_user" %}
Username for "basic" authentication
{% endswagger-parameter %}

{% swagger-parameter in="body" name="remote_cfg_auth_basic_pass" %}
Password for "basic" authentication
{% endswagger-parameter %}

{% swagger-parameter in="body" name="remote_cfg_auth_bearer_token" %}
Bearer token for bearer authentication
{% endswagger-parameter %}

{% swagger-parameter in="body" name="use_http" type="Bool" %}
If true, then send data to the cloud via HTTP(S)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="http_url" %}
URL of the cloud server
{% endswagger-parameter %}

{% swagger-parameter in="body" name="http_user" %}
Username
{% endswagger-parameter %}

{% swagger-parameter in="body" name="http_pass" %}
Password
{% endswagger-parameter %}

{% swagger-parameter in="body" name="use_http_stat" type="Bool" %}
If true, then send statistics to the cloud via HTTP(S)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="http_stat_url" %}
URL of the cloud statistrics server
{% endswagger-parameter %}

{% swagger-parameter in="body" name="http_stat_user" %}
Username
{% endswagger-parameter %}

{% swagger-parameter in="body" name="http_stat_pass" %}
Password
{% endswagger-parameter %}

{% swagger-parameter in="body" name="use_mqtt" type="Bool" %}
If true, then send data to the cloud via MQTT(S)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mqtt_transport" %}
MQTT transport: "TCP", "SSL", "WS" or "WSS"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mqtt_server" %}
IP address of MQTT server
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mqtt_port" type="Int" %}
TCP/IP port of MQTT server
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mqtt_prefix" %}
MQTT prefix
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mqtt_client_id" %}
MQTT client ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mqtt_user" %}
Username for MQTT authentication
{% endswagger-parameter %}

{% swagger-parameter in="body" name="mqtt_pass" %}
Password for MQTT authentication
{% endswagger-parameter %}

{% swagger-parameter in="body" name="lan_auth_api_key" %}
Bearer key for authentication when accessing the Gateway from LAN
{% endswagger-parameter %}

{% swagger-parameter in="body" name="company_use_filtering" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="scan_coded_phy" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="scan_1mbit_phy" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="scan_extended_payload" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="scan_channel_37" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="scan_channel_38" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="scan_channel_39" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="auto_update_cycle" %}
"regular", "beta" or "manual"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="auto_update_weekdays_bitmask" type="Int" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="auto_update_interval_from" type="Int" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="auto_update_interval_to" type="Int" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="auto_update_tz_offset_hours" type="Int" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="ntp_use" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="ntp_use_dhcp" type="Bool" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="ntp_server1" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="ntp_server2" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="ntp_server3" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="ntp_server4" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

Example:

```json
{
  "remote_cfg_use":false,
  "remote_cfg_url":"",
  "remote_cfg_auth_type":"no",
  "use_http":true,
  "http_url":"https://network.ruuvi.com/record",
  "http_user":"",
  "http_pass":"",
  "use_http_stat":true,
  "http_stat_url":"https://network.ruuvi.com/status",
  "http_stat_user":"",
  "http_stat_pass":"",
  "use_mqtt":false,
  "mqtt_transport":"TCP",
  "mqtt_server":"test.mosquitto.org",
  "mqtt_port":1883,
  "mqtt_prefix":"ruuvi/C8:25:2D:8E:9C:2C/",
  "mqtt_client_id":"C8:25:2D:8E:9C:2C",
  "mqtt_user":"",
  "mqtt_pass":"",
  "lan_auth_api_key":"",
  "company_use_filtering":true,
  "scan_coded_phy":false,
  "scan_1mbit_phy":true,
  "scan_extended_payload":true,
  "scan_channel_37":true,
  "scan_channel_38":true,
  "scan_channel_39":true,
  "auto_update_cycle":"manual",
  "auto_update_weekdays_bitmask":127,
  "auto_update_interval_from":0,
  "auto_update_interval_to":24,
  "auto_update_tz_offset_hours":3,
  "ntp_use":true,
  "ntp_use_dhcp":false,
  "ntp_server1":"time.google.com",
  "ntp_server2":"time.cloudflare.com",
  "ntp_server3":"time.nist.gov",
  "ntp_server4":"pool.ntp.org"
}
```



{% swagger baseUrl="http://10.10.0.1" path="/status.json" method="get" summary="status.json" %}
{% swagger-description %}
This URL can be polled to get the Wi-Fi/Ethernet connection status of the gateway. 
{% endswagger-description %}

{% swagger-response status="200" description="Status of the network connection if it's not connected" %}
```json
{}
```
{% endswagger-response %}

{% swagger-response status="200: OK" description="Status of current Wi-Fi connection if it's connected" %}
```json
{"ssid":"my_wifi_1","ip":"192.168.1.119","netmask":"255.255.255.0","gw":"192.168.1.1","urc":0}
```
{% endswagger-response %}

{% swagger-response status="200: OK" description="After an unsuccessful attempt to connect" %}
```json
{"ssid":"my_wifi_1","ip":"0","netmask":"0","gw":"0","urc":1}
```
{% endswagger-response %}

{% swagger-response status="200: OK" description="After the user has disconnected from Wi-Fi" %}
```json
{"ssid":"my_wifi_1","ip":"0","netmask":"0","gw":"0","urc":2}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="http://10.10.0.1" path="/ap.json" method="get" summary="ap.json" %}
{% swagger-description %}
Scan for available Wi-Fi access points that the gateway can connect to.
{% endswagger-description %}

{% swagger-response status="200" description="An array of JSON objects containing nearby Wi-Fi networks " %}
```json
[
{"ssid":"Pantum-AP-A6D49F","chan":11,"rssi":-55,"auth":4},
{"ssid":"a0308","chan":1,"rssi":-56,"auth":3}
]
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="http://10.10.0.1" path="/connect.json" method="post" summary="connect.json" %}
{% swagger-description %}
Connect to a Wi-Fi network or Ethernet.

Data containing authentication information is transmitted in the body of the request in encrypted form.
{% endswagger-description %}

{% swagger-parameter in="body" name="encrypted" required="true" %}
Encrypted request, encoded as base64
{% endswagger-parameter %}

{% swagger-parameter in="body" name="iv" required="true" %}
AES initialization vector, encoded as base64
{% endswagger-parameter %}

{% swagger-parameter in="body" required="true" name="hash" %}
SHA256 hash of unencrypted request, encoded as base64
{% endswagger-parameter %}

{% swagger-response status="200" description="Gateway tries to connect to a given WiFi SSID or Ethernet." %}
```json
{}
```
{% endswagger-response %}

{% swagger-response status="400" description="If required parameter is missing." %}
```
Example: 

```
{% endswagger-response %}
{% endswagger %}

**Example**:

Unencrypted content of "**/connect.json**" is data in json format:

| Field name | Description                                                                                                                               |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| ssid       | WiFi network SSID or **null** for Ethernet                                                                                                |
| password   | Strings with a Wi-Fi password or **null** for Ethernet. The **null** value is also used for reconnecting to the last saved Wi-Fi network. |
| stub       | A string of spaces, which is chosen so that the json length is always 240 bytes, regardless of SSID length and password length.           |

Example of unencrypted data for connecting to Wi-Fi with the name "my\_ssid1":

```json
{"ssid": "my_ssid1", "password": "12345678", "stub": "                            "}
```

Example of unencrypted data for connecting to Wi-Fi with the name "my\_ssid1" using the saved password (the value "null" is passed to indicate that the saved value of the password is to be used):

```json
{"ssid": "my_ssid1", "password": null, "stub": "                            "}
```

Example of unencrypted data for connecting to Ethernet:

```json
{"ssid": null, "password": null, "stub": "                            "}
```

{% swagger baseUrl="http://10.10.0.1" path="/connect.json" method="delete" summary="connect.json" %}
{% swagger-description %}
Disconnect from WiFi or Ethernet.
{% endswagger-description %}

{% swagger-response status="200" description="Connection is dropped. " %}
```json
{}
```
{% endswagger-response %}

{% swagger-response status="400" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="http://10.10.0.1" path="/metrics" method="get" summary="metrics" %}
{% swagger-description %}
Get machine statistics, such as uptime and free memory. Data is in Prometheus format. For more details, please see https://prometheus.io/docs/instrumenting/exposition_formats/ .
{% endswagger-description %}

{% swagger-response status="200" description="Prometheus text data" %}
```
ruuvigw_received_advertisements 2566 ruuvigw_uptime_us 65447769 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_EXEC"} 205004 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_32BIT"} 211468 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_8BIT"} 136412 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_DMA"} 136412 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID2"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID3"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID4"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID5"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID6"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID7"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_SPIRAM"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_INTERNAL"} 211468 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_DEFAULT"} 136604 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_EXEC"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_32BIT"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_8BIT"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_DMA"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID2"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID3"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID4"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID5"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID6"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID7"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_SPIRAM"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_INTERNAL"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_DEFAULT"} 129948
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="http://10.10.0.1" path="/history" method="get" summary="history" %}
{% swagger-description %}
Get history data in json format
{% endswagger-description %}

{% swagger-parameter in="path" name="time" type="integer" %}
Read the history for the last N seconds only
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

See examples of the "history" payload here: [http-get-history-with-timestamps.md](../gw-data-formats/http-get-history-with-timestamps.md "mention")
