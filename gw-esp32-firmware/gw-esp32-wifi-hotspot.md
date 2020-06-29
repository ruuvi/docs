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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
status.json
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="get" host="" path="" %}
{% api-method-summary %}
ap.json
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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

{% api-method method="post" host="" path="" %}
{% api-method-summary %}
configuration
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

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
| Hotspot is active on first boot | Check that there is hotspot "Ruuvi Gateway ABCD" Check that it is connectable with password "12345678" | Manual |
| Hotspot is deactivated on internet connection | Connect gateway with Ethernet cable, observe that hotspot is turned off. | Manual |
| Hotspot remains deactivated after internet connection | Disconnect Ethernet cable, reboot | Manual |
| Hotspot is reactivated on short button press | Connect to WiFi, press button. | Manual |

