---
description: Internal API for Network Management
---

# Internal API

The Internal API consists of a set of endpoints designed to govern the Ruuvi Network, such as whitelisting and blacklisting devices and/or IP addresses.

{% swagger baseUrl="https://network.ruuvi.com" path="/whitelist" method="post" summary="whitelist" %}
{% swagger-description %}
Whitelists a set of gateways.
{% endswagger-description %}

{% swagger-parameter in="header" name="X-Internal-Secret" type="string" %}
The secret to authenticate with the internal API
{% endswagger-parameter %}

{% swagger-parameter in="body" name="" type="object" %}
JSON object containing a list of Gateway Mac Addresses and their corresponding Signing Secrets.
{% endswagger-parameter %}

{% swagger-response status="200" description="In case of success, a 200 OK is returned." %}
```
{
  "gateway": "<<MAC>>",
  "blockedAt": <<TIMESTAMP IF BLOCKED>>
}
```
{% endswagger-response %}

{% swagger-response status="400" description="If the provided data is invalid, 400 is returned." %}
```
```
{% endswagger-response %}

{% swagger-response status="403" description="In case no internal secret or invalid internal secret is provided, you will receive a 403 Forbidden." %}
```
```
{% endswagger-response %}
{% endswagger %}

```
POST /whitelist
{
    "macAddress": "ab:ba:cd:ba:cd:ba",
    "secret": "1234"
}

```

{% swagger baseUrl="https://network.ruuvi.com" path="/gwinfo" method="get" summary="" %}
{% swagger-description %}
Fetches info for the gateway
{% endswagger-description %}

{% swagger-parameter in="header" name="X-Internal-Secret" type="string" %}
The secret to authenticate with the internal API
{% endswagger-parameter %}

{% swagger-parameter in="query" name="gateway" type="string" %}
Gateway Mac Address
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "result": "success",
    "data": {
        "gateway": {
            "GatewayId": "<<GATEWAY MAC>>",
            "Whitelisted": <<UNIX TIMESTAMP WHEN WHITELISTED>>,
            "Connected": <<FIRST CONNECTED AFTER WHITELISTING>>,
            "Latest": <<MOST RECENT UPDATE>>,
            "InvalidSignatureTimestamp": <<MOST RECENT SIGNING REJECTION>>
        }
    }
}
```
{% endswagger-response %}

{% swagger-response status="401" description="If not authorized" %}
```
```
{% endswagger-response %}
{% endswagger %}
