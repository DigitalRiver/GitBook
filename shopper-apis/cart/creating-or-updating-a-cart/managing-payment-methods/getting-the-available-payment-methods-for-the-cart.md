---
description: Learn how to get the available payment methods for a cart.
---

# Getting the available payment methods for the cart

You can [get the available payment methods for a cart](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Payment-Methods/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1payment-methods/get).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location -g --request GET ' https://api.digitalriver.com/v1/shoppers/me/carts/active/payment-methods' \
--header 'Authorization: bearer {{access_token}}' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/payment-methods",
  "applyPaymentMethod": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/apply-payment-method"
  },
  "paymentMethod": [
    {
      "type": "americanExpress",
      "displayName": "American Express",
      "description": "American Express"
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

See [Payment methods query parameters](../../../../general-resources/shopper-apis-reference/carts/payment-methods.md#payment-methods-query-parameters) for more information.
