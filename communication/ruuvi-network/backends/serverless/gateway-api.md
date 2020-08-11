---
description: API for the Ruuvi Gateway
---

# Gateway API

Gateway API uses a JSON based API to facilitate communication between Ruuvi Gateways and the databases by validating and forwarding the data.

{% api-method method="post" host="https://api.placeholder.com/dev" path="/record" %}
{% api-method-summary %}
Send sensor data
{% endapi-method-summary %}

{% api-method-description %}
Sends a bulk of data to Ruuvi Network to be processed and stored.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Gateway specific access token / Signature \(TBD\)
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="data" type="object" required=true %}
Data object contains a formatted JSON blob of sensor data to be stored. Example below.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
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

Data payload consists of gateway information and an array of tag measurements as illustrated below.

```text
{
	"data":	{
		"coordinates": "",
		"timestamp": <UNIX TIMESTAMP>,
		"gwmac":	"<GATEWAY MAC ADDRESS>",
		"tags":	{
			"<TAG ID 1>": {
				"rssi": <RSSI VALUE>,
				"timestamp": <MEASUREMENT TIMESTAMP>,
				"data":	"<HEX ENCODED DATA>"
			},
			"<TAG ID 2>": {
				"rssi": <RSSI VALUE>,
				"timestamp": <MEASUREMENT TIMESTAMP>,
				"data":	"<HEX ENCODED DATA>"
			},
			...
		}
	}
}
```

