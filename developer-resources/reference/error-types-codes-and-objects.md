---
description: Learn about error types, codes, and objects.
---

# Error types, codes, and objects

## Change event error object

When DigitalRiver.js detects an error with an element, it returns an error object with the change event. This object will contain a type, code, and message.

{% tabs %}
{% tab title="Change Event Error object" %}
```javascript
{
    "type": "validation_error",
    "code": "invalid_card_number",
    "message": "Your card number is invalid."
}
```
{% endtab %}
{% endtabs %}

## Create source error object

DigitalRiver.js returns this error object within the [createSource](digitalriver-object.md#creating-sources) method if an error occurs with the tokenization request. This object will contain a type and an array of detailed messages explaining the error.

{% tabs %}
{% tab title="Create Source Error object" %}
```javascript
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
{% endtab %}
{% endtabs %}

## Error codes

The following table contains a list of DigitalRiver.js error codes.

{% hint style="info" %}
You must only indicate that the payment has been declined and do not share the code or descriptions below with the customer.
{% endhint %}

| Code                      | Description                                                                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `address_mismatch`        | There is a problem with your address.                                                                                                                                          |
| `invalid_expiration_date` | The card is expired or the expiration date is invalid.                                                                                                                         |
| `invalid_format`          | The format of your request is invalid.                                                                                                                                         |
| `invalid_parameter`       | The parameter is invalid. Check the [Digital River API Reference](https://www.digitalriver.com/docs/digital-river-api-reference) to see which values are valid and try again.  |
| `invalid_string_empty`    | The string value is empty. Provide a valid string value and try again.                                                                                                         |
| `method_not_allowed`      | The method is not allowed. Provide a valid method value and try again.                                                                                                         |
| `missing_parameter`       | A parameter is missing. Check the [Digital River API Reference](https://www.digitalriver.com/docs/digital-river-api-reference) to see which values are required and try again. |
| `not_found`               | The item requested was not found.                                                                                                                                              |
| `source_not_found`        | The source you have requested was not found.                                                                                                                                   |
| `unknown_error`           | An unknown error has occurred                                                                                                                                                  |
