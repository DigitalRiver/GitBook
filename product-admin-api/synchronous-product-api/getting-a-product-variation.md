---
description: Learn how to get information for a product variation.
---

# Getting a product variation

You can [get a product variation for a specific base product](getting-a-product-variation.md#getting-a-product-variation-for-a-specific-base-product) or [a specific product variation](getting-a-product-variation.md#getting-a-specific-product-variation). Note that both of these calls result in the same response when specifying the same `variationId`. If you know the `variationId`, you only need to [get a specific product variation](getting-a-product-variation.md#getting-a-specific-product-variation).&#x20;

## Getting a product variation for a specific base product

The following `GET /products/{baseProductId}/variations/{variationId}` request retrieves data for all locales associated with the specified product variation.  <mark style="background-color:orange;">??? TODO: Add a link to the GET request. ???</mark>

To get a specific product variation for a specific base product, you must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)and the variation identifier (`variationId`) or a unique [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid) for both. If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% tabs %}
{% tab title="productId request" %}
{% code overflow="wrap" %}
```http
curl --location --curl --location --request GET 'https://api.digitalriver.com/products/{baseProductId}/variations/{variationId}' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
{% code overflow="wrap" %}
```http
request GET 'https://api.digitalriver.com/products/{baseERID}/variations/{variationId}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

The request returns the product variation information in the response.&#x20;

{% tabs %}
{% tab title="200 OK Response" %}
{% code overflow="wrap" %}
```json
[
  {
    "productType": "VARIATION",
    "companyId": "digitalriver",
    "siteIds": [
      "domoSite1",
      "domoSite2"
    ],
    "id": 1234567900,
    "state": "Deployed",
    "locked": false,
    "version": 1,
    "variationName": "Business, 1-year-license",
    "baseProductId": 1234567800,
    "varyingAttributes": [
      {
        "attributeName": "fulfillmentType",
        "attributeValue": "Download"
      }
    ],
    "deploymentRequiredChanges": {
      "fulfillmentTypes": [
        "Download"
      ],
      "otherFulfillmentIntegration": {
        "fulfillerIds": [
          "digitalRiver"
        ]
      },
      "transferProduct": 2234567800,
      "upgradeProducts": [
        3234567800
      ],
      "downgradeProducts": [
        4234567800
      ]
    },
    "liveChanges": {
      "externalReferenceId": "sku-1234-5678-xyz",
      "catalogs": [
        {
          "catalogId": 123456000,
          "catalogName": "a catalog",
          "categories": [
            {
              "categoryId": 19000000,
              "categoryName": "a category"
            }
          ],
          "prices": [
            {
              "type": "listPrice",
              "priceListName": "Unit Price",
              "taxInclusive": true,
              "prices": [
                {
                  "currency": "USD",
                  "locale": "en_US",
                  "configuredPrice": 15.99,
                  "calculatedPrice": 0
                }
              ]
            }
          ]
        }
      ]
    },
    "localizations": [
      {
        "locale": "en_US",
        "isDefault": true,
        "groups": [
          {
            "groupId": 11000,
            "groupName": "Storefront Settings",
            "attributes": {
              "property1": "string",
              "property2": "string"
            }
          }
        ]
      }
    ]
  }
]
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Getting a specific product variation

The following `GET /products/product/variations/{variationId}` request retrieves data for all locales associated with the specified product variation. <mark style="background-color:orange;">??? Add a link to the GET request. ???</mark>

To get a specific product variation, you must provide the variation identifier (`variationId`) or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid). If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% code overflow="wrap" %}
```
request GET 'https://api.digitalriver.com/products/product/variations/{variaionId}' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}

The request returns the product variation information in the response.&#x20;

{% code title="Response example" overflow="wrap" %}
```json
[
  {
    "productType": "VARIATION",
    "companyId": "digitalriver",
    "siteIds": [
      "domoSite1",
      "domoSite2"
    ],
    "id": 1234567900,
    "state": "Deployed",
    "locked": false,
    "version": 1,
    "variationName": "Business, 1-year-license",
    "baseProductId": 1234567800,
    "varyingAttributes": [
      {
        "attributeName": "fulfillmentType",
        "attributeValue": "Download"
      }
    ],
    "deploymentRequiredChanges": {
      "fulfillmentTypes": [
        "Download"
      ],
      "otherFulfillmentIntegration": {
        "fulfillerIds": [
          "digitalRiver"
        ]
      },
      "transferProduct": 2234567800,
      "upgradeProducts": [
        3234567800
      ],
      "downgradeProducts": [
        4234567800
      ]
    },
    "liveChanges": {
      "externalReferenceId": "sku-1234-5678-xyz",
      "catalogs": [
        {
          "catalogId": 123456000,
          "catalogName": "a catalog",
          "categories": [
            {
              "categoryId": 19000000,
              "categoryName": "a category"
            }
          ],
          "prices": [
            {
              "type": "listPrice",
              "priceListName": "Unit Price",
              "taxInclusive": true,
              "prices": [
                {
                  "currency": "USD",
                  "locale": "en_US",
                  "configuredPrice": 15.99,
                  "calculatedPrice": 0
                }
              ]
            }
          ]
        }
      ]
    },
    "localizations": [
      {
        "locale": "en_US",
        "isDefault": true,
        "groups": [
          {
            "groupId": 11000,
            "groupName": "Storefront Settings",
            "attributes": {
              "property1": "string",
              "property2": "string"
            }
          }
        ]
      }
    ]
  }
]
```
{% endcode %}



## Key read-only attributes

The following details describe the key read-only attributes when getting information production variation information by locale. These attributes will be ignored if they appear in the payload. For a complete list, refer to the <mark style="background-color:orange;">??? add a link to getting a product variation ???</mark> in the API Reference document.

### `companyId`&#x20;

The company identifier (owner of this product). This field is read-only and will be ignored in create/update/delete requests.&#x20;

### `id`&#x20;

The individual product identifier (productId), base product identifier (baseProductId), product variation identifier (`productVariationId`) or external reference identifier (ERID). &#x20;

### `liveChanges.catalogs.categories.categoryName`

The name of the category for the default locale.

### `liveChanges.catalogs.pricing.priceListName`

The name of the price list.

### `liveChanges.catalogs.pricing.prices.calculatedPrice`

The calculated price if the price was not configured for a specific currency and locale (optional) and conversion rate is available.

### `liveChanges.catalogs.pricing.taxinclusive`

Indicates whether or not the price list is tax inclusive.

### `localizations.groups.groupId`

The product family's group identifier. Global Commerce only needs this attribute key when updating data.&#x20;

### `localizations.groups.groupName`

The product family's group name. Global Commerce only needs this attribute key when updating data.&#x20;

### `locked`&#x20;

Indicates whether the product is locked or unlocked. When the product is locked, the product is not editable.&#x20;

### `productType`&#x20;

The product type. Once created, the product type cannot be changed. The possible product types are as follows:&#x20;

* **`BASE`**: A base product has one or more product variations such as different colors, sizes, or versions.&#x20;
* **`INDIVIDUAL`**: An individual product a single item or many single items sold as a single product (such as a collection or box set. An individual product is a single item or many single items sold as a single product such as a collection or box set.&#x20;
* **`VARIATION`**: A variation of a base product such as different colors, sizes, or versions.

### `siteIds`&#x20;

One or more site identifiers are associated with a product.

### `state`&#x20;

The current state of the product. The value changes automatically when you deploy, update, or retire the product. The possible states are as follows:&#x20;

* **`Deployed`**: The status indicates the product is available in your store.&#x20;
* **`Design`**: The status indicates you created or updated the product. It will not be available in the store until you deploy the product.&#x20;
* **`Retired`**: This status indicates the product is retired and will not appear in the store. Once retired, you can still search for the retired product by using `GET /products/{productId}` request or within Global Commerce.

### `version`

The current version of the product by state. This value is controlled by Digital River. The possible states are as follows:&#x20;

* **`Deployed`**: The status indicates the product is available in your store.
* **`Design`**: The status indicates you created or updated the product. It will not be available in the store until you deploy the product.&#x20;
* **`Retired`**: This status indicates the product is retired and will not appear in the store. Once retired, you can still search for the retired product by using `GET /products/{productId}` request or within Global Commerce.
