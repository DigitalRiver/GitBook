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
--header 'authorization: Basic ***\
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

See [Shipping options](../../../general-resources/shopper-apis-reference/carts/shipping-options.md) for more information.

## Getting all shipping options

You can also [get all shipping options](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Shipping-Options/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-options/get).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/carts/active/shipping-options' \
--header 'authorization: Basic ***\
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

See [shipping options](../../../general-resources/shopper-apis-reference/carts/shipping-options.md#shipping-option-query-parameters) query parameters for more information.

## Shipping options

You can retrieve the [shipping options for a cart](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shipping-Options/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-options\~1{shippingOptionsId}/get) or [all shipping options](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Shipping-Options/paths/\~1v1\~1shoppers\~1me\~1carts\~1active\~1shipping-options/get). The `shippingOptions` object in the response retrieves the discounted shipping rate based on the matching deployed [shipping discount offer](providing-a-shipping-discount.md#creating-a-shipping-discount-offer). A successful request returns the `costWithDiscount` and `formattedCostWithDiscount` .

| Parameter                   | Description                                                                                                                                                                                                                                                   |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `costWithDiscount`          | The sum of the shipping cost with discounts.                                                                                                                                                                                                                  |
| `formattedCostWithDiscount` | The sum of the shipping cost with a discount in locale currency format (for example, $ 19.14). Contact your Digital River team to set up the currency symbol, decimal separator, and number of fractional digits for the formatted cost with discount amount. |

{% tabs %}
{% tab title="JSON" %}
{% code overflow="wrap" %}
```json
{
    "shippingOption": {
        "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/carts/active/shipping-options/167400",
        "id": 167400,
        "description": "Express",
        "cost": {
            "currency": "USD",
            "value": 12.5
        },
        "formattedCost": "12.50USD",
        "costWithDiscount": {
            "currency": "USD",
            "value": 10.87
        },
        "formattedCostWithDiscount": "10.87USD",
        "applyShippingOptionToCart": {
            "uri": "http://dispatch-test.digitalriver.com/v1/shoppers/me/carts/active/apply-shipping-option?shippingOptionId=167400"
        }
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
