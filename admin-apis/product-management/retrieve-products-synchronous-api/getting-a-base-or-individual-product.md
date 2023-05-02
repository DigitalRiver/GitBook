---
description: Learn how to get the information for a base or individual product.
---

# Getting a base or individual product

## Getting a base or individual product

The following [`GET /v1/products/{productId, ERID, baseProductId, or baseProductERID}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Product-\(Synchronous-API\)/paths/\~1v1\~1products\~1%7BproductId%7D/get) request retrieves data for an individual or base product. All product variations (if any) for a base product will appear as a URL in the response.&#x20;

To get a specific product, you must provide either a [`productId`](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md). If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% hint style="info" %}
Duplicate ERIDs are not allowed. To prevent duplicate ERIDs, [enable the Enforce Unique Value](broken-reference) when [configuring company settings](https://help.digitalriver.com/internal-help/gc/Administration/Company/Configuring-company-settings.htm) in Global Commerce. This ensures that you won't accidentally provide an ERID that would result in duplicate products in the response if you searched for a product by ERID.
{% endhint %}

{% tabs %}
{% tab title="productId cURL" %}
The following example gets a specific base or individual product with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/{productId or baseProductId}' \
--header 'Authorization: Basic <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/{ERID or baseProductERID}' \
--header 'Authorization: Basic <API_key>' \
--header 'header x-erid-as-pid=true' \
...
```
{% endcode %}
{% endtab %}

{% tab title="productId 200 OK response " %}
The request returns the product information for the specified `productId` in the [synchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.&#x20;

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

{% tab title="ERID 200 OK response" %}
The request returns the product information for the specified `externalReferenceId` in the [synchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.&#x20;

{% code overflow="wrap" %}
```json
[
    {
        "productType": "INDIVIDUAL",
        "companyId": "acme",
        "siteIds": [
            "acme"
        ],
        "id": "51954990080",
        "state": "DESIGN",
        "locked": false,
        "version": 1,
        "deploymentRequiredChanges": {
            "fulfillmentTypes": [],
            "otherFulfillmentIntegration": {
                "fulfillerIds": []
            },
            "upgradeProducts": [],
            "downgradeProducts": []
        },
        "liveChanges": {
            "externalReferenceId": "external-reference-id-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
            "catalogs": [
                {
                    "catalogId": "4783669800",
                    "catalogName": "acme",
                    "categories": [],
                    "pricing": [
                        {
                            "type": "listPrice",
                            "priceListName": "acme",
                            "taxInclusive": false,
                            "prices": [
                                {
                                    "currency": "CAD",
                                    "locale": "en_CA"
                                },
                                {
                                    "currency": "CAD",
                                    "locale": "en_US"
                                },
                                {
                                    "currency": "USD",
                                    "locale": "en_US",
                                    "configuredPrice": 10.00
                                },
                                {
                                    "currency": "CAD",
                                    "locale": "fr_CA"
                                },
                                {
                                    "currency": "ARS"
                                },
                                {
                                    "currency": "AUD"
                                },
                                {
                                    "currency": "BRL"
                                },
                                {
                                    "currency": "CAD"
                                },
                                {
                                    "currency": "CHF"
                                },
                                {
                                    "currency": "CLP"
                                },
                                {
                                    "currency": "CNY"
                                },
                                {
                                    "currency": "COP"
                                },
                                {
                                    "currency": "CZK"
                                },
                                {
                                    "currency": "DKK"
                                },
                                {
                                    "currency": "EGP"
                                },
                                {
                                    "currency": "EUR"
                                },
                                {
                                    "currency": "GBP"
                                },
                                {
                                    "currency": "HKD"
                                },
                                {
                                    "currency": "HUF"
                                },
                                {
                                    "currency": "IDR"
                                },
                                {
                                    "currency": "ILS"
                                },
                                {
                                    "currency": "INR"
                                },
                                {
                                    "currency": "JPY"
                                },
                                {
                                    "currency": "KRW"
                                },
                                {
                                    "currency": "MXN"
                                },
                                {
                                    "currency": "MYR"
                                },
                                {
                                    "currency": "NOK"
                                },
                                {
                                    "currency": "NZD"
                                },
                                {
                                    "currency": "OMR"
                                },
                                {
                                    "currency": "PEN"
                                },
                                {
                                    "currency": "PLN"
                                },
                                {
                                    "currency": "RUB"
                                },
                                {
                                    "currency": "SEK"
                                },
                                {
                                    "currency": "SGD"
                                },
                                {
                                    "currency": "THB"
                                },
                                {
                                    "currency": "TRY"
                                },
                                {
                                    "currency": "TWD"
                                },
                                {
                                    "currency": "USD"
                                },
                                {
                                    "currency": "VEF"
                                },
                                {
                                    "currency": "ZAR"
                                }
                            ]
                        },
                        {
                            "type": "subscriptionRenewalPrice",
                            "priceListName": "Subscription Renewal Price list",
                            "taxInclusive": false,
                            "prices": [
                                {
                                    "currency": "ARS"
                                },
                                {
                                    "currency": "EUR"
                                },
                                {
                                    "currency": "GBP"
                                },
                                {
                                    "currency": "USD"
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
                        "groupId": "2",
                        "groupName": "Storefront Settings",
                        "attributes": {
                            "longDescription": "longDescription-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "nonSolr": true,
                            "keywords": "keywords-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "displayName": "demo-display-name-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "taxableUnspscCode": "43230000",
                            "confirmAddlInfo": "confirmAddlInfo-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "shortDescription": "shortDescription-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "isViewable": true,
                            "taxableProductCode": "4323.320_D",
                            "isOrderable": true,
                            "returnMethod": "LOD",
                            "emailAddlInfoText": "emailAddlInfoText-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "name": "demo-name-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "emailAddlInfo": "emailAddlInfo-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "minOrderQuantity": 0,
                            "privateStoreOnly": false,
                            "productReturnMethod": "ByAgentAndSelfService",
                            "sku": "demo-sku-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "maxOrderQuantity": 0
                        }
                    },
                    {
                        "groupId": "10",
                        "groupName": "Subscription",
                        "attributes": {
                            "freeExtension": "2_WEEK",
                            "timeIntervalForTrialReminderNotifications": [
                                "30",
                                "15",
                                "7",
                                "2"
                            ],
                            "gracePeriod": "1_WEEK",
                            "timeIntervalForUpgradeReminderNotificationsPostCreation": [
                                "7",
                                "15",
                                "30",
                                "90"
                            ],
                            "timeIntervalForReminderNotifications": [
                                "90",
                                "30",
                                "15",
                                "7"
                            ],
                            "suppressOFIInQuantityIncrease": false,
                            "suppressDRMInUpgradeDowngrade": false,
                            "suppressOFIInUpgradeDowngrade": false,
                            "suppressDRMInQuantityIncrease": false,
                            "timeIntervalForReminderNotificationsPostExpiration": [
                                "7",
                                "15",
                                "30",
                                "90"
                            ],
                            "autoRenewalDateBasis": "PurchaseDate",
                            "timeIntervalForUpgradeReminderNotificationsPreExpiration": [
                                "97",
                                "37",
                                "22",
                                "14"
                            ],
                            "isFreeTrial": true,
                            "combinedRenewalPeriod": 1,
                            "timeIntervalForCCExpirationReminderNotifications": [
                                "30",
                                "15",
                                "7"
                            ],
                            "duration": "TWO_MONTH",
                            "timeIntervalForManualReminderNotifications": [
                                "90",
                                "30",
                                "15",
                                "7"
                            ],
                            "isDistinctScheduleTurnedOn": false,
                            "isCombinedRenewal": true,
                            "suppressDRMInRenewal": false,
                            "paymentSchedule": "matchRecurrence",
                            "isAutomatic": true,
                            "numOfDaysPriorExpirationForRenewalPreFirst": 30,
                            "isChangeProductAsRenewal": false,
                            "freeTrialPeriod": 45,
                            "includeRenewalProductInUpgradeList": true,
                            "numOfDaysPriorExpirationForRenewal": 4,
                            "suppressOFIInTrialConversion": true,
                            "numOfDaysPriorExpirationForRenewalFirst": 15,
                            "timeIntervalForUpgradeReminderNotificationsPostExpiration": [
                                "97",
                                "37",
                                "22",
                                "14"
                            ],
                            "postExpirationBillingAttemptIntervalInDays": 7,
                            "suppressOFIInRenewal": true,
                            "suppressDRMInTrialConversion": false,
                            "trialPostExpirationBillingAttemptIntervalInDays": 7,
                            "trialGracePeriod": "1_MONTH",
                            "timeIntervalForTrialManualReminderNotifications": [
                                "30",
                                "15",
                                "7",
                                "2"
                            ]
                        }
                    },
                    {
                        "groupId": "16",
                        "groupName": "Export Controls",
                        "attributes": {
                            "manufactureCountry": "US",
                            "eccn": "3A992"
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

## Getting the deployed or retired versions of a product

To [retrieve a filtered list of deployed or retired products](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Retrieve-Product-\(Synchronous-API\)/paths/\~1v1\~1products\~1%7BproductId%7D/get), specify the [`version` ](../../../general-resources/admin-apis-reference/products.md#version)query parameter. The `version` values are `DEPLOYED` and `RETIRED`. The request returns products with the specified values. See the [`version` ](../../../general-resources/admin-apis-reference/products.md#version)query parameter for more information.

{% tabs %}
{% tab title="cURL with RETIRED query parameter" %}
The following example gets retired versions of a specific product with a `productId`.

{% code overflow="wrap" %}
```json
curl --location --request GET 'https://api.digitalriver.com/v1/products/{productId}?version=RETIRED' \
--header 'Authorization: Basic <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

<pre class="language-json" data-overflow="wrap"><code class="lang-json"><strong>curl --location --request GET 'https://api.digitalriver.com/v1/products/{ERID}?version=RETIRED' \
</strong>--header 'Authorization: Basic &#x3C;API_key>' \
--header 'header x-erid-as-pid=true' \
...
</code></pre>
{% endtab %}

{% tab title="200 OK response" %}
The request returns the product information for the specified `productId` in the [synchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.&#x20;

{% code overflow="wrap" %}
```json
[
    {
        "productType": "INDIVIDUAL",
        "companyId": "acme",
        "siteIds": [
            "acme"
        ],
        "id": "51954990080",
        "state": "RETIRED",
        "locked": false,
        "version": 1,
        "deploymentRequiredChanges": {
            "fulfillmentTypes": [],
            "otherFulfillmentIntegration": {
                "fulfillerIds": []
            },
            "upgradeProducts": [],
            "downgradeProducts": []
        },
        "liveChanges": {
            "externalReferenceId": "external-reference-id-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
            "catalogs": [
                {
                    "catalogId": "4783669800",
                    "catalogName": "acme",
                    "categories": [],
                    "pricing": [
                        {
                            "type": "listPrice",
                            "priceListName": "acme",
                            "taxInclusive": false,
                            "prices": [
                                {
                                    "currency": "CAD",
                                    "locale": "en_CA"
                                },
                                {
                                    "currency": "CAD",
                                    "locale": "en_US"
                                },
                                {
                                    "currency": "USD",
                                    "locale": "en_US",
                                    "configuredPrice": 10.00
                                },
                                {
                                    "currency": "CAD",
                                    "locale": "fr_CA"
                                },
                                {
                                    "currency": "ARS"
                                },
                                {
                                    "currency": "AUD"
                                },
                                {
                                    "currency": "BRL"
                                },
                                {
                                    "currency": "CAD"
                                },
                                {
                                    "currency": "CHF"
                                },
                                {
                                    "currency": "CLP"
                                },
                                {
                                    "currency": "CNY"
                                },
                                {
                                    "currency": "COP"
                                },
                                {
                                    "currency": "CZK"
                                },
                                {
                                    "currency": "DKK"
                                },
                                {
                                    "currency": "EGP"
                                },
                                {
                                    "currency": "EUR"
                                },
                                {
                                    "currency": "GBP"
                                },
                                {
                                    "currency": "HKD"
                                },
                                {
                                    "currency": "HUF"
                                },
                                {
                                    "currency": "IDR"
                                },
                                {
                                    "currency": "ILS"
                                },
                                {
                                    "currency": "INR"
                                },
                                {
                                    "currency": "JPY"
                                },
                                {
                                    "currency": "KRW"
                                },
                                {
                                    "currency": "MXN"
                                },
                                {
                                    "currency": "MYR"
                                },
                                {
                                    "currency": "NOK"
                                },
                                {
                                    "currency": "NZD"
                                },
                                {
                                    "currency": "OMR"
                                },
                                {
                                    "currency": "PEN"
                                },
                                {
                                    "currency": "PLN"
                                },
                                {
                                    "currency": "RUB"
                                },
                                {
                                    "currency": "SEK"
                                },
                                {
                                    "currency": "SGD"
                                },
                                {
                                    "currency": "THB"
                                },
                                {
                                    "currency": "TRY"
                                },
                                {
                                    "currency": "TWD"
                                },
                                {
                                    "currency": "USD"
                                },
                                {
                                    "currency": "VEF"
                                },
                                {
                                    "currency": "ZAR"
                                }
                            ]
                        },
                        {
                            "type": "subscriptionRenewalPrice",
                            "priceListName": "Subscription Renewal Price list",
                            "taxInclusive": false,
                            "prices": [
                                {
                                    "currency": "ARS"
                                },
                                {
                                    "currency": "EUR"
                                },
                                {
                                    "currency": "GBP"
                                },
                                {
                                    "currency": "USD"
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
                        "groupId": "2",
                        "groupName": "Storefront Settings",
                        "attributes": {
                            "longDescription": "longDescription-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "nonSolr": true,
                            "keywords": "keywords-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "displayName": "demo-display-name-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "taxableUnspscCode": "43230000",
                            "confirmAddlInfo": "confirmAddlInfo-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "shortDescription": "shortDescription-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "isViewable": true,
                            "taxableProductCode": "4323.320_D",
                            "isOrderable": true,
                            "returnMethod": "LOD",
                            "emailAddlInfoText": "emailAddlInfoText-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "name": "demo-name-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "emailAddlInfo": "emailAddlInfo-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "minOrderQuantity": 0,
                            "privateStoreOnly": false,
                            "productReturnMethod": "ByAgentAndSelfService",
                            "sku": "demo-sku-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "maxOrderQuantity": 0
                        }
                    },
                    {
                        "groupId": "10",
                        "groupName": "Subscription",
                        "attributes": {
                            "freeExtension": "2_WEEK",
                            "timeIntervalForTrialReminderNotifications": [
                                "30",
                                "15",
                                "7",
                                "2"
                            ],
                            "gracePeriod": "1_WEEK",
                            "timeIntervalForUpgradeReminderNotificationsPostCreation": [
                                "7",
                                "15",
                                "30",
                                "90"
                            ],
                            "timeIntervalForReminderNotifications": [
                                "90",
                                "30",
                                "15",
                                "7"
                            ],
                            "suppressOFIInQuantityIncrease": false,
                            "suppressDRMInUpgradeDowngrade": false,
                            "suppressOFIInUpgradeDowngrade": false,
                            "suppressDRMInQuantityIncrease": false,
                            "timeIntervalForReminderNotificationsPostExpiration": [
                                "7",
                                "15",
                                "30",
                                "90"
                            ],
                            "autoRenewalDateBasis": "PurchaseDate",
                            "timeIntervalForUpgradeReminderNotificationsPreExpiration": [
                                "97",
                                "37",
                                "22",
                                "14"
                            ],
                            "isFreeTrial": true,
                            "combinedRenewalPeriod": 1,
                            "timeIntervalForCCExpirationReminderNotifications": [
                                "30",
                                "15",
                                "7"
                            ],
                            "duration": "TWO_MONTH",
                            "timeIntervalForManualReminderNotifications": [
                                "90",
                                "30",
                                "15",
                                "7"
                            ],
                            "isDistinctScheduleTurnedOn": false,
                            "isCombinedRenewal": true,
                            "suppressDRMInRenewal": false,
                            "paymentSchedule": "matchRecurrence",
                            "isAutomatic": true,
                            "numOfDaysPriorExpirationForRenewalPreFirst": 30,
                            "isChangeProductAsRenewal": false,
                            "freeTrialPeriod": 45,
                            "includeRenewalProductInUpgradeList": true,
                            "numOfDaysPriorExpirationForRenewal": 4,
                            "suppressOFIInTrialConversion": true,
                            "numOfDaysPriorExpirationForRenewalFirst": 15,
                            "timeIntervalForUpgradeReminderNotificationsPostExpiration": [
                                "97",
                                "37",
                                "22",
                                "14"
                            ],
                            "postExpirationBillingAttemptIntervalInDays": 7,
                            "suppressOFIInRenewal": true,
                            "suppressDRMInTrialConversion": false,
                            "trialPostExpirationBillingAttemptIntervalInDays": 7,
                            "trialGracePeriod": "1_MONTH",
                            "timeIntervalForTrialManualReminderNotifications": [
                                "30",
                                "15",
                                "7",
                                "2"
                            ]
                        }
                    },
                    {
                        "groupId": "16",
                        "groupName": "Export Controls",
                        "attributes": {
                            "manufactureCountry": "US",
                            "eccn": "3A992"
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

{% tabs %}
{% tab title="cURL with DEPLOYED query parameter" %}
The following example gets deployed versions of a specified product with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request GET 
'https://api.digitalriver.com/v1/products/[productId}?version=DEPLOYED' \
--header 'Authorization: Basic <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{ERID}?version=DEPLOYED' \
--header 'Authorization: Basic <API_key>' \
--header 'header x-erid-as-pid=true' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The response displays the deployed version of the product.

{% code overflow="wrap" %}
```json
[
    {
        "productType": "INDIVIDUAL",
        "companyId": "acme",
        "siteIds": [
            "acme"
        ],
        "id": "51954990080",
        "state": "DEPLOYED",
        "locked": false,
        "version": 1,
        "deploymentRequiredChanges": {
            "fulfillmentTypes": [],
            "otherFulfillmentIntegration": {
                "fulfillerIds": []
            },
            "upgradeProducts": [],
            "downgradeProducts": []
        },
        "liveChanges": {
            "externalReferenceId": "external-reference-id-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
            "catalogs": [
                {
                    "catalogId": "4783669800",
                    "catalogName": "acme",
                    "categories": [],
                    "pricing": [
                        {
                            "type": "listPrice",
                            "priceListName": "acme",
                            "taxInclusive": false,
                            "prices": [
                                {
                                    "currency": "CAD",
                                    "locale": "en_CA"
                                },
                                {
                                    "currency": "CAD",
                                    "locale": "en_US"
                                },
                                {
                                    "currency": "USD",
                                    "locale": "en_US",
                                    "configuredPrice": 10.00
                                },
                                {
                                    "currency": "CAD",
                                    "locale": "fr_CA"
                                },
                                {
                                    "currency": "ARS"
                                },
                                {
                                    "currency": "AUD"
                                },
                                {
                                    "currency": "BRL"
                                },
                                {
                                    "currency": "CAD"
                                },
                                {
                                    "currency": "CHF"
                                },
                                {
                                    "currency": "CLP"
                                },
                                {
                                    "currency": "CNY"
                                },
                                {
                                    "currency": "COP"
                                },
                                {
                                    "currency": "CZK"
                                },
                                {
                                    "currency": "DKK"
                                },
                                {
                                    "currency": "EGP"
                                },
                                {
                                    "currency": "EUR"
                                },
                                {
                                    "currency": "GBP"
                                },
                                {
                                    "currency": "HKD"
                                },
                                {
                                    "currency": "HUF"
                                },
                                {
                                    "currency": "IDR"
                                },
                                {
                                    "currency": "ILS"
                                },
                                {
                                    "currency": "INR"
                                },
                                {
                                    "currency": "JPY"
                                },
                                {
                                    "currency": "KRW"
                                },
                                {
                                    "currency": "MXN"
                                },
                                {
                                    "currency": "MYR"
                                },
                                {
                                    "currency": "NOK"
                                },
                                {
                                    "currency": "NZD"
                                },
                                {
                                    "currency": "OMR"
                                },
                                {
                                    "currency": "PEN"
                                },
                                {
                                    "currency": "PLN"
                                },
                                {
                                    "currency": "RUB"
                                },
                                {
                                    "currency": "SEK"
                                },
                                {
                                    "currency": "SGD"
                                },
                                {
                                    "currency": "THB"
                                },
                                {
                                    "currency": "TRY"
                                },
                                {
                                    "currency": "TWD"
                                },
                                {
                                    "currency": "USD"
                                },
                                {
                                    "currency": "VEF"
                                },
                                {
                                    "currency": "ZAR"
                                }
                            ]
                        },
                        {
                            "type": "subscriptionRenewalPrice",
                            "priceListName": "Subscription Renewal Price list",
                            "taxInclusive": false,
                            "prices": [
                                {
                                    "currency": "ARS"
                                },
                                {
                                    "currency": "EUR"
                                },
                                {
                                    "currency": "GBP"
                                },
                                {
                                    "currency": "USD"
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
                        "groupId": "2",
                        "groupName": "Storefront Settings",
                        "attributes": {
                            "longDescription": "longDescription-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "nonSolr": true,
                            "keywords": "keywords-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "displayName": "demo-display-name-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "taxableUnspscCode": "43230000",
                            "confirmAddlInfo": "confirmAddlInfo-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "shortDescription": "shortDescription-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "isViewable": true,
                            "taxableProductCode": "4323.320_D",
                            "isOrderable": true,
                            "returnMethod": "LOD",
                            "emailAddlInfoText": "emailAddlInfoText-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "name": "demo-name-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "emailAddlInfo": "emailAddlInfo-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "minOrderQuantity": 0,
                            "privateStoreOnly": false,
                            "productReturnMethod": "ByAgentAndSelfService",
                            "sku": "demo-sku-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                            "maxOrderQuantity": 0
                        }
                    },
                    {
                        "groupId": "10",
                        "groupName": "Subscription",
                        "attributes": {
                            "freeExtension": "2_WEEK",
                            "timeIntervalForTrialReminderNotifications": [
                                "30",
                                "15",
                                "7",
                                "2"
                            ],
                            "gracePeriod": "1_WEEK",
                            "timeIntervalForUpgradeReminderNotificationsPostCreation": [
                                "7",
                                "15",
                                "30",
                                "90"
                            ],
                            "timeIntervalForReminderNotifications": [
                                "90",
                                "30",
                                "15",
                                "7"
                            ],
                            "suppressOFIInQuantityIncrease": false,
                            "suppressDRMInUpgradeDowngrade": false,
                            "suppressOFIInUpgradeDowngrade": false,
                            "suppressDRMInQuantityIncrease": false,
                            "timeIntervalForReminderNotificationsPostExpiration": [
                                "7",
                                "15",
                                "30",
                                "90"
                            ],
                            "autoRenewalDateBasis": "PurchaseDate",
                            "timeIntervalForUpgradeReminderNotificationsPreExpiration": [
                                "97",
                                "37",
                                "22",
                                "14"
                            ],
                            "isFreeTrial": true,
                            "combinedRenewalPeriod": 1,
                            "timeIntervalForCCExpirationReminderNotifications": [
                                "30",
                                "15",
                                "7"
                            ],
                            "duration": "TWO_MONTH",
                            "timeIntervalForManualReminderNotifications": [
                                "90",
                                "30",
                                "15",
                                "7"
                            ],
                            "isDistinctScheduleTurnedOn": false,
                            "isCombinedRenewal": true,
                            "suppressDRMInRenewal": false,
                            "paymentSchedule": "matchRecurrence",
                            "isAutomatic": true,
                            "numOfDaysPriorExpirationForRenewalPreFirst": 30,
                            "isChangeProductAsRenewal": false,
                            "freeTrialPeriod": 45,
                            "includeRenewalProductInUpgradeList": true,
                            "numOfDaysPriorExpirationForRenewal": 4,
                            "suppressOFIInTrialConversion": true,
                            "numOfDaysPriorExpirationForRenewalFirst": 15,
                            "timeIntervalForUpgradeReminderNotificationsPostExpiration": [
                                "97",
                                "37",
                                "22",
                                "14"
                            ],
                            "postExpirationBillingAttemptIntervalInDays": 7,
                            "suppressOFIInRenewal": true,
                            "suppressDRMInTrialConversion": false,
                            "trialPostExpirationBillingAttemptIntervalInDays": 7,
                            "trialGracePeriod": "1_MONTH",
                            "timeIntervalForTrialManualReminderNotifications": [
                                "30",
                                "15",
                                "7",
                                "2"
                            ]
                        }
                    },
                    {
                        "groupId": "16",
                        "groupName": "Export Controls",
                        "attributes": {
                            "manufactureCountry": "US",
                            "eccn": "3A992"
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
