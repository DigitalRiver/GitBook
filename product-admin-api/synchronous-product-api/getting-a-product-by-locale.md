---
description: Learn how to get the information for a product by locale.
---

# Getting a product by locale

The following `GET /products/{productid}/locales/{locale}` request retrieves data associated with a specific locale for an individual or base product. All product variations (if any) for a base product will appear as a URL in the response. <mark style="background-color:orange;">??? TODO: Add a link to the GET request. ???</mark>

To get a specific product by locale, you must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid)  and the locale (for example, `en_us`). If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% tabs %}
{% tab title="productId request" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/products/{productId}/locales/en_US' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/products/{ERID}/locales/en_US' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

The request returns the product information for a specific locale in the response.&#x20;

{% tabs %}
{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
[
  {
    "productType": "BASE",
    "companyId": "digitalriver",
    "siteIds": [
      "domoSite1",
      "domoSite2"
    ],
    "id": 1234567800,
    "state": "Deployed",
    "locked": false,
    "version": 1,
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

The response returns an error if the locale is not found or invalid.



## Key read-only attributes

The following details describe the key read-only attributes when getting production information by locale. These attributes will be ignored if they appear in the payload. For a complete list, refer to the <mark style="background-color:orange;">??? add a link to getting a base or individual product ???</mark> in the API Reference document.

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
