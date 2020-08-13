---
description: Ruuvi Network (Serverless) user facing API
---

# User API

User API uses a JSON based API to allow users to register, secure and edit their information as well as claim and share tags, retrieve tag data and alter their subscription details.

For example, if the body parameter in the sections below refers to an **email** field, the corresponding JSON payload would look like this:

```text
{
    "email": "<YOUR VALUE>"
}
```

{% api-method method="post" host="https://api.placeholder.com/dev" path="/register" %}
{% api-method-summary %}
Register User
{% endapi-method-summary %}

{% api-method-description %}
Registers a new user or resets an existing user's password.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="reset" type="integer" required=false %}
Valid values: 1 or 0. If 1 is given, will issue a password reset
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
Email address to be registered
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

{% api-method-response-example httpCode=409 %}
{% api-method-response-example-description %}
If a pending request already exists with the same data, you might receive a Conflict response.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "E-mail already exists."
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
    "error": "Unknown error occurred."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.placeholder.com/dev" path="/verify" %}
{% api-method-summary %}
Verify Account
{% endapi-method-summary %}

{% api-method-description %}
Verifies the given e-mail address and finalizes creating the account. Notice that the token for this end-point is delivered via e-mail by the **Register User** endpoint.
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
        "access_token": "<NEW ACCESS TOKEN>"
    }
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
    "error": "Provided token is invalid or expired."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.placeholder.com/dev" path="/claim" %}
{% api-method-summary %}
Claim Tag to your user
{% endapi-method-summary %}

{% api-method-description %}
Claims an unclaimed tag for your user. This will allow you to fetch its data.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer token to authorize the request4
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="tag" type="string" required=true %}
ID of the claimed tag
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
On success, you will receive a corresponding result and the claimed Tag ID repeated back to you.
{% endapi-method-response-example-description %}

```
{
    "result": "success",
    "data": {
        "Tag": "<CLAIMED TAG ID>"
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
    "error": "Unauthorized request."
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=409 %}
{% api-method-response-example-description %}
If the tag has been claimed, you will receive a 409 Conflict.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Tag already claimed."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.placeholder.com/dev" path="/share" %}
{% api-method-summary %}
Share a tag
{% endapi-method-summary %}

{% api-method-description %}
You can share your Tag data with other users via **share** end-point. In addition to tag you want to share, you must also include the e-mail address of the recipient. This will grant them access to the data via the **get** end-point.
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

{% api-method-parameter name="tag" type="string" required=true %}
Tag ID to share
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
On success, you will get the shared tag id returned back to you.
{% endapi-method-response-example-description %}

```
{
    "result": "success",
    "data": {
        "tag": "<YOUR TAG ID>"
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
    "error": "Invalid E-mail given."
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
    "error": "Unauthorized request."
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
    "error": "User not found."
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=409 %}
{% api-method-response-example-description %}
You will receive a conflict if the tag is already shared to the user.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Tag already shared to user."
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
    "error": "Unknown error occurred."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.placeholder.com/dev" path="/user" %}
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
        "Email": "my-email@email.com",
        "Tags": [
            {
                "Tag": "CDCDCDCDED",
                "Owner": 1
            },
            {
                "Tag": "ABBACDBEST",
                "Owner": 0
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
    "error": "Unauthorized request."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.placeholder.com/dev" path="/get" %}
{% api-method-summary %}
Get Tag data
{% endapi-method-summary %}

{% api-method-description %}
Returns the data points for the requested tag.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=false %}
Bearer token to authorize the request
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="tag" type="string" required=false %}
Tag ID to retrieve the data 
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
        "tag": "<TAG ID>",
        "total": <TOTAL MEASUREMENTS RETURNED>,
        "measurements": [
            {
                "GatewayMac": "<SOURCE GATEWAY MAC>",
                "Coordinates": "<COORDINATES / N/A>",
                "RSSI": <RSSI>,
                "MeasurementTimestamp": <UNIZ TIMESTAMP OF MEASUREMENT>,
                "SensorData": "<HEX ENCODED SENSOR DATA>",
                "SensorId": "<TAG ID>"
            },
            ...
        ]
    }
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
    "error": "Unauthorized request."
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}
If you have not claimed or been shared the target tag, you will receive a Forbidden.
{% endapi-method-response-example-description %}

```
{
    "result": "error",
    "error": "Forbidden.
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
If no data is found, you will receive a 404 Not Found.
{% endapi-method-response-example-description %}

```
{
    "status": "error",
    "error": "Not found."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

