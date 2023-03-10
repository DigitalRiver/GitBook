---
description: Learn how to retrieve product information.
---

# Products

## Getting volume pricing for a specific product

The [`GET /v1/shoppers/me/products/{productId}/pricing/volume-pricing`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Products/paths/\~1v1\~1shoppers\~1me\~1products\~1%7BproductId%7D\~1pricing\~1volume-pricing/get) request retrieves volume pricing for a specific [product ](../../general-resources/admin-apis-reference/products.md)by its [product identifier](../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) (`productId`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/products/{productId}/pricing/volume-pricing' \
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

## Getting all products from the product catalog

The [`GET /v1/shoppers/me/products`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Products/paths/\~1v1\~1shoppers\~1me\~1products/get) request retrieves all products from the catalog.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/products' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "products": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products",
    "nextPage": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products?pageNumber=11&pageSize=1"
    },
    "previousPage": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products?pageNumber=9&pageSize=1"
    },
    "product": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/73248400",
        "displayName": "Class VI",
        "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft3/images/product/thumbnail/classVIThumb.jpg",
        "pricing": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/73248400/pricing",
          "formattedListPrice": "$79.99",
          "formattedSalePriceWithQuantity": "$79.99"
        },
        "addProductToCart": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=73248400",
          "cartUri": "https://api.digitalriver.com/v1/shoppers/me/carts/active?productId=73248400"
        }
      }
    ],
    "totalResults": 11,
    "totalResultPages": 11
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting a product by identifier

The [`GET /v1/shoppers/me/products/{productId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Products/paths/\~1v1\~1shoppers\~1me\~1products\~1%7BproductId%7D/get) request retrieves a specific product by its [product identifier](../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) (`productId`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/products/{productId}' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "product": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",
    "parentProduct": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200"
    },
    "categories": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/categories"
    },
    "familyAttributes": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/family-attributes"
    },
    "id": 64578500,
    "name": "Class I",
    "displayName": "Class I",
    "shortDescription": "Class I is the perfect GPS waypoint and route manager for the beginning or occasional GPS user.",
    "longDescription": "Class I is the fast and easy way to create, edit, and transfer waypoints and routes between your computer and your Garmin, Magellan, or Lowrance GPS. Using Class I, you can manage all of your waypoints and routes, and display them in lists sorted by name, elevation, or distance. Class I connects your GPS to the best mapping and information sites on the Internet, giving you one-click access to street and topo maps, aerial photos, weather forecasts, and nearby attractions.",
    "productType": "DOWNLOAD",
    "sku": "Class I",
    "externalReferenceId": "Test External Reference Number",
    "companyId": "demosft1",
    "displayableProduct": "true",
    "purchasable": "true",
    "manufacturerName": "Test Manufacturer Name",
    "manufacturerPartNumber": "Test Manufacturer Part Number",
    "minimumQuantity": "string",
    "maximumQuantity": "string",
    "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb.jpg",
    "productImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/detail/classIBox.jpg",
    "keywords": "testKeyword",
    "baseProduct": "false",
    "customAttributes": {
      "attribute": [
        {
          "name": "name",
          "value": "string",
          "type": "string"
        }
      ]
    },
    "pricing": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/pricing",
      "listPrice": {
        "currency": "USD",
        "value": "19.99"
      },
      "salePriceWithQuantity": {
        "currency": "USD",
        "value": "19.99"
      },
      "formattedListPrice": "$19.99",
      "formattedSalePriceWithQuantity": "$17.99",
      "msrpPrice": {
        "currency": "USD",
        "value": "19.99"
      },
      "formattedMsrpPrice": "$2.00",
      "listPriceIncludesTax": "false",
      "formattedCommitmentPrice": "$240.00",
      "commitmentPrice": {
        "currency": "USD",
        "value": "240.00"
      }
    },
    "addProductToCart": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=64578500",
      "cartUri": "https://api.digitalriver.com/v1/shoppers/me/carts/active?productId=64578500"
    },
    "transferProduct": {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/18977555",
      "displayName": "Transfer Product",
      "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/newImage.jpg",
      "addProductToCart": {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=18977555",
        "cartUri": "https://api.digitalriver.com/v1/shoppers/me/carts/active?productId=18977555"
      }
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting all products for a specified category

The [`GET /v1/shoppers/me/categories/{categoryId}/products`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Products/paths/\~1v1\~1shoppers\~1me\~1categories\~1%7BcategoryId%7D\~1products/get) request retrieves all products for a specified category (`categoryId`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/categories/{categoryId}/products' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "products": {
    "uri": "https://api.digitalriver.com/v1/shoppers/me/products",
    "product": [
      {
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200",
        "displayName": "Class I",
        "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft1/images/product/thumbnail/classIThumb_v2.jpg",
        "pricing": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200/pricing",
          "formattedListPrice": "$19.99",
          "formattedSalePriceWithQuantity": "$18.99"
        },
        "variations": {
          "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64358200/variations"
        }
      }
    ],
    "totalResults": 1,
    "totalResultPages": 1
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
