---
description: 'Lifecycle: Alpha. Last updated 2020-08-25'
---

# GW ESP32 WiFi Hotspot

The Gateway provides a WiFi hotspot for configuration. The hotspot has SSID with name "**RuuviGatewayABCD**", where ABCD are the last 2 bytes of gateway WiFi mac address. Password to connect to gateway is "**12345678**". 

The WiFi hotspot is only active if the gateway is not configured or within one minute after pressing the Configuration button. After the configuration of the gateway is complete, WiFi credentials are stored to flash and the hotspot is turned off. If the Internet connection is lost later, connection loss is indicated by "Red LED" but the hotspot is not turned back on unless the user enters configuration mode by pressing the Configuration button.

Gateway cannot be reconfigured over LAN, the configuration status page will be displayed in this case. Also following pages are available through LAN connection: /metrics and /history.  To reconfigure the gateway, press "configure" button and connect to the hotspot.

{% hint style="info" %}
If Ethernet cable is connected to an unconfigured gateway, then the gateway will automatically be set to the default configuration with Ethernet connection mode and WiFi hotspot will be deactivated. After that the user can activate the hotspot by short press on the "Configure" button or reset the configuration by long press on the "Configure" button \(In this case, the Ethernet cable must be disconnected, otherwise the gateway will automatically be set to default mode immediately after a configuration reset\).
{% endhint %}

| Event | Action  | Lifecycle | Since version |
| :--- | :--- | :--- | :--- |
| Boot, no previous internet connection. | Activate hotspot. | Beta | 0.2.0 |
| Boot, has been connected to internet. | Do not activate hotspot. | Beta | 0.2.0 |
| Internet connection established. | Deactivate hotspot. | Beta | 0.2.0 |
| Internet connection lost. | No action. | Beta | 0.2.0 |
| Short press on the Configuration button. | Drop WiFi or Ethernet connection, activate hotspot. | Beta | 1.3.2 |
| Long press on the Configuration button \(more than 5 seconds\). | Reset the configuration and reboot the gateway | Beta | 1.0.0 |

## API

The gateway is reachable at 10.10.0.1 once a client has connected to hotstop. These API calls are available:

{% api-method method="get" host="http://10.10.0.1" path="/status.json" %}
{% api-method-summary %}
status.json
{% endapi-method-summary %}

{% api-method-description %}
This URL can be polled to get the WiFi connection status of the gateway. 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Status of current WiFi connection
{% endapi-method-response-example-description %}

```
HTTP/1.0 200 OK
Content-type: application/json
Cache-Control: no-store, no-cache, must-revalidate, max-age=0
Pragma: no-cache

// If not connected
{}

// If Gateway is connected to WiFi
{"ssid":"%s","ip":"192.168.1.119","netmask":"255.255.255.0","gw":"192.168.1.1","urc":0}

// After unsuccessful connection attempt
{"ssid":"%s","ip":"0","netmask":"0","gw":"0","urc":1}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://10.10.0.1" path="/ap.json" %}
{% api-method-summary %}
ap.json
{% endapi-method-summary %}

{% api-method-description %}
Poll for available accesspoints Gateway can connect to.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Array of JSON objects containing nearby gateways. 
{% endapi-method-response-example-description %}

```
Content-type: application/json
Cache-Control: no-store, no-cache, must-revalidate, max-age=0
Pragma: no-cache

[
{"ssid":"Pantum-AP-A6D49F","chan":11,"rssi":-55,"auth":4},
{"ssid":"a0308","chan":1,"rssi":-56,"auth":3}
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="http://10.10.0.1" path="/connect.json" %}
{% api-method-summary %}
connect.json
{% endapi-method-summary %}

{% api-method-description %}
Connect to a WiFi.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-Custom-pwd" type="string" required=true %}
password
{% endapi-method-parameter %}

{% api-method-parameter name="X-Custom-ssid" type="string" required=true %}
WiFi SSID
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
The gateway tries to connect to given access point.
{% endapi-method-response-example-description %}

```
Content-type: application/json
Cache-Control: no-store, no-cache, must-revalidate, max-age=0
Pragma: no-cache

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
If required parameter is missing.
{% endapi-method-response-example-description %}

```
Content-Length: 0
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="http://10.10.0.1" path="/connect.json" %}
{% api-method-summary %}
connect.json
{% endapi-method-summary %}

{% api-method-description %}
Disconnect from WiFi or clear the connection status of the previous unsuccessful connection attempt.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Connection is dropped. 
{% endapi-method-response-example-description %}

```
Content-type: application/json
Cache-Control: no-store, no-cache, must-revalidate, max-age=0
Pragma: no-cache

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
Content-Length: 0
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://10.10.0.1" path="/metrics" %}
{% api-method-summary %}
metrics
{% endapi-method-summary %}

{% api-method-description %}
Get machine statistics, such as uptime and free memory. Data is in Prometheus format. For more details, please see https://prometheus.io/docs/instrumenting/exposition\_formats/ .
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Prometheus text data
{% endapi-method-response-example-description %}

```
ruuvigw_received_advertisements 2566 ruuvigw_uptime_us 65447769 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_EXEC"} 205004 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_32BIT"} 211468 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_8BIT"} 136412 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_DMA"} 136412 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID2"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID3"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID4"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID5"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID6"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_PID7"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_SPIRAM"} 0 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_INTERNAL"} 211468 ruuvigw_heap_free_bytes{capability="MALLOC_CAP_DEFAULT"} 136604 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_EXEC"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_32BIT"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_8BIT"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_DMA"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID2"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID3"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID4"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID5"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID6"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_PID7"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_SPIRAM"} 0 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_INTERNAL"} 129948 ruuvigw_heap_largest_free_block_bytes{capability="MALLOC_CAP_DEFAULT"} 129948
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="http://10.10.0.1/history" path="" %}
{% api-method-summary %}
history
{% endapi-method-summary %}

{% api-method-description %}
Get history data in json format.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="time" type="integer" required=false %}
Read the history for the last N seconds only
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Test checklist

| Event | Test | CI / Manual |
| :--- | :--- | :--- |
| Hotspot is active on first boot | Check that there is hotspot "RuuviGatewayABCD" Check that it is connectable with password "12345678" | Manual |
| Hotspot is deactivated on internet connection | Connect gateway with Ethernet cable, observe that hotspot is turned off. | Manual |
| Hotspot remains deactivated after internet connection | Disconnect Ethernet cable, reboot | Manual |
| Hotspot is reactivated on short button press | Connect to WiFi, press button. | Manual |

