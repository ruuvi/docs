---
description: Ruuvi Network (Serverless) user facing API
---

# User API

User API uses a JSON based API to allow users to register, secure and edit their information as well as claim and share sensors, retrieve sensor data and alter their subscription details.

For example, if the body parameter in the sections below refers to an **email **field, the corresponding JSON payload would look like this:

```
{
    "email": "<YOUR VALUE>"
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

{% swagger baseUrl="https://network.ruuvi.com" path="/claim" method="post" summary="Claim a Sensor to your user" %}
{% swagger-description %}
Claims an unclaimed sensor for your user. This will allow you to fetch its data.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token to authorize the request
{% endswagger-parameter %}

{% swagger-parameter in="body" name="name" type="string" %}
Name the tag on claiming
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" type="string" %}
ID of the claimed tag
{% endswagger-parameter %}

{% swagger-response status="200" description="On success, you will receive a corresponding result and the claimed Sensor ID repeated back to you." %}
```
{
    "result": "success",
    "data": {
        "sensor": "<CLAIMED SENSOR ID>"
    }
}
```
{% endswagger-response %}

{% swagger-response status="401" description="In case of an invalid or expired token, you will receive Unauthorized." %}
```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endswagger-response %}

{% swagger-response status="409" description="If the sensor has been claimed, you will receive a 409 Conflict." %}
```
{
    "result": "error",
    "error": "Sensor already claimed.",
    "code": "ER_SENSOR_ALREADY_CLAIMED"
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
                "sharedTo": [
                    "<EMAIL OF TARGET USER 1>",
                    ...
                ]
            },
            ...
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
Returns the data points for the requested sensor. Notice that for implementing pagination, you can use 

**since**

 and 

**until **

parameters with custom 

**limit**

 to segment your results as they are always returned in either ascending or descending order by timestamp.
{% endswagger-description %}

{% swagger-parameter in="header" name="Authorization" type="string" %}
Bearer token to authorize the request
{% endswagger-parameter %}

{% swagger-parameter in="query" name="mode" type="string" %}
Fetch mode: [dense, sparse, mixed], determines how the data is returned. Default: mixed
{% endswagger-parameter %}

{% swagger-parameter in="query" name="until" type="string" %}
Maximum timestamp of first returned result in Unix epoch format
{% endswagger-parameter %}

{% swagger-parameter in="query" name="since" type="string" %}
Minimum timestamp of first returned result in Unix epoch format
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" %}
Maximum amount of results returned (capped at 100)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sort" type="string" %}
Sort Direction for the result: [asc, desc]
{% endswagger-parameter %}

{% swagger-parameter in="query" name="sensor" type="string" %}
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

_reset _

(default: 'upload' if not given')
{% endswagger-parameter %}

{% swagger-parameter in="body" name="sensor" type="string" %}
ID of the target Sensor
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
(

**Required **

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
{% endswagger %}

{% swagger baseUrl="https://network.ruuvi.com" path="/alerts" method="post" summary="Create and update Alerts" %}
{% swagger-description %}
Sets an alert on a sensor for a given metric. The alert condition is tested against the absolute value received from the sensors in conjunction with the use set offsets for that particular sensor.
{% endswagger-description %}

{% swagger-parameter in="body" name="counter" type="number" %}
For movement alerts, one can manually set the current number
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
One of: temperature, humidity, pressure, signal, movement
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
                triggeredAt: <timestamp>
            }
        ]
    }
}
```
{% endswagger-response %}
{% endswagger %}
