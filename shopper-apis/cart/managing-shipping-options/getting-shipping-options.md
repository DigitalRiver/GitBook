---
description: Lear how to get shipping options.
---

# Getting shipping options

## Getting a shipping option by identifier

To [get a shipping option by identifier](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shipping-Options/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-options\~1%7BshippingOptionsId%7D/get), specify the shipping options identifier (`shippingOptionsId`) in the URI path.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options/{shippingOptionsId}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "shippingOptions": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options",
    "shippingOption": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options/5858800",
        "description": "UPS",
        "formattedCost": "19.99USD",
        "applyShippingOptionToCart": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/apply-shipping-option?shippingOptionId=5858800"
        }
      }
    ]
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting all shipping options

You can also [get all shipping options](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shipping-Options/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-options/get).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "shippingOption": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options/142400",
    "id": 142400,
    "description": "UPS Ground",
    "cost": {
      "currency": "USD",
      "value": "19.99"
    },
    "formattedCost": "19.99USD",
    "applyShippingOptionToCart": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/apply-shipping-option?shippingOptionId=142400"
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
