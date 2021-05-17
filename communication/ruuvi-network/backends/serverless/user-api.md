---
description: Ruuvi Network (Serverless) user facing API
---

# User API

User API uses a JSON based API to allow users to register, secure and edit their information as well as claim and share sensors, retrieve sensor data and alter their subscription details.

For example, if the body parameter in the sections below refers to an **email** field, the corresponding JSON payload would look like this:

```text
{
    "email": "<YOUR VALUE>"
}
```

{% api-method method="post" host="https://network.ruuvi.com" path="/register" %}
{% api-method-summary %}
Register User or Reset Token
{% endapi-method-summary %}

{% api-method-description %}
Registers a new user or resets an existing user's password if the user already exists.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="email" type="string" required=true %}
Email address to be registered / reset
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
On a successful call, you will receive a 200 OK. An e-mail will be sent to the given address to confirm the registration.  
In case of a reset, the token will be provided as a response to the call.
{% endapi-method-response-example-description %}

```
{
    "result": "success",
    "data": {
        "email": "matti@meikalainen.com"
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
If a something goes wrong with the request itself, you might receive an Unknown error. Please contact your system administrator if this occurs.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://network.ruuvi.com" path="/verify" %}
{% api-method-summary %}
Verify Account
{% endapi-method-summary %}

{% api-method-description %}
Verifies the given e-mail address and finalizes creating the account and creating a Ruuvi Network subscription. Notice that the token for this end-point is delivered via e-mail by the **Register User** endpoint.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="token" type="string" required=true %}
Verification token \(received in the e-mail\)
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
On a successful response, you will receive the confirmation on the e-mail address an an access token to be used with other end-points.  
Store it well as the only way to retrieve it is to go through the reset flow again.
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}
Forbidden if user is not allowed to access resource.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
\(Actual code 493\): You will receive an error if the token is invalid.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Code used or expired.",
    "code": "ER_TOKEN_EXPIRED"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://network.ruuvi.com" path="/claim" %}
{% api-method-summary %}
Claim a Sensor to your user
{% endapi-method-summary %}

{% api-method-description %}
Claims an unclaimed sensor for your user. This will allow you to fetch its data.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token to authorize the request
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=false %}
Name the tag on claiming
{% endapi-method-parameter %}

{% api-method-parameter name="sensor" type="string" required=true %}
ID of the claimed tag
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
On success, you will receive a corresponding result and the claimed Sensor ID repeated back to you.
{% endapi-method-response-example-description %}

```
{
    "result": "success",
    "data": {
        "sensor": "<CLAIMED SENSOR ID>"
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
In case of an invalid or expired token, you will receive Unauthorized.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=409 %}
{% api-method-response-example-description %}
If the sensor has been claimed, you will receive a 409 Conflict.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Sensor already claimed.",
    "code": "ER_SENSOR_ALREADY_CLAIMED"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://network.ruuvi.com" path="/unclaim" %}
{% api-method-summary %}
Unclaim a sensor from your user
{% endapi-method-summary %}

{% api-method-description %}
Unclaims a sensor from your user, revoking your own access to it and making it claimable by other users.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token to authorize the request
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="sensor" type="string" required=true %}
ID of the sensor to be unshared
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "success"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://network.ruuvi.com" path="/share" %}
{% api-method-summary %}
Share a sensor
{% endapi-method-summary %}

{% api-method-description %}
You can share your sensor data with other users via **share** end-point. In addition to sensor you want to share, you must also include the e-mail address of the recipient. This will grant them access to the data via the **get** end-point.  
Furthermore, it will also send the target user a notification e-mail about the new share.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token to authorize the request
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="user" type="string" required=true %}
E-mail of the user to share to
{% endapi-method-parameter %}

{% api-method-parameter name="sensor" type="string" required=true %}
Sensor ID to share
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
On success, you will get the shared sensor id returned back to you.
{% endapi-method-response-example-description %}

```
{
    "result": "success",
    "data": {
        "sensor": "<YOUR SENSOR ID>"
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
If the sharing failed due to malformed data, such as missing arguments.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Invalid E-mail given.",
    "code": "ER_INVALID_EMAIL_ADDRESS"  
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
If an invalid or expired access token is provided, you will receive _401 Unauthorized_.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
If the user you tried share to is not found on the system.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "User not found.",
    "code": "ER_USER_NOT_FOUND"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=409 %}
{% api-method-response-example-description %}
You will receive a conflict if the sensor is already shared to the user.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Sensor already shared to user.",
    "code": "ER_SENSOR_ALREADY_SHARED"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
If something went wrong with the request, you will receive a 500 internal server error. Please contact your System Administrator.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://network.ruuvi.com" path="/unshare" %}
{% api-method-summary %}
Unshare a sensor
{% endapi-method-summary %}

{% api-method-description %}
Unshares \(i.e. revokes access to\) the sensor from a target user. This can also currently be used to remove sensors shared with your user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token of the user
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="sensor" type="string" required=true %}
ID of the sensor being unshared
{% endapi-method-parameter %}

{% api-method-parameter name="user" type="string" required=false %}
E-mail of the user the sensor is shared to. Optional if removing sensor shared to current user.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "success"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Returned with Invalid or missing fields.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "<SPECIFIC ERROR>",
    "code": "ER_<ERROR>"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}
Returned when user
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Returned if shared sensor or user is not found.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "User not found.",
    "code": "ER_USER_NOT_FOUND"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://network.ruuvi.com" path="/shared" %}
{% api-method-summary %}
Get your shared sensors
{% endapi-method-summary %}

{% api-method-description %}
Fetches a list of sensors you have shared to other users
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token of the user
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

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
                "sharedTo": "<EMAIL OF TARGET USER>"
            },
            ...
        ]
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unauthorized.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://network.ruuvi.com" path="/user" %}
{% api-method-summary %}
Get User Info
{% endapi-method-summary %}

{% api-method-description %}
Fetches user information for an authenticated user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Authentication Bearer token retrieved from the login flow.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
User information successfully retrieved.
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Unauthorized request.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://network.ruuvi.com" path="/get" %}
{% api-method-summary %}
Get Sensor data
{% endapi-method-summary %}

{% api-method-description %}
Returns the data points for the requested sensor. Notice that for implementing pagination, you can use **since** and **until** parameters with custom **limit** to segment your results as they are always returned in either ascending or descending order by timestamp.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token to authorize the request
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="mode" type="string" required=false %}
Fetch mode: \[dense, sparse, mixed\], determines how the data is returned. Default: mixed
{% endapi-method-parameter %}

{% api-method-parameter name="until" type="string" required=false %}
Maximum timestamp of first returned result in Unix epoch format
{% endapi-method-parameter %}

{% api-method-parameter name="since" type="string" required=false %}
Minimum timestamp of first returned result in Unix epoch format
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="string" required=false %}
Maximum amount of results returned \(capped at 100\)
{% endapi-method-parameter %}

{% api-method-parameter name="sort" type="string" required=false %}
Sort Direction for the result: \[asc, desc\]
{% endapi-method-parameter %}

{% api-method-parameter name="sensor" type="string" required=true %}
Sensor ID to retrieve the data 
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Returns the most recent data points for the requested tag based on configuration and parameters.f
{% endapi-method-response-example-description %}

```
{
    "result": "success",
    "data": {
        "sensor": "<SENSOR ID>",
        "total": <TOTAL MEASUREMENTS RETURNED>,
        "name": "<SENSOR NAME>",
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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Invalid <SPECIFIC ERROR>",
    "code": "ER_INVALID_<SPECIFIC>"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
In case of an invalid or expired authentication token, you will receive a unauthorized response.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unauthorized request.",
    "code": "ER_UNAUTHORIZED"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}
If you have not claimed or been shared the target sensor, you will receive a Forbidden.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://network.ruuvi.com" path="/update" %}
{% api-method-summary %}
Update Sensor metadata
{% endapi-method-summary %}

{% api-method-description %}
Updates sensor metadata.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="offsetHumidity" type="number" required=false %}
Offset humidity to calibrate sensor
{% endapi-method-parameter %}

{% api-method-parameter name="offsetPressure" type="number" required=false %}
Offset pressure to calibrate sensor
{% endapi-method-parameter %}

{% api-method-parameter name="offsetTemperature" type="number" required=false %}
Offset temperature to calibrate sensor
{% endapi-method-parameter %}

{% api-method-parameter name="public" type="boolean" required=false %}
If true, data will be publicly accessible.
{% endapi-method-parameter %}

{% api-method-parameter name="sensor" type="string" required=true %}
Sensor ID to update
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
Desired name of the tag
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Only returns the fields that had an update targeted to them.
{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Sensor not claimed or found. Data not updated.",
    "code": "ER_SENSOR_NOT_FOUND"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Unknown error occurred.",
    "code": "ER_INTERNAL"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://network.ruuvi.com/" path="upload" %}
{% api-method-summary %}
Upload Sensor image \(part 1\)
{% endapi-method-summary %}

{% api-method-description %}
Retrieves a signed upload URL to a bucket. This makes the back-end ready for the image upload to happen.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token of the user
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="action" type="string" required=false %}
One of: _upload_, _reset_ \(default: 'upload' if not given'\)
{% endapi-method-parameter %}

{% api-method-parameter name="sensor" type="string" required=true %}
ID of the target Sensor
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=true %}
\(**Required** when type is 'upload'\)  
Content-Type of the desired image upload. Supported formats:  
image/png  
image/gif  
image/jpeg
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "success",
    "data": {
        "uploadURL": "<SIGNED UPLOAD URL>"
    }
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Forbidden.",
    "code": "ER_FORBIDDEN"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="<URL FROM part 1>" path=" " %}
{% api-method-summary %}
Upload the actual image
{% endapi-method-summary %}

{% api-method-description %}
Create a PUT request to the URL produced by /upload end-point with the data payload to complete the upload.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
Matching content type to part 1
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Image binary data" type="object" required=true %}
Binary data for the image upload
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

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://network.ruuvi.com" path="/settings" %}
{% api-method-summary %}
Get User Settings
{% endapi-method-summary %}

{% api-method-description %}
Gets the full list of existing user settings.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token of the user
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://network.ruuvi.com" path="/settings" %}
{% api-method-summary %}
Update user setting
{% endapi-method-summary %}

{% api-method-description %}
Sets a single user setting \(currently\).
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token of the user
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="value" type="string" required=true %}
Setting value
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
Setting key \(alphanumeric with "\_", "-" and "."
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "status": "success",
    "data": {
        "action": "<added|updated>"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://network.ruuvi.com" path="/setAlert" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}
Sets an alert on a sensor for a given metric. The alert condition is tested against the absolute value received from the sensors in conjunction with the use set offsets for that particular sensor.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="type" type="string" required=true %}
One of: temperature, humidity, pressure
{% endapi-method-parameter %}

{% api-method-parameter name="min" type="string" required=true %}
Lower limit for the alert
{% endapi-method-parameter %}

{% api-method-parameter name="max" type="string" required=true %}
Upper limit for the alert
{% endapi-method-parameter %}

{% api-method-parameter name="enabled" type="boolean" required=true %}
Used to toggle alert on and off
{% endapi-method-parameter %}

{% api-method-parameter name="sensor" type="string" required=true %}
Sensor MAC of the target sensor
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
    "status": "success",
    "data": {
        "action": "<success|failed>"
    }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://network.ruuvi.com" path="/getAlerts" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="sensor" type="string" required=true %}
Sensor MAC for which to fetch the alerts.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

