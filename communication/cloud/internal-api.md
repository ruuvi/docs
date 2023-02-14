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

{% swagger method="post" path="register-sensor" baseUrl="https://network.ruuvi.com/" summary="Register a sensor to Cloud" %}
{% swagger-description %}
This operation register a sensor with MAC address + secret to Cloud. The secret can be used to verify ownership of a sensor in case of a contested sensor.&#x20;

Parameters are packed inside a JSON object, e.g. { "macAddress":"value", "secret":"value"}
{% endswagger-description %}

{% swagger-parameter in="body" name="macAddress" required="true" %}
MAC address of sensor, 6 bytes. e.g. "AA:BB:CC:DD:EE:FF
{% endswagger-parameter %}

{% swagger-parameter in="body" name="secret" required="true" %}
Secret of sensor, e.g. "DE:AD:BE:EF:00:11:22:33
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-Internal-Secret" %}
The secret to authenticate with the internal API
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Sensor was added" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="A parameter is missing or data is invalid" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Missing or invalid internal secret" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="subscription-register" baseUrl="https://network.ruuvi.com/" summary="Register a subscription to be claimed by user" %}
{% swagger-description %}
This endpoint is called by Ruuvi Shop after payment for user subscription is verified. Parameters are in JSON object of body.
{% endswagger-description %}

{% swagger-parameter in="header" name="X-Shop-Secret" required="true" %}
Ruuvi Shop authentication secret
{% endswagger-parameter %}

{% swagger-parameter in="body" name="validDays" required="true" %}
Validity of subscription, e.g. 365
{% endswagger-parameter %}

{% swagger-parameter in="body" name="maxClaims" required="true" type="Number" %}
Number of sensors user can Claim
{% endswagger-parameter %}

{% swagger-parameter in="body" name="maxShares" type="Number" %}
Number of shares user can have. Defaults to maxClaims * maxSharesPerSensor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="maxSharesPerSensor" type="Number" %}
Number of times one sensor can be shared. Defaults to 10
{% endswagger-parameter %}

{% swagger-parameter in="body" name="maxHistoryDays" type="Number" required="true" %}
Number of days of history user is allowed to retrieve. This does not affect sensors shared to this user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="maxResolutionMinutes" type="Number" required="true" %}
Best resolution user is allowed to retrieve. This does not affect sensors shared to this user.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="subscriptionName" %}
Name of subscription. Defaults to "Ultimate" (custom)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="claimCode" required="true" %}
Code used to claim this subscription
{% endswagger-parameter %}

{% swagger-parameter in="body" name="creatorId" %}
String id for creator of code, e.g. webshop account which triggered code generation
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Subscription was registered" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Missing required fields in payload" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Missing or invalid authentication header" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Subscription code already used" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Server error, request might have been valid" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="iOS" baseUrl="FCM://" summary="Freebase Cloud Messaging to iOS devices - Proposal 2023-02-08" %}
{% swagger-description %}
FCM is used to deliver push notifications to user applications. To receive the notification, user must register their device token with a POST to [https://network.ruuvi.com/push-register](https://network.ruuvi.com/push-register)

`{ "notification":{` \
&#x20; `"body": $alertData,` \
&#x20; `"title":"Ruuvi $alertType alert: $name"`\
&#x20; `},` \
&#x20; `"alert":{` \
&#x20;   `"title-loc-key": RUUVI_$alertType,` \
&#x20;   `"title-loc-args": [$alertType, $triggertype],` \
&#x20;   `"loc-key" : "RUUVI_$alertType_$triggerType",` \
&#x20;   `"loc-args" : [ $name, $currentValue, $alertUnit, $thresholdValue, $alertUnit]` \
&#x20; `},` \
&#x20; `"content_available":1,`\
&#x20; `"mutable-content":1,`\
&#x20; `"token":$token,` \
&#x20; `"email":$email,` \
&#x20; `"type":"alert",` \
&#x20; `"data":{` \
&#x20;   `"name": $name,` \
&#x20;   `"id":$`sensor\_id`,` \
&#x20;   `"alertType": $alertType,` \
&#x20;   `"triggerType": $triggertype,` \
&#x20;   `"currentValue": $currentValue,` \
&#x20;   `"thresholdValue": $thresholdValue,` \
&#x20;   `"alertUnit": $alertUnit,` \
&#x20;   `"alertData": $alertData` \
&#x20; `}` \
`}`
{% endswagger-description %}

{% swagger-parameter in="body" name="alertData" %}
User-defined alert title. May be empty string
{% endswagger-parameter %}

{% swagger-parameter in="body" name="alertType" required="true" %}
Physical quantity of alert, one of: {"Temperature", "Humidity", "Pressure", "Movement", "Voltage", "RSSI", "noData"}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="triggerType" required="true" %}
Type of violation, one of {"Over", "Under", "Different from"}
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" required="true" %}
User-configured sensor name
{% endswagger-parameter %}

{% swagger-parameter in="body" name="alertUnit" required="true" %}
Unit of alert, e.g. "C", "F", "K"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="currentValue" required="true" %}
Current value of alerting sensor, in alertUnit units
{% endswagger-parameter %}

{% swagger-parameter in="body" name="thresholdValue" required="true" %}
Threshold value of alerting sensor, in alertUnit units
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" required="true" %}
FCM Token of receiver
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor_id" required="true" %}
MAC Address of alerting senser
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" required="true" %}
User email
{% endswagger-parameter %}
{% endswagger %}
