---
description: API for the Ruuvi Gateway
---

# Gateway API

Gateway API uses a JSON based API to facilitate communication between Ruuvi Gateways and the databases by validating and forwarding the data.

{% swagger baseUrl="https://api.placeholder.com/dev" path="/record" method="post" summary="Send sensor data" %}
{% swagger-description %}
Sends a bulk of data to Ruuvi Network to be processed and stored.
{% endswagger-description %}

{% swagger-parameter in="header" name="Ruuvi-HMAC-SHA256" type="string" %}
Signature for the payload, signed with device specific keys.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="data" type="object" %}
Data object contains a formatted JSON blob of sensor data to be stored. Example below.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}

{% swagger-response status="403" description="In case of an invalid signature, you will receive a 403: Forbidden." %}
```
```
{% endswagger-response %}
{% endswagger %}

Data payload consists of gateway information and an array of tag measurements as illustrated below.

```
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

MAC address format: XX:XX:XX:XX:XX:XX (where XX is a hexadecimal digit in upper case).\
Example: "11:22:33:AA:BB:CC"\
MAC address is used in "\<GATEWAY MAC ADDRESS>" and in "\<TAG ID 1>", "\<TAG ID 2>", ...

The signature is a HMAC (hash-based message authentication code) which is calculated using sha256 algorithm from a combination of headers and the message body. Ruuvi network validates the signature against the whitelisted gateways (see: [Internal API](internal-api.md#whitelist)).

Below is an example code for calculating the secret:

```javascript
// Secret information is only existent on the device and Ruuvi Network
// but is not a part of the payload.
const secret = deviceId + deviceAddr;

// Signature body consists of the secret, random nonce, timestamp and message body
// These need to match the corresponding headers sent to Ruuvi network:
//   x-ruuvi-timestamp
//   x-ruuvi-nonce
const nonce = 'RANDOMLY GENERATED STRING';
const timestamp = Date.now();
const signatureBody = secret + nonce + timestamp + messageBody;

// Signature can then be calculated using the 'crypto' library. The finalized
// signature will be passed in the header:
//   x-ruuvi-signature
const crypto = require('crypto');
const signature = crypto.createHmac('sha256', secret)
    .update(signatureBody)
    .digest('hex');
```
