---
description: 'Lifecycle: Alpha'
---

# WhereOS

{% api-method method="post" host="https://whereos.ruuvi.com" path="/stream/post?applicationid=387c6e87-f916-4c95-b067-b1d87726dde6&pipelinename=write" %}
{% api-method-summary %}
Gateway data
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get free cakes.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
"application/json"
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="applicationid" type="string" required=true %}
"387c6e87-f916-4c95-b067-b1d87726dde"
{% endapi-method-parameter %}

{% api-method-parameter name="pipelinename" type="string" required=true %}
"write"
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="data" type="object" required=true %}
JSON data object with gateway data
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```
{    "name": "Cake's name",    "recipe": "Cake's recipe name",    "cake": "Binary cake"}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```
{    "message": "Ain't no cake like that."}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



