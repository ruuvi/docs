---
description: Newsletter consent API behavior for Ruuvi applications and the webshop
---

# Marketing consent

Ruuvi Cloud provides a single interface for reading and changing a user's Ruuvi newsletter subscription. Sendy is the source of truth; marketing consent is not stored as a normal cloud application setting.

The complete public request and response schemas are available in the [User API OpenAPI documentation](user-api/). This page explains how clients should use the API and interpret Sendy's state.

## Subscription states

Every successful read or update returns:

```json
{
  "result": "success",
  "data": {
    "consent": true,
    "status": "subscribed"
  }
}
```

`consent` is `true` only for `subscribed`. Clients should use `status` when deciding how to present or enable subscription controls.

| Status | Meaning | Recommended switch state | User may change it |
| --- | --- | --- | --- |
| `subscribed` | The address is subscribed. | On | Yes |
| `unsubscribed` | The address has unsubscribed. | Off | Yes |
| `not_found` | The address is not present in the list. This is normal before the first subscription. | Off | Yes |
| `unconfirmed` | Sendy is waiting for double opt-in confirmation. | Off | No |
| `bounced` | Delivery to the address has failed. | Off | No |
| `soft_bounced` | Delivery has temporarily failed. | Off | No |
| `complained` | The recipient reported the newsletter as spam. | Off | No |

An `unconfirmed` state may be shown with a message asking the user to check their email. Mobile applications show the confirmation dialog only when an update initiated by the user returns `unconfirmed`, not whenever the account page is opened.

## Authenticated User API

These endpoints operate on the email address belonging to the bearer token. Clients must not send an email address in either request.

### Read consent

`GET https://network.ruuvi.com/marketing-consent`

```http
Authorization: Bearer <token>
```

### Update consent

`POST https://network.ruuvi.com/marketing-consent`

```http
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
  "consent": true,
  "silent": true,
  "joiningSource": "android",
  "language": "EN"
}
```

The request fields are:

| Field | Required | Description |
| --- | --- | --- |
| `consent` | Yes | `true` subscribes and `false` unsubscribes. |
| `silent` | No | Defaults to `false`. When `true`, Sendy bypasses double opt-in for a subscription. It has no effect when unsubscribing. |
| `joiningSource` | Yes | Lowercase client identifier stored in Sendy's `joiningSource` custom field, such as `ios`, `android`, or `webshop`. Maximum 32 characters. |
| `language` | Yes | Two-letter application language. Input is case-insensitive; Ruuvi Cloud stores it in uppercase, matching the website's WPML format, for example `EN`, `FI`, or `DE`. |

The mobile applications send `silent: true` when the user changes the switch. This makes an app-initiated subscription immediate regardless of region. They must still display an existing `unconfirmed` state if the subscription was started elsewhere with double opt-in.

## Webshop API

The webshop endpoints are for trusted server-to-server integrations. The shop credential must not be embedded in a browser or mobile application.

Authenticate requests with:

```http
X-Shop-Secret: ******
```

### Read consent by email

`POST https://network.ruuvi.com/internal/marketing-consent/status`

```json
{
  "email": "customer@example.com"
}
```

### Update consent by email

`POST https://network.ruuvi.com/internal/marketing-consent`

```json
{
  "email": "customer@example.com",
  "consent": true,
  "silent": false,
  "joiningSource": "webshop",
  "language": "DE"
}
```

The update fields follow the authenticated User API rules, with the addition of the required `email` field. The webshop determines whether its flow requires double opt-in by choosing the `silent` value.

## Errors and client behavior

Invalid input returns an error response with an `ER_INVALID_ARGUMENT` code. Missing or invalid credentials return an authorization error. Sendy communication or configuration failures return an internal error.

A marketing-consent read failure must not prevent sign-in or the normal cloud synchronization cycle. When an update fails, clients should restore the previous switch state rather than displaying an unconfirmed new state.
