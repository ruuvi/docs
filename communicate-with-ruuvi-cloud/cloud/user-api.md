---
description: 'Ruuvi Cloud user facing API. Lifecycle: in production'
---

# User API

User API uses a JSON based API to allow users to register, secure and edit their information as well as claim and share sensors, retrieve sensor data and alter their subscription details. Fields marked with <mark style="color:red;">\*</mark> are mandatory, and omitting them results in backend returning HTTP 400 - Bad Request.

For example, if the body parameter in the sections below refers to an **email** field, the corresponding JSON payload would look like this:

```
{
    "email": "<YOUR VALUE>"
}
```

Note that GET requests use URL parameters, e.g. `https://network.ruuvi.com/sensors-dense?measurements=true`, but the Authorization bearer token is in headers.&#x20;

All authenticated queries are ratelimited to 8 \* MAX\_SENSORS\_OWNED + 0.1 \* MAX\_HISTORY\_DAYS per minute. For example user with Basic plan has maximum of 90 days of history on 25 sensors and can make up to 209 queries per minute. The throtteled response has response code of 429 and payload of:&#x20;

```
{
      result: 'error',
      error: 'Too many requests.',
      code: 'ER_THROTTLED'
}
```



## Register User or Reset Token

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/register`

Registers a new user or resets an existing user's password if the user already exists.

#### Request Body

| Name  | Type   | Description                            |
| ----- | ------ | -------------------------------------- |
| email | string | Email address to be registered / reset |

{% tabs %}
{% tab title="200 On a successful call, you will receive a 200 OK. An e-mail will be sent to the given address to confirm the registration.
In case of a reset, the token will be provided as a response to the call." %}
```
{
    "result": "success",
    "data": {
        "email": "matti@meikalainen.com"
    }
}
```
{% endtab %}

{% tab title="500 If a something goes wrong with the request itself, you might receive an Unknown error. Please contact your system administrator if this occurs." %}
```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endtab %}

{% tab title="429: Too Many Requests Over 10 calls in an hour" %}
```
{
      result: 'error',
      error: 'Too many requests.',
      code: 'ER_THROTTLED'
}
```
{% endtab %}
{% endtabs %}

## Verify Account

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/verify`

Verifies the given e-mail address and finalizes creating the account and creating a Ruuvi Network subscription. Notice that the token for this end-point is delivered via e-mail by the **Register User** endpoint.

#### Query Parameters

| Name  | Type   | Description                                 |
| ----- | ------ | ------------------------------------------- |
| token | string | Verification token (received in the e-mail) |

{% tabs %}
{% tab title="200 On a successful response, you will receive the confirmation on the e-mail address an an access token to be used with other end-points.
Store it well as the only way to retrieve it is to go through the reset flow again." %}
```
{
    "result": "success",
    "data": {
        "email": "<E-MAIL ADDRESS OF THE USER>",
        "accessToken": "<NEW ACCESS TOKEN>",
        "newUser": <true|false>
    }
}
```
{% endtab %}

{% tab title="403 Forbidden if user is not allowed to access resource." %}
```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endtab %}

{% tab title="500 (Actual code 493): You will receive an error if the token is invalid." %}
```
{
    "result": "error",
    "error": "Code used or expired.",
    "code": "ER_TOKEN_EXPIRED"
}
```
{% endtab %}
{% endtabs %}

## Request deletion of account

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/request-delete`

This operation requests complete removal of user account from Ruuvi Cloud. After a successful call to this endpoint, user gets a verification email with a link to confirm deletion of account.

#### Headers

| Name                                            | Type   | Description                           |
| ----------------------------------------------- | ------ | ------------------------------------- |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer token to authorize the request |

#### Request Body

| Name                                    | Type   | Description                |
| --------------------------------------- | ------ | -------------------------- |
| email<mark style="color:red;">\*</mark> | String | Email of account to delete |

{% tabs %}
{% tab title="200: OK Verification email has been sent" %}
```javascript
{
    "result": "success",
    "data": {
        "email": "otso+test3@ruuvi.com"
    }
}
```
{% endtab %}

{% tab title="400: Bad Request Missing authorization or email parameter" %}
```javascript
{
    "result": "error",
    "error": "<SPECIFIC ERROR>",
    "code": "ER_<ERROR>"
}
```
{% endtab %}

{% tab title="403: Forbidden Returned if Authorization token does not match email" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}
{% endtabs %}

## Verify account deletion operation

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/verify-delete`

Following actions will be done:

User sensors will be unshared&#x20;

Sensors shared to user will be removed.

&#x20;~~Data of user sensors will be deleted~~. (TODO)

&#x20;User account data, including sensor claims and settings, will be deleted.

&#x20;Account deletion is a permament action which cannot be undone

#### Path Parameters

| Name                                    | Type   | Description               |
| --------------------------------------- | ------ | ------------------------- |
| token<mark style="color:red;">\*</mark> | String | Short verification string |

{% tabs %}
{% tab title="200: OK Account deletion was started" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="403: Forbidden Invalid or missing authorization token" %}
```javascript
{
   {
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}
{% endtabs %}

## Claim a sensor for user

<mark style="color:green;">`POST`</mark> `https://netowrk.ruuvi.com/claim`

After this call, given sensor is claimed under authenticated user account

#### Headers

| Name                                            | Type   | Description                            |
| ----------------------------------------------- | ------ | -------------------------------------- |
| Authorization<mark style="color:red;">\*</mark> | String | BBearer token to authorize the request |

#### Request Body

| Name                                     | Type   | Description                                                                |
| ---------------------------------------- | ------ | -------------------------------------------------------------------------- |
| sensor<mark style="color:red;">\*</mark> | String | MAC address of sensor to claim, e.g. "AA:BB:CC:11:22:33"                   |
| name                                     | String | Human-readable name of sensor, e.g. "Fridge temperature sensor"            |
| description                              | String | Human-readable description of sensor, e.g. "Sensor in top shelf of fridge" |

{% tabs %}
{% tab title="200: OK Sensor was claimed successfully" %}
```javascript
{
    "result": "success",
    "data": {
        "sensor": "C5:2A:E7:4D:CE:7F"
    }
}
```
{% endtab %}

{% tab title="400: Bad Request Request had malformed JSON or was missing a required parameter.  Alternatively user account has reached subscription limit" %}
```javascript
{
    'code': {'ER_MISSING_ARGUMENT', 'ER_CLAIM_COUNT_REACHED'}
}
```
{% endtab %}

{% tab title="401: Unauthorized Request had no authorization token" %}
```javascript
{

}
```
{% endtab %}

{% tab title="409: Conflict Sensor is claimed by another account" %}
```javascript
{
    'code': 'ER_SENSOR_ALREADY_CLAIMED';
}
```
{% endtab %}

{% tab title="500: Internal Server Error Unexpected error occurred in handler" %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}

## Unclaim a sensor from your user

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/unclaim`

Unclaims a sensor from your user, revoking your own access to it and making it claimable by other users.

#### Headers

| Name                                            | Type   | Description                           |
| ----------------------------------------------- | ------ | ------------------------------------- |
| Authorization<mark style="color:red;">\*</mark> | string | Bearer token to authorize the request |

#### Request Body

| Name                                     | Type    | Description                     |
| ---------------------------------------- | ------- | ------------------------------- |
| sensor<mark style="color:red;">\*</mark> | string  | ID of the sensor to be unshared |
| deleteData                               | boolean | set to true to delete user data |

{% tabs %}
{% tab title="200 " %}
```
{
    "result": "success"
}
```
{% endtab %}
{% endtabs %}

## Share a sensor

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/share`

You can share your sensor data with other users via **share** end-point. In addition to sensor you want to share, you must also include the e-mail address of the recipient. This will grant them access to the data via the **get** end-point.\
Furthermore, it will also send the target user a notification e-mail about the new share. If the target user does not exist yet, an invitation to create an account will be sent to them and they will gain access upon sign up.

#### Headers

| Name          | Type   | Description                           |
| ------------- | ------ | ------------------------------------- |
| Authorization | string | Bearer token to authorize the request |

#### Request Body

| Name   | Type   | Description                    |
| ------ | ------ | ------------------------------ |
| user   | string | E-mail of the user to share to |
| sensor | string | Sensor ID to share             |

{% tabs %}
{% tab title="200 On success, you will get the shared sensor id returned back to you." %}
```
{
    "result": "success",
    "data": {
        "sensor": "<YOUR SENSOR ID>"
        "invited": true
    }
}
```
{% endtab %}

{% tab title="400 If the sharing failed due to malformed data, such as missing arguments." %}
```
{
    "result": "error",
    "error": "Invalid E-mail given.",
    "code": "ER_INVALID_EMAIL_ADDRESS"  
}
```
{% endtab %}

{% tab title="401 If an invalid or expired access token is provided, you will receive 401 Unauthorized." %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}

{% tab title="409 You will receive a conflict if the sensor is already shared to the user." %}
```
{
    "result": "error",
    "error": "Sensor already shared to user.",
    "code": "ER_SENSOR_ALREADY_SHARED"
}
```
{% endtab %}

{% tab title="500 If something went wrong with the request, you will receive a 500 internal server error. Please contact your System Administrator." %}
```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endtab %}
{% endtabs %}

## Unshare a sensor

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/unshare`

Unshares (i.e. revokes access to) the sensor from a target user. This can also currently be used to remove sensors shared with your user.

#### Headers

| Name          | Type   | Description              |
| ------------- | ------ | ------------------------ |
| Authorization | string | Bearer token of the user |

#### Request Body

| Name   | Type   | Description                                                                                     |
| ------ | ------ | ----------------------------------------------------------------------------------------------- |
| sensor | string | ID of the sensor being unshared                                                                 |
| user   | string | E-mail of the user the sensor is shared to. Optional if removing sensor shared to current user. |

{% tabs %}
{% tab title="200 " %}
```
{
    "result": "success"
}
```
{% endtab %}

{% tab title="400 Returned with Invalid or missing fields." %}
```
{
    "result": "error",
    "error": "<SPECIFIC ERROR>",
    "code": "ER_<ERROR>"
}
```
{% endtab %}

{% tab title="403 Returned when user" %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}

{% tab title="404 Returned if shared sensor or user is not found." %}
```
{
    "result": "error",
    "error": "User not found.",
    "code": "ER_USER_NOT_FOUND"
}
```
{% endtab %}
{% endtabs %}

## Get your sensors

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/sensors`

Fetches a list of sensors you have access to including who those are shared to. This end-point deprecates the old _shared_ end-point.

#### Query Parameters

<table><thead><tr><th width="136">Name</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>sensor</td><td>string</td><td>Optionally filter only one sensor</td></tr></tbody></table>

#### Headers

| Name          | Type   | Description              |
| ------------- | ------ | ------------------------ |
| Authorization | string | Bearer token of the user |

{% tabs %}
{% tab title="200 " %}
```
{
    "result": "success",
    "data": {
        "sensors": [
            {
                "sensor": "<SENSOR ID>",
                "name": "<SENSOR NAME>",
                "picture": "<SENSOR PICTURE URL>",
                "public": <TRUE|FALSE>,
                "canShare": <TRUE|FALSE>,
                "offsetHumidity": <DOUBLE>,
                "offsetTemperature": <DOUBLE>,
                "offsetPressure": <DOUBLE>,
                "measurements": [
                    {
                        "gwmac": "<SOURCE GATEWAY MAC>",
                        "coordinates": "<COORDINATES / N/A>",
                        "rssi": <RSSI>,
                        "timestamp": <UNIX TIMESTAMP OF MEASUREMENT>,
                        "data": "<HEX ENCODED SENSOR DATA>"
                    }
                ]
                "sharedTo": [
                    "<EMAIL OF TARGET USER 1>",
                    ...
                ]
            },
            ...
        ],
        "sharedToMe": [
            {
                "sensor": "<SENSOR ID>",
                "name": "<SENSOR NAME>",
                "picture": "<SENSOR PICTURE URL>",
                "public": <TRUE|FALSE>,
                "canShare": <TRUE|FALSE>,
                "offsetHumidity": <DOUBLE>,
                "offsetTemperature": <DOUBLE>,
                "offsetPressure": <DOUBLE>,
                "measurements": [
                    {
                        "gwmac": "<SOURCE GATEWAY MAC>",
                        "coordinates": "<COORDINATES / N/A>",
                        "rssi": <RSSI>,
                        "timestamp": <UNIX TIMESTAMP OF MEASUREMENT>,
                        "data": "<HEX ENCODED SENSOR DATA>"
                    }
                ]
            },
        ]
    }
}
```
{% endtab %}

{% tab title="401 " %}
```
{
    "result": "error",
    "error": "Unauthorized.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}
{% endtabs %}

## Get your sensors with calibration data, latest measurement, and alerts settings

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/sensors-dense`

Fetches the list of claimed and shared sensors with calibration data, sensor last measurement, subscription type and alert settings. By default the endpoint returns only the claimed sensors with calibration data. Optional arguments must be passed to get shared sensors, last measurement, and alert settings.&#x20;

#### Query Parameters

| Name           | Type   | Description                                                                                                                                       |
| -------------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| sensor         | string | Optionally filter only one sensor                                                                                                                 |
| sharedToOthers | bool   | Optionally returns the list of users with whom each of the sensors is shared to. Returns empty list for non-owners                                |
| sharedToMe     | bool   | Optionally returns the sensors shared to the logged-in user alongside claimed sensors by the user                                                 |
| measurements   | bool   | Optionally returns the latest measurement of each of the sensors in the collection. Returns also the subscription on which the data is based on.  |
| alerts         | bool   | Optionally returns the alerts settings of each of the sensors in the collection                                                                   |
| settings       | bool   | Optionally returns the sensor-specific settings of sensors.                                                                                       |
| mode           | string | Fetch mode: \[dense, sparse, mixed], determines how the data is returned. Default: mixed                                                          |

{% tabs %}
{% tab title="401: Unauthorized " %}
```javascript
{
    "result": "error",
    "error": "Unauthorized.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}

{% tab title="200: OK " %}
```javascript
{
    "result": "success",
    "data": {
        "sensors": [
            {
                "sensor": "<SENSOR ID>",
                "name": "<SENSOR NAME>",
                "picture": "<SENSOR PICTURE URL>",
                "public": <TRUE|FALSE>,
                "canShare": <TRUE|FALSE>,
                "offsetHumidity": <DOUBLE>,
                "offsetTemperature": <DOUBLE>,
                "offsetPressure": <DOUBLE>,
                "measurements": [
                    {
                        "gwmac": "<SOURCE GATEWAY MAC>",
                        "coordinates": "<COORDINATES / N/A>",
                        "rssi": <RSSI>,
                        "timestamp": <UNIX TIMESTAMP OF MEASUREMENT>,
                        "data": "<HEX ENCODED SENSOR DATA>"
                    }
                ],
                "sharedTo": [
                    "<EMAIL OF TARGET USER 1>",
                    ...
                ],
                "alerts": [
                    {
                        userId: <userId>,
                        sensorId: <sensorMAC>,
                        type: <humidity|pressure|temperature>,
                        min: <lower limit>,
                        max: <higher limit>,
                        enabled: <true|false>,
                        offsetHumidity: <double>,
                        offsetTemperature: <double>,
                        offsetPressure: <double>,
                        triggered: <true|false>,
                        triggeredAt: <timestamp>
                    },
                    ...
                ]
            },
            owner: <EMAIL, masked if public sensor>
            subscription: {
                    "maxHistoryDays": <INT>,
                    "maxResolutionMinutes": <INT>,
                    "emailAlertAllowed": <true|false>,
                    "pushAlertAllowed": <true|false>,
                    "subscriptionName": <STRING>
            }
            ...
        ]
    }
}
```
{% endtab %}
{% endtabs %}

## Get User Info

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/user`

Fetches user information for an authenticated user.

#### Headers

| Name           | Type   | Description                                                |
| -------------- | ------ | ---------------------------------------------------------- |
| Authentication | string | Authentication Bearer token retrieved from the login flow. |

{% tabs %}
{% tab title="200 User information successfully retrieved." %}
```
{
    "result": "success",
    "data": {
        "email": "my-email@email.com",
        "sensors": [
            {
                "sensor": "CD:CD:CD:CD:ED:01",
                "owner": "my-email@email.com",
                "name": "Sauna",
                "picture": "https://url-to/picture.png",
                "public": true
            },
            {
                "sensor": "AB:BA:CD:BE:AB:AA",
                "owner": "someone-else@email.com",
                "name": "Kitchen",
                "picture": "",
                "public": false
            }
        ]
    }
}
```
{% endtab %}

{% tab title="401 Unauthorized request." %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}
{% endtabs %}

## Get Sensor data

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/get`

Returns the data points for the requested sensor. Notice that for implementing pagination, you can use **since** and **until** parameters with custom **limit** to segment your results as they are always returned in either ascending or descending order by timestamp.

Data can be fetched in dense, sparse and mixed mode. Dense mode returns highest data density possible, but has a limited time range before data is pruned to save storage space. Sparse mode has downsampled data, but time range is not limited. Mixed mode returns all the dense data available and rest of the time range is filled with sparse data

#### Query Parameters

| Name                                     | Type   | Description                                                                                     |
| ---------------------------------------- | ------ | ----------------------------------------------------------------------------------------------- |
| mode                                     | string | Fetch mode: \[dense, sparse, mixed], determines how the data is returned. Default: mixed        |
| until                                    | string | Maximum timestamp of first returned result in Unix epoch format, in seconds. Default until now. |
| since                                    | string | Minimum timestamp of first returned result in Unix epoch format, in seconds. Default 0.         |
| limit                                    | string | Maximum amount of results returned (capped at 5000).                                            |
| sort                                     | string | Sort Direction for the result: \[asc, desc]. Default descending                                 |
| sensor<mark style="color:red;">\*</mark> | string | Sensor ID to retrieve the data                                                                  |

#### Headers

| Name          | Type   | Description                           |
| ------------- | ------ | ------------------------------------- |
| Authorization | string | Bearer token to authorize the request |

{% tabs %}
{% tab title="200 Returns the most recent data points for the requested tag based on configuration and parameters.f" %}
```
{
    "result": "success",
    "data": {
        "sensor": "<SENSOR ID>",
        "total": <TOTAL MEASUREMENTS RETURNED>,
        "name": "<SENSOR NAME>",
        "picture": "<SENSOR PICTURE URL OR FILENAME>",
        "measurements": [
            {
                "gwmac": "<SOURCE GATEWAY MAC>",
                "coordinates": "<COORDINATES / N/A>",
                "rssi": <RSSI>,
                "timestamp": <UNIZ TIMESTAMP OF MEASUREMENT>,
                "data": "<HEX ENCODED SENSOR DATA>"
            },
            ...
        ]
    }
}
```
{% endtab %}

{% tab title="400 " %}
```
{
    "result": "error",
    "error": "Invalid <SPECIFIC ERROR>",
    "code": "ER_INVALID_<SPECIFIC>"
}
```
{% endtab %}

{% tab title="401 In case of an invalid or expired authentication token, you will receive a unauthorized response." %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}

{% tab title="403 If you have not claimed or been shared the target sensor, you will receive a Forbidden." %}
```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endtab %}
{% endtabs %}

## Update Sensor metadata

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/update`

Updates sensor metadata.

#### Headers

| Name          | Type   | Description |
| ------------- | ------ | ----------- |
| Authorization | string |             |

#### Request Body

| Name              | Type    | Description                                                                                        |
| ----------------- | ------- | -------------------------------------------------------------------------------------------------- |
| picture           | string  | Filename of a picture (or URL if uploaded)                                                         |
| offsetHumidity    | number  | Offset humidity to calibrate sensor                                                                |
| offsetPressure    | number  | Offset pressure to calibrate sensor                                                                |
| offsetTemperature | number  | Offset temperature to calibrate sensor                                                             |
| public            | boolean | If true, data will be publicly accessible.                                                         |
| sensor            | string  | Sensor ID to update                                                                                |
| name              | string  | Desired name of the tag                                                                            |
| timestamp         | number  | Epoch timestamp in seconds of settings. If backend has fresher data stored, this will be ignored.  |

{% tabs %}
{% tab title="200 Only returns the fields that had an update targeted to them." %}
```
{
    "result": "success",
    "data": {
        "sensor": "<SENSOR ID>",
        "name": "<GIVEN NAME>",
        "public": "<GIVEN PUBLIC VALUE>"
    }
}
```
{% endtab %}

{% tab title="403 " %}
```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endtab %}

{% tab title="404 " %}
```
{
    "result": "error",
    "error": "Sensor not claimed or found. Data not updated.",
    "code": "ER_SENSOR_NOT_FOUND"
}
```
{% endtab %}

{% tab title="500 " %}
```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endtab %}

{% tab title="409: Conflict Cloud has fresher data than timestamp" %}
```
{
    "result": "error",
    "error": "Newer setting already exists",
    "code": "ER_CONFLICT",
    "sub_code": "ER_OLD_ENTRY"
}
```
{% endtab %}
{% endtabs %}

## Upload Sensor image (part 1)

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/upload`

Retrieves a signed upload URL to a bucket. This makes the back-end ready for the image upload to happen.

#### Headers

| Name          | Type   | Description              |
| ------------- | ------ | ------------------------ |
| Authorization | string | Bearer token of the user |

#### Request Body

| Name   | Type   | Description                                                                                                                                                      |
| ------ | ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| action | string | One of: _upload_, _reset_ (default: 'upload' if not given')                                                                                                      |
| sensor | string | ID of the target Sensor                                                                                                                                          |
| type   | string | <p>(<strong>Required</strong> when type is 'upload')<br>Content-Type of the desired image upload. Supported formats:<br>image/png<br>image/gif<br>image/jpeg</p> |

{% tabs %}
{% tab title="200 " %}
```
{
    "result": "success",
    "data": {
        "uploadURL": "<SIGNED UPLOAD URL>"
    }
}
```
{% endtab %}

{% tab title="403 " %}
```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endtab %}
{% endtabs %}

## Upload the actual image

<mark style="color:orange;">`PUT`</mark> `<URL FROM part 1>`&#x20;

Create a PUT request to the URL produced by /upload end-point with the data payload to complete the upload.

#### Headers

| Name         | Type   | Description                     |
| ------------ | ------ | ------------------------------- |
| Content-Type | string | Matching content type to part 1 |

#### Request Body

| Name              | Type   | Description                      |
| ----------------- | ------ | -------------------------------- |
| Image binary data | object | Binary data for the image upload |

{% tabs %}
{% tab title="200 " %}
```
```
{% endtab %}

{% tab title="403 " %}
```
```
{% endtab %}
{% endtabs %}

## Get User Settings

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/settings`

Gets the full list of existing user settings.

#### Headers

| Name          | Type   | Description              |
| ------------- | ------ | ------------------------ |
| Authorization | string | Bearer token of the user |

{% tabs %}
{% tab title="200 " %}
```
{
    "status": "success",
    "data": {
        "settings": {
            "<SETTING 1>": "<SETTING 1 VALUE>",
            ...
        }
    }
}
```
{% endtab %}
{% endtabs %}

## Update user setting

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/settings`

Sets a single user setting (currently).

#### Headers

| Name          | Type   | Description              |
| ------------- | ------ | ------------------------ |
| Authorization | string | Bearer token of the user |

#### Request Body

| Name      | Type   | Description                                                                                       |
| --------- | ------ | ------------------------------------------------------------------------------------------------- |
| value     | string | Setting value                                                                                     |
| name      | string | Setting key (alphanumeric with "\_", "-" and "."                                                  |
| timestamp | number | Epoch timestamp in seconds of settings. If backend has fresher data stored, this will be ignored. |

{% tabs %}
{% tab title="200 " %}
```
{
    "status": "success",
    "data": {
        "action": "<added|updated>"
    }
}
```
{% endtab %}

{% tab title="409: Conflict Cloud has fresher data than timestamp" %}
```
{
    "result": "error",
    "error": "Newer setting already exists",
    "code": "ER_CONFLICT",
    "sub_code": "ER_OLD_ENTRY"
}
```
{% endtab %}
{% endtabs %}

## Create and update Alerts

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/alerts`

Sets an alert on a sensor for a given metric. The alert condition is tested against the absolute value received from the sensors in conjunction with the use set offsets for that particular sensor.

#### Headers

| Name                                            | Type   | Description              |
| ----------------------------------------------- | ------ | ------------------------ |
| Authorization<mark style="color:red;">\*</mark> | string | Bearer token of the user |

####

#### Request Body

| Name                                     | Type    | Description                                                                                                                         |
| ---------------------------------------- | ------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| counter                                  | number  | For movement alerts, one can manually set the current number. If not provided, last known value is used.                            |
| type<mark style="color:red;">\*</mark>   | string  | One of: temperature, humidity, pressure, signal, movement, offline, co2, pm10, pm25, pm40, pm100, sound, luminosity, voc, nox       |
| min                                      | number  | Lower limit for the alert - omit to leave unchanged                                                                                 |
| max                                      | number  | Upper limit for the alert - omit to leave unchanged                                                                                 |
| enabled                                  | boolean | Used to toggle alert on and off                                                                                                     |
| sensor<mark style="color:red;">\*</mark> | string  | Sensor MAC of the target sensor                                                                                                     |
| timestamp                                | number  | Epoch timestamp in seconds of settings. If backend has fresher data stored, this will be ignored. Set to current second by default  |
| delay                                    | number  | How many \*seconds\* alert condition has to be valid before alert gets triggered. Delay is reset if alert is cleared. Defaults to 0 |



{% tabs %}
{% tab title="200 " %}
```
{
    "result": "success",
    "data": {
        "action": "success"
    }
}
```
{% endtab %}

{% tab title="400: Bad Request" %}
```
 { 
  "result": "error", 
  "error": "Invalid MAC address format", 
  "code": "ER_INVALID_MAC_ADDRESS" 
  }
```
{% endtab %}

{% tab title="409: Conflict Cloud has fresher data than timestamp" %}
```
{
    "result": "error",
    "error": "Newer setting already exists",
    "code": "ER_CONFLICT",
    "sub_code": "ER_OLD_ENTRY"
}
```
{% endtab %}
{% endtabs %}

## Get alerts

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/alerts`

Fetches alerts for all sensors user has access to or a single sensor if optional parameter is provided.

#### Request Body

| Name   | Type   | Description                               |
| ------ | ------ | ----------------------------------------- |
| sensor | string | Optional Sensor MAC for filter the alerts |

{% tabs %}
{% tab title="200 " %}
```
{
    "result": "success",
    "data": {
        "alerts": [
            {
                userId: <userId>,
                sensorId: <sensorMAC>,
                description: <string>
                type: <humidity|pressure|temperature|movement|offline>,
                counter: number, // Relevant for movement
                min: <lower limit>,
                max: <higher limit>,
                enabled: <true|false>,
                offsetHumidity: <double>,
                offsetTemperature: <double>,
                offsetPressure: <double>,
                triggered: <true|false>,
                triggeredAt: <timestamp>,
                delay: <number, positive integer>
            }
        ]
    }
}
```
{% endtab %}
{% endtabs %}





## Update sensor setting

<mark style="color:green;">`POST`</mark> `/sensor-settings`

Configure a sensor-specific setting. Note: Offsets, image, name and shares of sensors are updated in their own endpoints. Only owner of a sensor can configure the settings.&#x20;

To clear a setting, send empty string as a value of setting type.&#x20;

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body**

| Name          | Type         | Description                                                                                                                                     |
| ------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `sensor`\*    | string       | MAC address of sensor                                                                                                                           |
| `type`\*      | string array | Type of the setting. Free-form. sensor+type combination is unique identifier of setting.                                                        |
| `value`\*     | string array | Value of setting. Length of type and value arrays must match. Settings are appended, e.g. it's allowed to configure settings individually       |
| `timestamp`\* | number       | Epoch timestamp in seconds of settings. If backend has fresher data stored, this will be ignored. If omitted, timestamp is set to current time. |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "result": "success",
    "data": {
        "action": "<added | updated>"
    }
}
```
{% endtab %}

{% tab title="400" %}
```json
{
    "result": "error",
    "error": "Body must be a valid JSON string",
    "code": "ER_INVALID_ARGUMENT"
}
```
{% endtab %}

{% tab title="409" %}
```json
{
    "result": "error",
    "error": "No setting was updated or added, newer settings might exist.",
    "code": "ER_CONFLICT"
}
```
{% endtab %}

{% tab title="500" %}
```json
{
    "result": "error",
    "error": "Unknown error occured in User API",
    "code": "ER_INTERNAL"
}
```
{% endtab %}
{% endtabs %}

## Check if a sensor with given MAC address is claimed by someone

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/check`

#### Query Parameters

| Name                                     | Type        | Description                |
| ---------------------------------------- | ----------- | -------------------------- |
| sensor<mark style="color:red;">\*</mark> | MAC address | AA:BB:CC:DD:EE:FF (String) |

#### Headers

| Name                                            | Type   | Description            |
| ----------------------------------------------- | ------ | ---------------------- |
| Authorization<mark style="color:red;">\*</mark> | Bearer | Bearer \<Bearer Token> |

{% tabs %}
{% tab title="200: OK Masked email of sensor owner, empty string if sensor is not owned" %}
```javascript
{
    "status": "success",
    "data": {
        "email": <string>
    }
}
```
{% endtab %}

{% tab title="400: Bad Request If request doesn't have "sensor" parameter, or parameter is not a valid MAC address" %}
```javascript
    "status": "success",
    "data": {
        "email": <string>
    }
}
```
{% endtab %}

{% tab title="403: Forbidden If there was no valid authentication" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}
{% endtabs %}

## Contest ownership of a sensor

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/contest-sensor`

This call is used to reclaim a sensor claimed by someone else. After this endpoint returns 200, the sensor is claimed by calling account. Parameters are passed as a body JSON object.

#### Headers

| Name                                            | Type   | Description              |
| ----------------------------------------------- | ------ | ------------------------ |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer token of the user |

#### Request Body

| Name                                     | Type   | Description                      |
| ---------------------------------------- | ------ | -------------------------------- |
| sensor<mark style="color:red;">\*</mark> | String | MAC address of sensor to reclaim |
| secret<mark style="color:red;">\*</mark> | String | Secret of sensor to reclaim      |

{% tabs %}
{% tab title="200: OK Sensor ownership was transferred" %}
```javascript
{
    "result": "success",
    "data": {
        "sensor": "C5:2A:E7:4D:CE:7F"
    }
}
```
{% endtab %}

{% tab title="400: Bad Request Missing parameter or user has full claim count" %}
```javascript
{
    'code': {'ER_CLAIM_COUNT_REACHED', 'ER_MISSING_ARGUMENT'}
}
```
{% endtab %}

{% tab title="401: Unauthorized User is not authenticated" %}
```javascript
{
    'code': 'ER_UNAUTHORIZED'
}
```
{% endtab %}

{% tab title="403: Forbidden macAddress and secret do not match" %}
```javascript
{
    'code': 'ER_FORBIDDEN'
}
```
{% endtab %}
{% endtabs %}

## Claim a subscription by a code

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/subscription`

This endpoints applies a new subscription to user immediately. Previous subscription is lost. Parameters are passed as JSON in body. The success response has full subscription history of user, with active subscription being first element of array of subscriptions.&#x20;

#### Headers

| Name                                            | Type   | Description              |
| ----------------------------------------------- | ------ | ------------------------ |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer token of the user |

#### Request Body

| Name                                   | Type   | Description           |
| -------------------------------------- | ------ | --------------------- |
| code<mark style="color:red;">\*</mark> | String | Code of subscription  |

{% tabs %}
{% tab title="200: OK Subscription was applied successfully" %}
```javascript
{
    "result": "success",
    "data": {
        "subscriptions": [
            {
                "subscriptionName": "DEV",
                "maxClaims": 25,
                "maxShares": 40,
                "maxSharesPerSensor": 5,
                "maxHistoryDays": 720,
                "maxResolutionMinutes": 1,
                "isActive": true,
                "startTime": 1673435374,
                "endTime": 1673608174
            },
            {
                "subscriptionName": "DEV",
                "maxClaims": 25,
                "maxShares": 40,
                "maxSharesPerSensor": 5,
                "maxHistoryDays": 720,
                "maxResolutionMinutes": 1,
                "isActive": false,
                "startTime": 1673435292,
                "endTime": 1673608092
            }
        ]
    }
}
```
{% endtab %}

{% tab title="400: Bad Request Missing code" %}
```javascript
{
    "result": "error",
    "error": "Invalid request format.",
    "code": "ER_INVALID_FORMAT"
}
```
{% endtab %}

{% tab title="401: Unauthorized Missing or invalid authorization header" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}

{% tab title="409: Conflict Subscription code is already used" %}
```javascript
{
    "result": "error",
    "error": "Code already claimed",
    "code": "ER_SUBSCRIPTION_CODE_USED"
}
```
{% endtab %}

{% tab title="404: Not Found Subscription code does not exist" %}
```javascript
{
    "result": "error",
    "error": "Code not found",
    "code": "ER_SUBSCRIPTION_NOT_FOUND"
}
```
{% endtab %}
{% endtabs %}

## Get subscription history

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/subscription`

Return array of JSON objects detaling the subscriptions user has had.&#x20;

#### Headers

| Name                                            | Type   | Description              |
| ----------------------------------------------- | ------ | ------------------------ |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer token of the user |

{% tabs %}
{% tab title="200: OK Returns subscription history" %}
```javascript
{
    "result": "success",
    "data": {
        "subscriptions": [
            {
                "subscriptionName": "DEV",
                "maxClaims": 25,
                "maxShares": 40,
                "maxSharesPerSensor": 5,
                "maxHistoryDays": 720,
                "maxResolutionMinutes": 1,
                "isActive": true,
                "startTime": 1673435374,
                "endTime": 1673608174
            },
            {
                "subscriptionName": "DEV",
                "maxClaims": 25,
                "maxShares": 40,
                "maxSharesPerSensor": 5,
                "maxHistoryDays": 720,
                "maxResolutionMinutes": 1,
                "isActive": false,
                "startTime": 1673435292,
                "endTime": 1673608092
            }
        ]
    }
}
```
{% endtab %}

{% tab title="403: Forbidden Request was not authenticated or authentication token was not valid" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endtab %}
{% endtabs %}

## Register a push notification token for user

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/push-register`

Register a device to Cloud so Cloud can send push notifications to user. Currently only alerts for Android and iOS are supported.&#x20;

Tokens must be unique, one token cannot be associated with two accounts. If token already exists in Ruuvi Cloud with another account, the token will be removed from old account.&#x20;

#### Headers

| Name                                            | Type   | Description              |
| ----------------------------------------------- | ------ | ------------------------ |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer token of the user |

#### Request Body

| Name                                    | Type   | Description                                                                                                                 |
| --------------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------- |
| token<mark style="color:red;">\*</mark> | String | Device identification token                                                                                                 |
| type<mark style="color:red;">\*</mark>  | String | Device type, e.g. "Android" or "iOS"                                                                                        |
| data                                    | String | Optional data to be passed to to push notification. Can be e.g. authentication token.                                       |
| params                                  | String | Optional parameters used internally by Ruuvi Cloud when delivering notifications. Currently unused,this is for future needs |
| name                                    | String | Human-readable device name, e.g. "Otso's mobile phone". Defaults to device type.                                            |

{% tabs %}
{% tab title="200: OK Token was successfully registered" %}
```javascript
{
    "result": "success",
    "data": {
        "tokenId": INT
    }
}
```
{% endtab %}

{% tab title="400: Bad Request Request had malformed data" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="401: Unauthorized Request did not have authentication" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="403: Forbidden Authentication was invalid" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="500: Internal Server Error Internal problem. Try again later. " %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}

## Remove a push notification token for user

<mark style="color:green;">`POST`</mark> `https://network.ruuvi.com/push-unregister`

Removes given token from user, e.g. when signing off from the app. This does not require authentication to ensure that a device can always unregister itself.

Either full token or Token ID must be given, but both are optional. If both arguments are given, either can be processed but not both in one request. &#x20;

#### Request Body

| Name  | Type   | Description                            |
| ----- | ------ | -------------------------------------- |
| token | String | Device identification token            |
| id    | String | Token ID received in listing of tokens |

{% tabs %}
{% tab title="200: OK Token was removed" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="400: Bad Request Message body did not have required data" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="500: Internal Server Error Internal problem. Try again later. " %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="404: Not Found Given token or ID was not found." %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}

## Get a list of tokens associated with user account

<mark style="color:blue;">`GET`</mark> `https://network.ruuvi.com/push-list`

List all tokens of user. Returns a listing of tokenId - name pairs.&#x20;

#### Headers

| Name                                            | Type   | Description              |
| ----------------------------------------------- | ------ | ------------------------ |
| Authorization<mark style="color:red;">\*</mark> | String | Bearer token of the user |

{% tabs %}
{% tab title="200: OK List was successfully retrieved" %}
```javascript
{
    "result": "success",
    "data": {
        "tokens": [
            {
                "id": 3308157406,
                "lastAccessed": 1674799893,
                "name": "Otso's landline"
            },
            {
                "id": 3721015809,
                "lastAccessed": 1674799924,
                "name": "Otso's mobile phone"
            }
        ]
    }
}
```
{% endtab %}

{% tab title="401: Unauthorized Authentication token was missing" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="403: Forbidden Authentication token is invalid" %}
```javascript
{
    // Response
}
```
{% endtab %}

{% tab title="500: Internal Server Error Iinternal problem. Try again later. " %}
```javascript
{
    // Response
}
```
{% endtab %}
{% endtabs %}

