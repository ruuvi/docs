---
description: 'Ruuvi Network (Serverless) user facing API. Lifecycle: in production'
---

# User API

User API uses a JSON based API to allow users to register, secure and edit their information as well as claim and share sensors, retrieve sensor data and alter their subscription details.

For example, if the body parameter in the sections below refers to an **email** field, the corresponding JSON payload would look like this:

```
{
    "email": "<YOUR VALUE>"
}
```

All authenticated queries are ratelimited to 4 \* MAX\_SENSORS\_OWNED + 0.1 \* MAX\_HISTORY\_DAYS per minute. For example user with Basic plan has maximum of 90 days of history on 25 sensors and can make up to 109 queries per minute. The throtteled response has response code of 429 and payload of:&#x20;

```
{
      result: 'error',
      error: 'Too many requests.',
      code: 'ER_THROTTLED'
}
```



{% swagger baseUrl="https://network.ruuvi.com" path="/register" method="post" summary="Register User or Reset Token" %}
{% swagger-description %}
Registers a new user or resets an existing user's password if the user already exists.
{% endswagger-description %}

{% swagger-parameter in="body" name="email" type="string" %}
Email address to be registered / reset
{% endswagger-parameter %}

{% swagger-response status="200" description="On a successful call, you will receive a 200 OK. An e-mail will be sent to the given address to confirm the registration.
In case of a reset, the token will be provided as a response to the call." %}
```
{
    "result": "success",
    "data": {
        "email": "matti@meikalainen.com"
    }
}
```
{% endswagger-response %}

{% swagger-response status="429: Too Many Requests" description="Over 10 calls in an hour" %}
```
{
      result: 'error',
      error: 'Too many requests.',
      code: 'ER_THROTTLED'
}
```
{% endswagger-response %}

{% swagger-response status="500" description="If a something goes wrong with the request itself, you might receive an Unknown error. Please contact your system administrator if this occurs." %}
```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/verify" method="get" summary="Verify Account" %}
{% swagger-description %}
Verifies the given e-mail address and finalizes creating the account and creating a Ruuvi Network subscription. Notice that the token for this end-point is delivered via e-mail by the 

**Register User**

 endpoint.
{% endswagger-description %}

{% swagger-parameter in="query" name="token" type="string" %}
Verification token (received in the e-mail)
{% endswagger-parameter %}

{% swagger-response status="200" description="On a successful response, you will receive the confirmation on the e-mail address an an access token to be used with other end-points.
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
{% endswagger-response %}

{% swagger-response status="403" description="Forbidden if user is not allowed to access resource." %}
```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endswagger-response %}

{% swagger-response status="500" description="(Actual code 493): You will receive an error if the token is invalid." %}
```
{
    "result": "error",
    "error": "Code used or expired.",
    "code": "ER_TOKEN_EXPIRED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/request-delete" baseUrl="https://network.ruuvi.com" summary="Request deletion of account" %}
{% swagger-description %}
This operation requests complete removal of user account from Ruuvi Cloud. After a successful call to this endpoint, user gets a verification email with a link to confirm deletion of account.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Bearer token to authorize the request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="email" required="true" %}
Email of account to delete
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Verification email has been sent" %}
```javascript
{
    "result": "success",
    "data": {
        "email": "otso+test3@ruuvi.com"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Missing authorization or email parameter" %}
```javascript
{
    "result": "error",
    "error": "<SPECIFIC ERROR>",
    "code": "ER_<ERROR>"
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Returned if Authorization token does not match email" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/verify-delete" baseUrl="https://network.ruuvi.com" summary="Verify account deletion operation" %}
{% swagger-description %}
Following actions will be done:

User sensors will be unshared&#x20;

Sensors shared to user will be removed.

&#x20;~~Data of user sensors will be deleted~~. (TODO)

&#x20;User account data, including sensor claims and settings, will be deleted.

&#x20;Account deletion is a permament action which cannot be undone
{% endswagger-description %}

{% swagger-parameter in="path" name="token" required="true" %}
Short verification string
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Account deletion was started" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Invalid or missing authorization token" %}
```javascript
{
   {
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="/claim" baseUrl="https://netowrk.ruuvi.com" summary="Claim a sensor for user" %}
{% swagger-description %}
After this call, given sensor is claimed under authenticated user account
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
BBearer token to authorize the request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" required="true" %}
MAC address of sensor to claim, e.g. "AA:BB:CC:11:22:33"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
Human-readable name of sensor, e.g. "Fridge temperature sensor"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="description" %}
Human-readable description of sensor, e.g. "Sensor in top shelf of fridge"
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Sensor was claimed successfully" %}
```javascript
{
    "result": "success",
    "data": {
        "sensor": "C5:2A:E7:4D:CE:7F"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Request had malformed JSON or was missing a required parameter.  Alternatively user account has reached subscription limit" %}
```javascript
{
    'code': {'ER_MISSING_ARGUMENT', 'ER_CLAIM_COUNT_REACHED'}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Request had no authorization token" %}
```javascript
{

}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Sensor is claimed by another account" %}
```javascript
{
    'code': 'ER_SENSOR_ALREADY_CLAIMED';
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Unexpected error occurred in handler" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/unclaim" method="post" summary="Unclaim a sensor from your user" %}
{% swagger-description %}
Unclaims a sensor from your user, revoking your own access to it and making it claimable by other users.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token to authorize the request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" type="string" %}
ID of the sensor to be unshared
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "result": "success"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/share" method="post" summary="Share a sensor" %}
{% swagger-description %}
You can share your sensor data with other users via 

**share**

 end-point. In addition to sensor you want to share, you must also include the e-mail address of the recipient. This will grant them access to the data via the 

**get**

 end-point.

\


Furthermore, it will also send the target user a notification e-mail about the new share. If the target user does not exist yet, an invitation to create an account will be sent to them and they will gain access upon sign up.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token to authorize the request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user" type="string" %}
E-mail of the user to share to
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" type="string" %}
Sensor ID to share
{% endswagger-parameter %}

{% swagger-response status="200" description="On success, you will get the shared sensor id returned back to you." %}
```
{
    "result": "success",
    "data": {
        "sensor": "<YOUR SENSOR ID>"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400" description="If the sharing failed due to malformed data, such as missing arguments." %}
```
{
    "result": "error",
    "error": "Invalid E-mail given.",
    "code": "ER_INVALID_EMAIL_ADDRESS"  
}
```
{% endswagger-response %}

{% swagger-response status="401" description="If an invalid or expired access token is provided, you will receive 401 Unauthorized." %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}

{% swagger-response status="404" description="If the user you tried share to is not found on the system." %}
```
{
    "result": "error",
    "error": "User not found.",
    "code": "ER_USER_NOT_FOUND"
}
```
{% endswagger-response %}

{% swagger-response status="409" description="You will receive a conflict if the sensor is already shared to the user." %}
```
{
    "result": "error",
    "error": "Sensor already shared to user.",
    "code": "ER_SENSOR_ALREADY_SHARED"
}
```
{% endswagger-response %}

{% swagger-response status="500" description="If something went wrong with the request, you will receive a 500 internal server error. Please contact your System Administrator." %}
```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/unshare" method="post" summary="Unshare a sensor" %}
{% swagger-description %}
Unshares (i.e. revokes access to) the sensor from a target user. This can also currently be used to remove sensors shared with your user.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" type="string" %}
ID of the sensor being unshared
{% endswagger-parameter %}

{% swagger-parameter in="body" name="user" type="string" %}
E-mail of the user the sensor is shared to. Optional if removing sensor shared to current user.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "result": "success"
}
```
{% endswagger-response %}

{% swagger-response status="400" description="Returned with Invalid or missing fields." %}
```
{
    "result": "error",
    "error": "<SPECIFIC ERROR>",
    "code": "ER_<ERROR>"
}
```
{% endswagger-response %}

{% swagger-response status="403" description="Returned when user" %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}

{% swagger-response status="404" description="Returned if shared sensor or user is not found." %}
```
{
    "result": "error",
    "error": "User not found.",
    "code": "ER_USER_NOT_FOUND"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/sensors" method="get" summary="Get your sensors" %}
{% swagger-description %}
Fetches a list of sensors you have access to including who those are shared to. This end-point deprecates the old 

_shared_

 end-point.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sensor" type="string" %}
Optionally filter only one sensor
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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
{% endswagger-response %}

{% swagger-response status="401" description="" %}
```
{
    "result": "error",
    "error": "Unauthorized.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/sensors-dense" baseUrl="https://network.ruuvi.com" summary="Get your sensors with calibration data, latest measurement, and alerts settings" %}
{% swagger-description %}
Fetches the list of claimed and shared sensors with calibration data, sensor last measurement, subscription type and alert settings. By default the endpoint returns only the claimed sensors with calibration data. Optional arguments must be passed to get shared sensors, last measurement, and alert settings. 
{% endswagger-description %}

{% swagger-parameter in="query" name="mode" type="string" %}
Fetch mode: [dense, sparse, mixed], determines how the data is returned. Default: mixed
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sensor" type="string" %}
Optionally filter only one sensor
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sharedToOthers" type="bool" %}
Optionally returns the list of users with whom each of the sensors is shared to
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sharedToMe" type="bool" %}
Optionally returns the sensors shared to the logged-in user alongside claimed sensors by the user
{% endswagger-parameter %}

{% swagger-parameter in="query" name="measurements" type="bool" %}
Optionally returns the latest measurement of each of the sensors in the collection. Returns also the subscription on which the data is based on. 
{% endswagger-parameter %}

{% swagger-parameter in="query" name="alerts" type="bool" %}
Optionally returns the alerts settings of each of the sensors in the collection
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
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
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/user" method="get" summary="Get User Info" %}
{% swagger-description %}
Fetches user information for an authenticated user.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authentication" type="string" %}
Authentication Bearer token retrieved from the login flow.
{% endswagger-parameter %}

{% swagger-response status="200" description="User information successfully retrieved." %}
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
{% endswagger-response %}

{% swagger-response status="401" description="Unauthorized request." %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/get" method="get" summary="Get Sensor data" %}
{% swagger-description %}
Returns the data points for the requested sensor. Notice that for implementing pagination, you can use **since** and **until** parameters with custom **limit** to segment your results as they are always returned in either ascending or descending order by timestamp.

Data can be fetched in dense, sparse and mixed mode. Dense mode returns highest data density possible, but has a limited time range before data is pruned to save storage space. Sparse mode has downsampled data, but time range is not limited. Mixed mode returns all the dense data available and rest of the time range is filled with sparse data
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token to authorize the request
{% endswagger-parameter %}

{% swagger-parameter in="query" name="mode" type="string" %}
Fetch mode: [dense, sparse, mixed], determines how the data is returned. Default: mixed
{% endswagger-parameter %}

{% swagger-parameter in="query" name="until" type="string" %}
Maximum timestamp of first returned result in Unix epoch format, in seconds. Default until now.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="since" type="string" %}
Minimum timestamp of first returned result in Unix epoch format, in seconds. Default 0. 
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" %}
Maximum amount of results returned (capped at 5000).
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sort" type="string" %}
Sort Direction for the result: [asc, desc]. Default descending
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sensor" type="string" required="true" %}
Sensor ID to retrieve the data 
{% endswagger-parameter %}

{% swagger-response status="200" description="Returns the most recent data points for the requested tag based on configuration and parameters.f" %}
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
{% endswagger-response %}

{% swagger-response status="400" description="" %}
```
{
    "result": "error",
    "error": "Invalid <SPECIFIC ERROR>",
    "code": "ER_INVALID_<SPECIFIC>"
}
```
{% endswagger-response %}

{% swagger-response status="401" description="In case of an invalid or expired authentication token, you will receive a unauthorized response." %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}

{% swagger-response status="403" description="If you have not claimed or been shared the target sensor, you will receive a Forbidden." %}
```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/update" method="post" summary="Update Sensor metadata" %}
{% swagger-description %}
Updates sensor metadata.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}

{% endswagger-parameter %}

{% swagger-parameter in="body" name="picture" type="string" %}
Filename of a picture (or URL if uploaded)
{% endswagger-parameter %}

{% swagger-parameter in="body" name="offsetHumidity" type="number" %}
Offset humidity to calibrate sensor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="offsetPressure" type="number" %}
Offset pressure to calibrate sensor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="offsetTemperature" type="number" %}
Offset temperature to calibrate sensor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="public" type="boolean" %}
If true, data will be publicly accessible.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" type="string" %}
Sensor ID to update
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" %}
Desired name of the tag
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="number" %}
Epoch timestamp in seconds of settings. If backend has fresher data stored, this will be ignored. 
{% endswagger-parameter %}

{% swagger-response status="200" description="Only returns the fields that had an update targeted to them." %}
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
{% endswagger-response %}

{% swagger-response status="403" description="" %}
```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endswagger-response %}

{% swagger-response status="404" description="" %}
```
{
    "result": "error",
    "error": "Sensor not claimed or found. Data not updated.",
    "code": "ER_SENSOR_NOT_FOUND"
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Cloud has fresher data than timestamp" %}

{% endswagger-response %}

{% swagger-response status="500" description="" %}
```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com/" path="upload" method="post" summary="Upload Sensor image (part 1)" %}
{% swagger-description %}
Retrieves a signed upload URL to a bucket. This makes the back-end ready for the image upload to happen.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="action" type="string" %}
One of: 

_upload_

, 

_reset_

 (default: 'upload' if not given')
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" type="string" %}
ID of the target Sensor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
(

**Required**

 when type is 'upload')

\


Content-Type of the desired image upload. Supported formats:

\


image/png

\


image/gif

\


image/jpeg
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "result": "success",
    "data": {
        "uploadURL": "<SIGNED UPLOAD URL>"
    }
}
```
{% endswagger-response %}

{% swagger-response status="403" description="" %}
```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="<URL FROM part 1>" path=" " method="put" summary="Upload the actual image" %}
{% swagger-description %}
Create a PUT request to the URL produced by /upload end-point with the data payload to complete the upload.
{% endswagger-description %}

{% swagger-parameter in="header" name="Content-Type" type="string" %}
Matching content type to part 1
{% endswagger-parameter %}

{% swagger-parameter in="body" name="Image binary data" type="object" %}
Binary data for the image upload
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
```
{% endswagger-response %}

{% swagger-response status="403" description="" %}
```
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/settings" method="get" summary="Get User Settings" %}
{% swagger-description %}
Gets the full list of existing user settings.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/settings" method="post" summary="Update user setting" %}
{% swagger-description %}
Sets a single user setting (currently).
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="value" type="string" %}
Setting value
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" %}
Setting key (alphanumeric with "_", "-" and "."
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="number" %}
Epoch timestamp in seconds of settings. If backend has fresher data stored, this will be ignored.
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "status": "success",
    "data": {
        "action": "<added|updated>"
    }
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Cloud has fresher data than timestamp" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/alerts" method="post" summary="Create and update Alerts" %}
{% swagger-description %}
Sets an alert on a sensor for a given metric. The alert condition is tested against the absolute value received from the sensors in conjunction with the use set offsets for that particular sensor.

Proposed values are marked with \*.&#x20;
{% endswagger-description %}

{% swagger-parameter in="body" name="counter" type="number" %}
For movement alerts, one can manually set the current number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" required="true" %}
One of: temperature, humidity, pressure, signal, movement, *offline
{% endswagger-parameter %}

{% swagger-parameter in="body" name="min" type="number" %}
Lower limit for the alert
{% endswagger-parameter %}

{% swagger-parameter in="body" name="max" type="number" %}
Upper limit for the alert
{% endswagger-parameter %}

{% swagger-parameter in="body" name="enabled" type="boolean" %}
Used to toggle alert on and off
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" type="string" %}
Sensor MAC of the target sensor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="timestamp" type="number" %}
Epoch timestamp in seconds of settings. If backend has fresher data stored, this will be ignored. 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="*delay" type="number" %}
How many *seconds* alert condition has to be valid before alert gets triggered. Delay is reset if alert is cleared. Defaults to 0. 
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "status": "success",
    "data": {
        "action": "<success|failed>"
    }
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Cloud has fresher data than timestamp" %}

{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/alerts" method="get" summary="Get alerts" %}
{% swagger-description %}
Fetches alerts for all sensors user has access to or a single sensor if optional parameter is provided.
{% endswagger-description %}

{% swagger-parameter in="body" name="sensor" type="string" %}
Optional Sensor MAC for filter the alerts
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```
{
    "status": "success",
    "data": {
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
                triggeredAt: <timestamp>,
                *delay: <number, positive integer>
            }
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/check" baseUrl="https://network.ruuvi.com" summary="Check if a sensor with given MAC address is claimed by someone" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="query" name="sensor" type="MAC address" required="true" %}
AA:BB:CC:DD:EE:FF (String)
{% endswagger-parameter %}

{% swagger-parameter in="header" required="true" name="Authorization" type="Bearer" %}
Bearer <Bearer Token>
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Masked email of sensor owner, empty string if sensor is not owned" %}
```javascript
{
    "status": "success",
    "data": {
        "email": <string>
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="If request doesn't have "sensor" parameter, or parameter is not a valid MAC address" %}
```javascript
    "status": "success",
    "data": {
        "email": <string>
    }
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="If there was no valid authentication" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="contest-sensor" baseUrl="https://network.ruuvi.com/" summary="Contest ownership of a sensor" %}
{% swagger-description %}
This call is used to reclaim a sensor claimed by someone else. After this endpoint returns 200, the sensor is claimed by calling account. Parameters are passed as a body JSON object.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" required="true" %}
MAC address of sensor to reclaim
{% endswagger-parameter %}

{% swagger-parameter in="body" name="secret" required="true" %}
Secret of sensor to reclaim
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Sensor ownership was transferred" %}
```javascript
{
    "result": "success",
    "data": {
        "sensor": "C5:2A:E7:4D:CE:7F"
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Missing parameter or user has full claim count" %}
```javascript
{
    'code': {'ER_CLAIM_COUNT_REACHED', 'ER_MISSING_ARGUMENT'}
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="User is not authenticated" %}
```javascript
{
    'code': 'ER_UNAUTHORIZED'
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="macAddress and secret do not match" %}
```javascript
{
    'code': 'ER_FORBIDDEN'
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="subscription" baseUrl="https://network.ruuvi.com/" summary="Claim a subscription by a code" %}
{% swagger-description %}
This endpoints applies a new subscription to user immediately. Previous subscription is lost. Parameters are passed as JSON in body. The success response has full subscription history of user, with active subscription being first element of array of subscriptions. 
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="code" required="true" %}
Code of subscription 
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Subscription was applied successfully" %}
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
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Missing code" %}
```javascript
{
    "result": "error",
    "error": "Invalid request format.",
    "code": "ER_INVALID_FORMAT"
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Missing or invalid authorization header" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Subscription code does not exist" %}
```javascript
{
    "result": "error",
    "error": "Code not found",
    "code": "ER_SUBSCRIPTION_NOT_FOUND"
}
```
{% endswagger-response %}

{% swagger-response status="409: Conflict" description="Subscription code is already used" %}
```javascript
{
    "result": "error",
    "error": "Code already claimed",
    "code": "ER_SUBSCRIPTION_CODE_USED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="/subscription" baseUrl="https://network.ruuvi.com" summary="Get subscription history" %}
{% swagger-description %}
Return array of JSON objects detaling the subscriptions user has had. 
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Returns subscription history" %}
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
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Request was not authenticated or authentication token was not valid" %}
```javascript
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="push-register" baseUrl="https://network.ruuvi.com/" summary="Register a push notification token for user" %}
{% swagger-description %}
Register a device to Cloud so Cloud can send push notifications to user. Currently only alerts for Android and iOS are supported.&#x20;

Tokens must be unique, one token cannot be associated with two accounts. If token already exists in Ruuvi Cloud with another account, the token will be removed from old account.&#x20;
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-parameter in="body" name="token" required="true" %}
Device identification token
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" required="true" %}
Device type, e.g. "Android" or "iOS"
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" %}
Human-readable device name, e.g. "Otso's mobile phone". Defaults to device type.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="data" %}
Optional data to be passed to to push notification. Can be e.g. authentication token. 
{% endswagger-parameter %}

{% swagger-parameter in="body" name="params" %}
Optional parameters used internally by Ruuvi Cloud when delivering notifications. Currently unused,this is for future needs
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Token was successfully registered" %}
```javascript
{
    "result": "success",
    "data": {
        "tokenId": INT
    }
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Request had malformed data" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Request did not have authentication" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Authentication was invalid" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Internal problem. Try again later. " %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="post" path="push-unregister" baseUrl="https://network.ruuvi.com/" summary="Remove a push notification token for user" %}
{% swagger-description %}
Removes given token from user, e.g. when signing off from the app. This does not require authentication to ensure that a device can always unregister itself.

Either full token or Token ID must be given, but both are optional. If both arguments are given, either can be processed but not both in one request. &#x20;
{% endswagger-description %}

{% swagger-parameter in="body" name="token" required="false" %}
Device identification token
{% endswagger-parameter %}

{% swagger-parameter in="body" name="id" %}
Token ID received in listing of tokens
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Token was removed" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="400: Bad Request" description="Message body did not have required data" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Given token or ID was not found." %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Internal problem. Try again later. " %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger method="get" path="push-list" baseUrl="https://network.ruuvi.com/" summary="Get a list of tokens associated with user account" %}
{% swagger-description %}
List all tokens of user. Returns a listing of tokenId - name pairs. 
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" required="true" %}
Bearer token of the user
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="List was successfully retrieved" %}
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
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Authentication token was missing" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="403: Forbidden" description="Authentication token is invalid" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="Iinternal problem. Try again later. " %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

