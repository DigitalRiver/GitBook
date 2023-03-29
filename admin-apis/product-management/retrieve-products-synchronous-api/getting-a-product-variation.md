---
description: Learn how to get information for a product variation.
---

# Getting a product variation

The following [`GET /v1/products/{baseProductId or baseERID}/variations/{variationProductId or variationERID}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Product-\(Synchronous-API\)/paths/\~1v1\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D/get) request retrieves data for all locales associated with the specified product variation.

To get a specific product variation, you must provide the [product identifiers (`productId`)](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or a unique [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) for both the base product and the variation product. If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% tabs %}
{% tab title="cURL" %}
The following example gets a specific product variation with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request GET https://api.digitalriver.com/v1/products/{baseProductId}/variations/{variationProductId}' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
request GET 'https://api.digitalriver.com/v1/products/{baserERID}/variations/{variationERID}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The request returns the product variation information in the response.&#x20;

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
