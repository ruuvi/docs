---
description: Internal API for Network Management
---

# Internal API

The Internal API consists of a set of endpoints designed to govern the Ruuvi Network, such as whitelisting and blacklisting devices and/or IP addresses.

{% api-method method="post" host="https://network.ruuvi.com" path="/whitelist" %}
{% api-method-summary %}
whitelist
{% endapi-method-summary %}

{% api-method-description %}
Whitelists a set of gateways.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="X-Internal-Secret" type="string" required=true %}
The secret to authenticate with the internal API
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="" type="object" required=true %}
JSON object containing a list of Gateway Mac Addresses and their corresponding Signing Secrets.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
In case of success, a 200 OK is returned.
{% endapi-method-response-example-description %}

```
I
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
If the provided data is invalid, 400 is returned.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}
In case no internal secret or invalid internal secret is provided, you will receive a 403 Forbidden.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

```text
POST /whitelist
{
    "gateways": [
        {"macAddress": "ab:ba:cd:ba:cd:ba", "secret": "1234"},
        {"macAddress": "bb:ba:cd:ba:cd:ba", "secret": "abcd"},
        {"macAddress": "cb:ba:cd:ba:cd:ba", "secret": "qwer"}
    ]
}

```

