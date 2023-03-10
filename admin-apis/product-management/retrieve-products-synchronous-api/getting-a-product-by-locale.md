---
description: Learn how to get the information for a product by locale.
---

# Getting a product by locale

The following [`GET /v1/products/{productid or ERID}/locales/{locale}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Product-\(Synchronous-API\)/paths/\~1v1\~1products\~1%7BproductId%7D\~1locales\~1%7Blocale%7D/get) request retrieves data associated with a specific locale for an individual or base product. All product variations (if any) for a base product will appear as a URL in the response.

To get a specific product by locale, you must provide either a [`productId`](broken-reference) or [`ERID`](broken-reference)  and the locale (for example, `en_us`). If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% tabs %}
{% tab title="productId cURL" %}
The following example uses `productId` to get the locale for a specific product.

{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/{productId}/locales/en_US' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/{ERID}/locales/en_US' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The request returns the product information for the specific locale in the [synchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.&#x20;

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

The response returns an error if the locale is not found or is invalid.
{% endtab %}
{% endtabs %}
