---
description: Internal API for Network Management
---

# Internal API

The Internal API consists of a set of endpoints designed to govern the Ruuvi Network, such as whitelisting and blacklisting devices and/or IP addresses.

## whitelist

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/whitelist`

Whitelists a set of gateways.

#### Headers

| Name              | Type   | Description                                      |
| ----------------- | ------ | ------------------------------------------------ |
| X-Internal-Secret | string | The secret to authenticate with the internal API |

#### Request Body

| Name | Type   | Description                                                                                     |
| ---- | ------ | ----------------------------------------------------------------------------------------------- |
|      | object | JSON object containing a list of Gateway Mac Addresses and their corresponding Signing Secrets. |

{% tabs %}
{% tab title="200 In case of success, a 200 OK is returned." %}
```
{
  "gateway": "<<MAC>>",
  "blockedAt": <<TIMESTAMP IF BLOCKED>>
}
```
{% endtab %}

{% tab title="400 If the provided data is invalid, 400 is returned." %}
```
```
{% endtab %}

{% tab title="403 In case no internal secret or invalid internal secret is provided, you will receive a 403 Forbidden." %}
```
```
{% endtab %}
{% endtabs %}

```
POST /whitelist
{
    "macAddress": "ab:ba:cd:ba:cd:ba",
    "secret": "1234"
}

```

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/gwinfo`

Fetches info for the gateway

#### Query Parameters

| Name    | Type   | Description         |
| ------- | ------ | ------------------- |
| gateway | string | Gateway Mac Address |

#### Headers

| Name              | Type   | Description                                      |
| ----------------- | ------ | ------------------------------------------------ |
| X-Internal-Secret | string | The secret to authenticate with the internal API |

{% tabs %}
{% tab title="200 " %}
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
{% endtab %}

{% tab title="401 If not authorized" %}
```
```
{% endtab %}
{% endtabs %}

## Register a sensor to Cloud

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/register-sensor`

This operation register a sensor with MAC address + secret to Cloud. The secret can be used to verify ownership of a sensor in case of a contested sensor.&#x20;

Parameters are packed inside a JSON object, e.g. { "macAddress":"value", "secret":"value"}

#### Headers

| Name              | Type   | Description                                      |
| ----------------- | ------ | ------------------------------------------------ |
| X-Internal-Secret | String | The secret to authenticate with the internal API |

#### Request Body

| Name                                         | Type   | Description                                             |
| -------------------------------------------- | ------ | ------------------------------------------------------- |
| macAddress<mark style="color:red;">\*</mark> | String | MAC address of sensor, 6 bytes. e.g. "AA:BB:CC:DD:EE:FF |
| secret<mark style="color:red;">\*</mark>     | String | Secret of sensor, e.g. "DE:AD:BE:EF:00:11:22:33         |

{% tabs %}
{% tab title="200: OK Sensor was added" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="400: Bad Request A parameter is missing or data is invalid" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="403: Forbidden Missing or invalid internal secret" %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}

## Register a subscription to be claimed by user

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/subscription-register`

This endpoint is called by Ruuvi Shop after payment for user subscription is verified. Parameters are in JSON object of body.

#### Headers

| Name                                            | Type   | Description                      |
| ----------------------------------------------- | ------ | -------------------------------- |
| X-Shop-Secret<mark style="color:red;">\*</mark> | String | Ruuvi Shop authentication secret |

#### Request Body

| Name                                                   | Type   | Description                                                                                              |
| ------------------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------- |
| validDays<mark style="color:red;">\*</mark>            | String | Validity of subscription, e.g. 365                                                                       |
| maxClaims<mark style="color:red;">\*</mark>            | Number | Number of sensors user can Claim                                                                         |
| maxShares                                              | Number | Number of shares user can have. Defaults to maxClaims \* maxSharesPerSensor                              |
| maxSharesPerSensor                                     | Number | Number of times one sensor can be shared. Defaults to 10                                                 |
| maxHistoryDays<mark style="color:red;">\*</mark>       | Number | Number of days of history user is allowed to retrieve. This does not affect sensors shared to this user. |
| maxResolutionMinutes<mark style="color:red;">\*</mark> | Number | Best resolution user is allowed to retrieve. This does not affect sensors shared to this user.           |
| subscriptionName                                       | String | Name of subscription. Defaults to "Ultimate" (custom)                                                    |
| claimCode<mark style="color:red;">\*</mark>            | String | Code used to claim this subscription                                                                     |
| creatorId                                              | String | String id for creator of code, e.g. webshop account which triggered code generation                      |

{% tabs %}
{% tab title="200: OK Subscription was registered" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="403: Forbidden Missing or invalid authentication header" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="400: Bad Request Missing required fields in payload" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="500: Internal Server Error Server error, request might have been valid" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="409: Conflict Subscription code already used" %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}

## Freebase Cloud Messaging to iOS devices - Proposal 2023-02-08

<mark style="color:green;">`POST`</mark> `FCM://iOS`

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

#### Request Body

| Name                                             | Type   | Description                                                                                                          |
| ------------------------------------------------ | ------ | -------------------------------------------------------------------------------------------------------------------- |
| alertData                                        | String | User-defined alert title. May be empty string                                                                        |
| alertType<mark style="color:red;">\*</mark>      | String | Physical quantity of alert, one of: {"Temperature", "Humidity", "Pressure", "Movement", "Voltage", "RSSI", "noData"} |
| triggerType<mark style="color:red;">\*</mark>    | String | Type of violation, one of {"Over", "Under", "Different from"}                                                        |
| name<mark style="color:red;">\*</mark>           | String | User-configured sensor name                                                                                          |
| alertUnit<mark style="color:red;">\*</mark>      | String | Unit of alert, e.g. "C", "F", "K"                                                                                    |
| currentValue<mark style="color:red;">\*</mark>   | String | Current value of alerting sensor, in alertUnit units                                                                 |
| thresholdValue<mark style="color:red;">\*</mark> | String | Threshold value of alerting sensor, in alertUnit units                                                               |
| token<mark style="color:red;">\*</mark>          | String | FCM Token of receiver                                                                                                |
| sensor\_id<mark style="color:red;">\*</mark>     | String | MAC Address of alerting senser                                                                                       |
| email<mark style="color:red;">\*</mark>          | String | User email                                                                                                           |
