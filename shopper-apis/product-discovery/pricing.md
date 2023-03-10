---
description: Learn how to get pricing for a specific product.
---

# Pricing

## Getting pricing for a specific product

The [GET /v1/shoppers/me/products/{productId}/pricing](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Pricing/paths/\~1v1\~1shoppers\~1me\~1products\~1%7BproductId%7D\~1pricing/get) request retrieves volume pricing for a specific [product identifier](../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) (`productId`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/products/{productId}/pricing' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "volumePricing": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/73248500/pricing/volume-pricing",
    "tier": [
      {
        "from": 1,
        "to": 1,
        "pricing": {
          "listPrice": {
            "currency": "USD",
            "value": "19.99"
          },
          "listPriceWithQuantity": {
            "currency": "USD",
            "value": "19.99"
          },
          "salePriceWithQuantity": {
            "currency": "USD",
            "value": "19.99"
          },
          "formattedListPrice": "$8.00",
          "formattedListPriceWithQuantity": "$8.00",
          "formattedSalePriceWithQuantity": "$8.00",
          "totalDiscountWithQuantity": {
            "currency": "USD",
            "value": "19.99"
          },
          "formattedTotalDiscountWithQuantity": "$0.00",
          "discountDescription": "string",
          "feePricing": {
            "salePriceWithFeesAndQuantity": {
              "currency": "USD",
              "value": "19.99"
            },
            "formattedSalePriceWithFeesAndQuantity": "$8.00"
          },
          "listPriceIncludesTax": "false",
          "msrpPrice": {
            "currency": "USD",
            "value": "19.99"
          },
          "formattedMsrpPrice": "string"
        }
      }
    ],
    "formattedSalesPriceRange": "$5.00-$8.00"
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
