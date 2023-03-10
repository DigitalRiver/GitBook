---
description: Learn about error types, codes, and objects.
---

# Error types, codes, and objects

## Change event error object

When a DigitalRiver.js detects an error with an element, it returns an error object with the change event. This object will contain a type, code, and message.

{% tabs %}
{% tab title="Change Event Error object" %}
{% code overflow="wrap" %}
```json
{
    "type": "validation_error",
    "code": "invalid_card_number",
    "message": "Your card number is invalid."
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Create source error object

DigitalRiver.js returns this error object within the [createSource ](digitalriver-object.md#digitalriver-createsource-element-sourcedata)method if an error occurs with the tokenization request. This object will contain a type and an array of messages that will explain the error in detail.

{% tabs %}
{% tab title="Create Source Error object" %}
{% code overflow="wrap" %}
```json
{
    "type": "bad_request",
    "errors": [{
           "code": "invalid_parameter",
           "parameter": "owner.firstName",
           "message": "'' is not a valid owner.firstname."
    },
    {
            "code": "currency_unsupported",
            "parameter": "currency",
            "message": "currency 'xyz' is not supported."
    }]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Error types

The following table contains a list of DigitalRiver.js error types.

### `bad_request`

The server could not process the request due to a client error (for example, malformed request syntax). Correct the problem and try again.

### `not_found`

The server can't find the requested resource. No indication is given of whether the condition is temporary or permanent.

### `request_timeout`

The client did not produce the request within the time that the server was prepared to wait. Resend the request without modifications at any later time.

### `internal_server_error`

The server encountered an unexpected problem that prevented it from fulfilling the request.

### `unauthorized`

The request requires user authentication. Resend the request with valid user authentication.

### `too_many_requests`

The user sent too many requests in a given amount of time ("rate limiting"). The response should include details explaining the condition and may include a Retry-After header indicating how long to wait before sending a new request.

### `conflict`

There is a request conflict with the current state of the server.

Conflicts are most likely to occur in response to a PUT request. For example, you may get a 409 response when uploading a file that is older than the one already on the server resulting in a version control conflict.

### `validation_error`

Errors triggered by our client-side libraries when failing to validate fields (for example, when a card number or expiration date is invalid or incomplete).

Used by: DigitalRiver.js

### `no_network`

There is no network coverage or cellular data connection.

## Error codes

The following table contains a list of DigitalRiver.js error codes.

{% hint style="info" %}
It's important that you only indicate that the payment has been declined and do not share the code or descriptions listed below with the customer.
{% endhint %}

### `address_mismatch`

There is a problem with your address.

### `invalid_expiration_date`

The card is expired, or the expiration date is invalid.&#x20;

### `invalid_format`

The format of your request is invalid.

### `invalid_parameter`

The parameter is invalid. Check the [Shopper APIs](https://www.digitalriver.com/docs/commerce-shopper-api/) or [Admin APIs](https://www.digitalriver.com/docs/commerce-admin-api/) reference to see which values are valid and try again.

### `invalid_string_empty`

The string value is empty. Provide a valid string value and try again.

### `method_not_allowed`

The method is not allowed. Provide a valid method value and try again.

### `missing_parameter`

A parameter is missing. Check the [Shopper APIs](https://www.digitalriver.com/docs/commerce-shopper-api/) or [Admin APIs](https://www.digitalriver.com/docs/commerce-admin-api/) reference to see which values are required and try again.

### `not_found`

The item requested was not found.

### `source_not_found`

The source you requested was not found.

### `unknown_error`

An unknown error has occurred.
