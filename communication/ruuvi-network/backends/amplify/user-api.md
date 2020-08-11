---
description: Ruuvi Network (Serverless) user facing API
---

# User API

User API uses a JSON based API to allow users to register, secure and edit their information as well as claim and share tags, retrieve tag data and alter their subscription details.

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



