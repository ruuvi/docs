---
description: 'Lifecycle: Alpha'
---

# GW ESP32 WiFi Hotspot

The Gateway provides a WiFi hotspot for configuration. The hotspot has SSID with name "Ruuvi Gateway ABCD", where ABCD are the last 2 bytes of gateway WiFi mac address. Password to connect to gateway is "12345678". 

The WiFi hotspot is active only if the gateway has not connected to the Internet. After gateway has connected to the Internet at least once, WiFi credentials are stored to flash and hotspot is turned off. If the Internet connection is lost later, connection loss is indicated by LEDs but hotspot is not turned back on unless user enter configuration mode by pressing button.

HTTP server is activated and deactivate in sync with WiFi hotspot, gateway cannot be reconfigured over LAN. 

{% hint style="info" %}
If Ethernet cable is connected, configuration mode cannot be entered as hotspot is immediately deactivated on internet connection. 
{% endhint %}

| Event | Action  | Lifecycle | Since version |
| :--- | :--- | :--- | :--- |
| Boot, no previous internet connection. | Activate hotspot. | Beta | 1.0 |
| Boot, has been connected to internet. | Do not activate hotspot. | Beta | 1.0 |
| Internet connection established. | Deactivate hotspot. | Beta | 1.0 |
| Internet connection lost. | No action. | Beta | 1.0 |
| Configuration button pressed. | Drop WiFi connection, activate hotspot. | Beta | 1.0 |
| Hotspot activated | Start http server. | Alpha | 1.0 |
| Hotspot deactivated | Stop http server. | Alpha | 1.0 |

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

## Test checklist

| Event | Test | CI / Manual |
| :--- | :--- | :--- |
| Hotspot is active on first boot | Check that there is hotspot "Ruuvi Gateway ABCD" Check that it is connectable with password "12345678" | Manual |
| Hotspot is deactivated on internet connection | Connect gateway with Ethernet cable, observe that hotspot is turned off. | Manual |
| Hotspot remains deactivated after internet connection | Disconnect Ethernet cable, reboot | Manual |
| Hotspot is reactivated on short button press | Connect to WiFi, press button. | Manual |

