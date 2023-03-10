---
description: Learn how to retrieve product variation information.
---

# Product variations

## Getting product variations

The [`GET /v1/shoppers/me/products/{productId}/variations`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Product-Variations) request gets all [product variations](../../general-resources/admin-apis-reference/products.md#product-variations) for a specified [product identifier](../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) (`productId`) (`productId`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/products/{productId}/variations{
  "variations": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200/variations",
    "product": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
        "displayName": "Class I",
        "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
        "pricing": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/pricing",
          "formattedListPrice": "$19.99",
          "formattedSalePriceWithQuantity": "$17.99"
        },
        "addProductToCart": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=64578500",
          "cartUri": "https://api.digitalriver.com/v1/shoppers/me/carts/active?productId=64578500"
        }
      }
    ]
  }
}{
  "variations": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200/variations",
    "product": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
        "displayName": "Class I",
        "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
        "pricing": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/pricing",
          "formattedListPrice": "$19.99",
          "formattedSalePriceWithQuantity": "$17.99"
        },
        "addProductToCart": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=64578500",
          "cartUri": "https://api.digitalriver.com/v1/shoppers/me/carts/active?productId=64578500"
        }
      }
    ]
  }
}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "variations": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200/variations",
    "product": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
        "displayName": "Class I",
        "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
        "pricing": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/pricing",
          "formattedListPrice": "$19.99",
          "formattedSalePriceWithQuantity": "$17.99"
        },
        "addProductToCart": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=64578500",
          "cartUri": "https://api.digitalriver.com/v1/shoppers/me/carts/active?productId=64578500"
        }
      }
    ]
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
