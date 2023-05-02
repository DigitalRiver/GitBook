---
description: Learn how to get information for a product variation by locale.
---

# Getting a product variation by locale

Basic The following [`GET /v1/products/{ProductId or ERID}/variation/{productId or ERID}/locales/{locale}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Product-\(Synchronous-API\)/paths/\~1v1\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D\~1locales\~1%7Blocale%7D/get) request retrieves data for a specific locale associated with a particular product variation.&#x20;

To get a product variation for a specific base product and locale, you must provide one of the following options:&#x20;

* A [`productId`](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md)  for the base product, the `variationProductId` for the product variation and the `locale`.&#x20;
* An [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) for the base product, and  a `variationERID` for the product variation, and the `locale`. If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% tabs %}
{% tab title="productId cURL" %}
The following example gets product variation for a specific base product and a locale with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/{productId}/variation/{variationProductId}/locales/{locale}' \
--header 'Authorization: Basic <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request GET 'https://api.digitalriver.com/v1/products/{ERID}/variation/{variationERID}/locales/{locale}' \
--header 'Authorization: Basic &#x3C;API_key>' \
<strong>--header 'header x-erid-as-pid=true' \
</strong><strong>...
</strong></code></pre>

The response returns an error if the locale is not found or is invalid.
{% endtab %}

{% tab title="200 OK response " %}
The request returns the product variation information for a specific locale in the [synchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.&#x20;

```
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
{% endtab %}
{% endtabs %}
