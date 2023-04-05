---
description: >-
  Learn how to create or update a product programmatically using product
  identifiers (productId).
---

# Creating or updating a product

{% hint style="danger" %}
Do not send multiple simultaneous requests to create or update a product via API and Global Commerce or Bulk Product Upload (BPU). Simultaneous changes to a product can lead to errors in the database.
{% endhint %}

When managing a product or a product's locale, note that:

* You can [create a base product with variations](adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product) by adding the `variations` object to the payload. When you [create a product without the `variations` object](creating-or-updating-a-product.md#creating-an-individual-or-base-product), it is an individual product. You cannot transfer an individual product to a base product programmatically. However, you can [transfer an individual product to a base product](https://help.digitalriver.com/help/gc/Products/All-Products/Editing-a-product.htm#AddingRemovingVariations) from [Global Commerce](https://acrobat.adobe.com/link/review?uri=urn:aaid:scds:US:76a71070-bb8d-3782-8d8a-c8c4173352bf).
* The request automatically adds the `locales` object from the base product to each product variation. An error appears in the response if the locales are not consistent between the base product and the product variations.
  * If `en_GB` and `en_US` exist in the base product and only `en_US` exists in the product variation, the request copies `en_GB` to the product variation.
  * If `en_GB` and `en_US` exist in the base product and `ja_JP` exists in the product variation, the response returns an error.
* The request updates the correct attribute value even if the attribute value is in the wrong group. For example, if you put the `eccn` attribute for export control in the storefront setting group, the request will update the `eccn` attribute as long as the value is correct. However, the response will put the attribute in the export control group where it belongs.

## Product payload example

When creating a product, you need to provide the following objects in the payload:

* [`deploymentRequiredChanges`](creating-or-updating-a-product.md#deploymentrequiredchanges): This object is required for [base ](../../../general-resources/admin-apis-reference/products.md#base-product)or [individual products](../../../general-resources/admin-apis-reference/products.md#individual-product).
* [`liveChanges`](creating-or-updating-a-product.md#livechanges): This object is required for [base ](../../../general-resources/admin-apis-reference/products.md#base-product)or [individual products](../../../general-resources/admin-apis-reference/products.md#individual-product).
* [`localization`](creating-or-updating-a-product.md#localizations): This object is required for [base ](../../../general-resources/admin-apis-reference/products.md#base-product)or [individual products](../../../general-resources/admin-apis-reference/products.md#individual-product).
* [`variations`](creating-or-updating-a-product.md#variations): This object is only required for a [base product](../../../general-resources/admin-apis-reference/products.md#base-product) with [product variations](../../../general-resources/admin-apis-reference/products.md#product-variations).

The following payload example contains data attributes for a base product with variations.

{% tabs %}
{% tab title="Base product payload example" %}
The following payload example contains data attributes for a base product with variations. See the [products ](../../../general-resources/admin-apis-reference/products.md#products-resource)resource for a description of the attributes.

{% code overflow="wrap" %}
```json
{
  "deploymentRequiredChanges": {
    "fulfillmentTypes": [
      "Download"
    ],
    "otherFulfillmentIntegration": {
      "fulfillerIds": [
        "digitalRiver"
      ]
    },
    "transferProduct": "2234567800",
    "upgradeProducts": [
      "3234567800"
    ],
    "downgradeProducts": [
      "4234567800"
    ]
  },
  "liveChanges": {
    "externalReferenceId": "sku-1234-5678-xyz",
    "catalogs": [
      {
        "catalogId": "123456000",
        "categories": [
          {
            "categoryId": "19000000"
          }
        ],
        "prices": [
          {
            "type": "listPrice",
            "prices": [
              {
                "currency": "USD",
                "locale": "en_US",
                "configuredPrice": 15.99
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
          "attributes": {
            "property1": "string",
            "property2": "string"
          }
        }
      ]
    }
  ],
  "variations": [
    {
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
        "transferProduct": "2234567800",
        "upgradeProducts": [
          "3234567800"
        ],
        "downgradeProducts": [
          "4234567800"
        ]
      },
      "liveChanges": {
        "externalReferenceId": "sku-1234-5678-xyz",
        "catalogs": [
          {
            "catalogId": "123456000",
            "categories": [
              {
                "categoryId": "19000000"
              }
            ],
            "prices": [
              {
                "type": "listPrice",
                "prices": [
                  {}
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
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Creating an individual or base product

You can create the base product and all of its product variations using one call. When doing so, the request copies the base product attributes to each product variation. You can update the attributes for a product variation by including the modified attributes in the product variation request payload.

The following [`POST /v1/products`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products/post) request creates a [base product](../../../general-resources/admin-apis-reference/products.md#base-product) with [product variations](../../../general-resources/admin-apis-reference/products.md#product-variations).&#x20;

When creating an individual or base product, you do not need to provide a [`productId`](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md). The `productId` will be provided when you create the product. If you want to use an [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md), provide the ERID in the payload. [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) will associate the created product with the given ERID. After associating the ERID with the product, you can continue to use the ERID in the call request when [updating the product](creating-or-updating-a-product.md#updating-an-individual-or-base-product).

You can [create a base product with variations](adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product) by adding the `variations` object to the payload. When you [create a product without the `variations` object](creating-or-updating-a-product.md#creating-an-individual-or-base-product), it is an individual product.

{% hint style="info" %}
To add a locale to a product, [add the locale data](creating-or-updating-a-product.md#adding-or-updating-a-products-locale) in the payload using the [`POST /v1/products/{productid}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BproductId%7D/post) request.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
The following example creates a new base product with a `productId` and product variations using a `variationProductId`. See the [products ](../../../general-resources/admin-apis-reference/products.md#products-resource)resource for a description of the attributes.

{% code overflow="wrap" %}
```json
curl --location --request POST 'https://api.digitalriver.com/v1/products' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "liveChanges": {  },  
    "variations": [    
        {          
            "varyingAttributes": [        
                {          
                    "attributeName": "Color",          
                    "attributeValue": "Black"        
                },        
                {          
                    "attributeName": "fulfillmentType",          
                    "attributeValue": "Download"        
                }      
            ],      
            "liveChanges": {  }    
        },    
        {      
            "varyingAttributes": [        
                {          
                    "attributeName": "Color",          
                    "attributeValue": "Blue"        
                },        
                {          
                    "attributeName": "fulfillmentType",          
                    "attributeValue": "Download"        
                }      
            ],      
            "liveChanges": {  }    
        }  
    ] 
}'
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header. The following example creates a new base product with an `ERID` and product variations using an `variationERID`. See the [products ](../../../general-resources/admin-apis-reference/products.md#products-resource)resource for a description of the attributes.

```
curl --location --request POST 'https://api.digitalriver.com/v1/products/{ERID}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
--data-raw '{
    "productType": "BASE",  
    "companyId": "ace",  
    "liveChanges": 
        {  
            "externalReferenceId": "ERID_BASE"
        },  
    "variations": [    
        { 
            "productType": "VARIATION",      
            "companyId": "cast",      
            "varyingAttributes": [        
                {          
                    "attributeName": "Color",          
                    "attributeValue": "Black"        
                },        
                {          
                    "attributeName": "fulfillmentType",          
                    "attributeValue": "Download"        
                }      
            ],      
            "liveChanges": 
                { 
                    "externalReferenceId": "ERID_VARIATION_1"     
                }    
        },    
        {           
            "varyingAttributes": [        
                {          
                    "attributeName": "Color",          
                    "attributeValue": "Blue"        
                },        
                {          
                    "attributeName": "fulfillmentType",          
                    "attributeValue": "Download"        
                }      
            ],      
            "liveChanges":   
                { 
                    "externalReferenceId": "ERID_VARIATION_2"     
                }   
        }  
    ] 
}'
```
{% endtab %}

{% tab title="202 Accepted response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

{% code overflow="wrap" %}
```json
{    
    "taskId": "7aec3f23-3c12-479c-9d1f-4e34d498234b",    
    "requestType": "CREATE_PRODUCT",    
    "taskStatus": "PUBLISHED", 202 Accepted response"receivedTime": "2022-08-11T16:32:26.547Z" 
}
```
{% endcode %}

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/getting-the-latest-information-on-a-product-task.md).  You can also verify the successful completion of the task by [checking the product history](creating-or-updating-a-product.md#product-history-attributes) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Note that there may be a delay before these changes appear in Global Commerce.&#x20;
{% endtab %}
{% endtabs %}

### Creating a digital product

{% tabs %}
{% tab title="cURL" %}
The following example creates a digital product. See the [products ](../../../general-resources/admin-apis-reference/products.md#products-resource)resource for a description of the attributes.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "companyId":"acme",
    "deploymentRequiredChanges": {
        "fulfillmentTypes": ["Download"]
    },
    "liveChanges": {
        "externalReferenceId": "external-reference-id-{{uuid}}",
        "catalogs" : [ {
            "catalogId" : "4783669800",
            "pricing" : [ {
                "type": "listPrice",
                "prices": [{
                    "currency": "USD",
                    "locale": "en_US",
                    "configuredPrice": 10
                }]
            }]
        }]
        
    },
    "localizations": [
    {
      "locale": "en_US",
      "isDefault": "true",
      "groups": [
        {
          "groupId": "11",
          "groupName": "Software",
          "attributes": {
            "name": "demo-name-{{uuid}}",
            "displayName": "demo-display-name-{{uuid}}",
            "sku": "demo-sku-{{uuid}}",
            "returnMethod": "LOD",
            "productReturnMethod": "ByAgentAndSelfService",
            "taxableUnspscCode": "43230000",
            "taxableProductCode": "4323.320_D",
            "privateStoreOnly": false,
            "isViewable": true,
            "isOrderable": true,
            "nonSolr": true,
            "shortDescription": "shortDescription-{{uuid}}",
            "longDescription": "longDescription-{{uuid}}",
            "keywords": "keywords-{{uuid}}",
            "emailAddlInfoText": "emailAddlInfoText-{{uuid}}",
            "emailAddlInfo": "emailAddlInfo-{{uuid}}",
            "confirmAddlInfo": "confirmAddlInfo-{{uuid}}",
            "eccn": "3A992",
            "manufactureCountry": "US"
          }
        },
        {
          "groupId": "5678",
          "groupName": "subscription",
          "attributes": {
            "autoRenewalDateBasis": "PurchaseDate",
            "combinedRenewalPeriod": 1,
            "duration": "TWO_MONTH",
            "freeExtension": "2_WEEK",
            "freeTrialPeriod": 45,
            "gracePeriod": "1_WEEK",
            "includeRenewalProductInUpgradeList": true,
            "isAutomatic": true,
            "isChangeProductAsRenewal": false,
            "isCombinedRenewal": true,
            "isDistinctScheduleTurnedOn": false,
            "isFreeTrial": true,
            "numOfDaysPriorExpirationForRenewal": 4,
            "numOfDaysPriorExpirationForRenewalFirst": 15,
            "numOfDaysPriorExpirationForRenewalPreFirst": 30,
            "paymentSchedule": "matchRecurrence",
            "postExpirationBillingAttemptIntervalInDays": 7,
            "suppressDRMInQuantityIncrease": false,
            "suppressDRMInRenewal": false,
            "suppressDRMInTrialConversion": false,
            "suppressDRMInUpgradeDowngrade": false,
            "suppressOFIInQuantityIncrease": false,
            "suppressOFIInRenewal": true,
            "suppressOFIInTrialConversion": true,
            "suppressOFIInUpgradeDowngrade": false,
            "timeIntervalForCCExpirationReminderNotifications": ["30","15","7"],
            "timeIntervalForManualReminderNotifications": ["90","30","15","7"],
            "timeIntervalForReminderNotifications": ["90","30","15","7"],
            "timeIntervalForReminderNotificationsPostExpiration": ["7","15","30","90"],
            "timeIntervalForTrialManualReminderNotifications": ["30","15","7","2"],
            "timeIntervalForTrialReminderNotifications": ["30","15","7","2"],
            "timeIntervalForUpgradeReminderNotificationsPostCreation": ["7","15","30","90"],
            "timeIntervalForUpgradeReminderNotificationsPostExpiration": ["97","37","22","14"],
            "timeIntervalForUpgradeReminderNotificationsPreExpiration": ["97","37","22","14"],
            "trialGracePeriod": "1_MONTH",
            "trialPostExpirationBillingAttemptIntervalInDays": 7
          }
        }
      ]
    }
  ]
}'
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

{% code overflow="wrap" %}
```json
{
    "taskId": "f906e297-2275-4411-80d4-99b84c80ec69",
    "requestType": "CREATE_PRODUCT",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-11-28T13:43:59.692Z"
}
```
{% endcode %}

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/getting-the-latest-information-on-a-product-task.md).  You can also verify the successful completion of the task by [checking the product history](creating-or-updating-a-product.md#product-history-attributes) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Note that there may be a delay before these chances appear in Global Commerce.&#x20;
{% endtab %}
{% endtabs %}

### Product history attributes

* **To Date**: The beginning of the search date range.
* **From Date**: The end of the search date range.
* **Change Type**: A brief description of the change applied to the product. Some of the possible change type values are as follows:&#x20;
  * **Copied**: This indicates a user copied the current product from another product. When a user copies an existing product, the Product History page shows the product ID and the name of the original product on which the new product is based.&#x20;
  * **Revert**: This indicates a user reverted the product to a previous version (and indicates the previous version). For more about reverting a product, see [Reverting changes to products](creating-or-updating-a-product.md#reverting-changes-to-products).&#x20;
  * **Save or Save (Including Live Change)**: This indicates you or another user saved a change to the product. Save indicates you must deploy the product before shoppers can see the change in your store. Save (Live Change) indicates the system automatically applied the change to your store, and you do not need to deploy the product. \
    \
    You can click the plus (**+**) sign next to a save event to see additional information for that event. One or more of the following columns appear with every save event:&#x20;
    * **Locale**: Indicates the locales where the change occurred.&#x20;
    * **Area**: Indicates the general area in the editor the change occurred. \
      \
      **Example**: If you change the name, the area lists "Storefront Settings" as the area where you can find the name. &#x20;
    * **Field**: Displays the changed field. \
      \
      **Example**: You can use this field name and the content displayed in the Area column to locate the attribute in Global Commerce.&#x20;
    * **Old Value**: Displays the old value. If a value is not present, no content appears in this column.&#x20;
    * **New Value**: Displays the new value. \
      \
      **Note**: Save does not always mean the item changed. If you view the item and click the **Save** button without applying any changes, the system logs that change.&#x20;
  * **Status Changed to Deployed**: Indicates the state of the product changed to the Live state. The changes now appear in your store.&#x20;
  * **Status Changed to Design**: Indicates the status of the product changed to the Design state.
  * **Status Changed to New**: Indicates the status of the product changed to the New state when you create a product.&#x20;
  * **Took Ownership**: Indicates that the right to edit a product belongs to a new user. The name of the new user appears in the Modified By column. Ownership indicates the last person to edit the product. Another user cannot edit the product until they take ownership of the product. Ownership prevents two users from editing the product at the same time.&#x20;
  * **Variation Added**: A user added a variation to the product. The variation ID, as well as the varying attributes, also appear in the Change Type column.&#x20;
  * **Variation Deleted**: A user deleted product variation. The variation ID, as well as the varying attributes, also appear in the Change Type column.
* **Product/Variation ID**: Displays the product identifier or variation for the product.&#x20;
  * If this is an individual product, only the product ID appears. If this is a base product, (Base) appears after the ID.&#x20;
  * If this is a product variation, the name of the variation and the varying attributes (in parentheses) appears after the ID.
* **Modified By**: The name of the person or application who last modified the product. API indicates the Admin API. For example, `jdoe` or `API (ZDIOODJi***)`, where `jdoe` is the Global Commerce username and `ZDIOODJi***` is the first 8 digits of the API key for an Admin API request.
* **Modified On**: The date and time when the product was last modified.

## Adding or replacing a product's locale

You can localize your products so shoppers can see product information in their native language, date format, time format, and currency. You can also localize themes and styles to create a look and feel for a specific locale or region.&#x20;

A locale is a designator that combines the two-letter [ISO 639-1](https://en.wikipedia.org/wiki/ISO\_639-1) language code with the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code (such as `en_US`). For example, the `en_GB` language code represents the English language and the country of Great Britain.&#x20;

When you create or update a product, you can configure the product to use those locales and enter localized content for that product. When choosing locales, note the following:&#x20;

* When you enter text for the product in the default locale, the same text appears for all supported locales until you either "override" or "specify" the default in a specific locale folder. You can override the default locales by adding a product variation after creating a base product. Or you can specify the default locales when you create a base product and its product variations at the same time. Changing the default locale for the product does not affect the global default locale settings in your store.&#x20;
* You can provide localized content for a product. A `localizations` object appears for each supported locale where you can enter the localized information. You do not have to enter localized content for all supported locales.&#x20;

{% tabs %}
{% tab title="Payload example" %}
The following example payload adds or replaces a product's locale. See the [products ](../../../general-resources/admin-apis-reference/products.md#products-resource)resource for a description of the attributes.

{% code overflow="wrap" %}
```json
{
  "localizations": [
    {
      "locale": "en_US",
      "isDefault": true,
      "groups": [
        {
          "attributes": {
            "property1": "string",
            "property2": "string"
          }
        }
      ]
    }
  ]
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

* By default, shoppers can purchase products in any locale (within any defined export controls). You should restrict the purchasing products to only supported locales. See [Limiting purchases to supported locales](https://help.digitalriver.com/internal-help/gc/Products/All-Products/About-localized-products.htm?Highlight=base%20product#Limit) for more information.&#x20;

Ideally, you should localize a product when you first create it. However, you can localize a product after you create and deploy it to your store. If the fields and options on a locale tab are disabled in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) the supported locale uses the default locale setting. See [Overriding the default locale](https://help.digitalriver.com/internal-help/gc/Products/All-Products/About-localized-products.htm?Highlight=base%20product#Override) for more information.

The following [`POST /v1/products/{productid}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1products\~1%7BproductId%7D/post) request updates an existing product by replacing attributes. You must provide either a [`productId`](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md). &#x20;

{% tabs %}
{% tab title="cURL" %}
The following example updates the locale for a product with a specified `productId`. You can also add or replace locales for a product variation in the payload. See the [products ](../../../general-resources/admin-apis-reference/products.md#products-resource)resource for a description of the attributes.

{% hint style="info" %}
You can replace the product's current locales by adding new locales in the payload. For example, if the current locale is `zh_TW` and you include `en_US`, `en_GB`, and `ja_JP` in the payload, the locales will change to `en_US`, `en_GB`, and `ja_JP`. Essentially when you update a product you are replacing the existing data with new data.\
&#x20;\
For example: If the current data is:\
\
`"prices": [{` \
&#x20;  `"currency": "USD",` \
&#x20;  `"configuredPrice": 10` \
`}]`\
\
And you replace it with:\
\
`"prices": []`\
\
The request replaces the current configures price with the data you provided. If you don't want to change specific data in a request, either do not include the data in the payload or include the data with the same values in the payload.
{% endhint %}

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{productId}' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "localizations": [    
        {      
            "locale": "en_US",      
            "isDefault": "true",      
            "groups": [        
                {          
                    "groupId": "ignored",          
                    "groupName": "ignored",          
                    "attributes": {            
                        "displayName": "display-name-{{defaultLocale}}-updated{{baseProductId}}"          
                    }        
                }      
            ]    
        }  
    ] 
}'
```
{% endcode %}

An `ERID` request requires the `x-erid-as-pid=true` header. Add new attributes and/or replace locale attributes in the payload. For example, you can add or replace locales for a product variation in the payload. See the [products ](../../../general-resources/admin-apis-reference/products.md#products-resource)resource for a description of the attributes.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{ERID}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
--data-raw '{
    "localizations": [    
        {      
            "locale": "en_US",      
            "isDefault": "true",      
            "groups": [        
                {          
                    "groupId": "ignored",          
                    "groupName": "ignored",          
                    "attributes": {            
                        "displayName": "display-name-{{defaultLocale}}-updated{{baseProductId}}"          
                    }        
                }      
            ]    
        }  
    ] 
}'
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

{% code overflow="wrap" %}
```json
{
    "taskId": "7aec3f23-3c12-479c-9d1f-4e34d498234b", 
    "requestType": "UPDATE_PRODUCT", 
    "taskStatus": "PUBLISHED", 
    "receivedTime": "2022-08-11T16:32:26.547Z"
}
```
{% endcode %}

Use the `taskId` in the response to verify the successful completion of the request.  You can also verify the successful completion of the task by [checking the product history](creating-or-updating-a-product.md#product-history-attributes) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Note that there may be a delay before these chances appear in Global Commerce.&#x20;
{% endtab %}
{% endtabs %}

## Updating an individual or base product

You can send a request to update any supported attribute, such as the [locale](creating-or-updating-a-product.md#adding-or-updating-a-products-locale), for a [base product](broken-reference) or [individual product](broken-reference). The change will be visible to the shopper when you deploy the updated product.&#x20;

The following [`POST /v1/products/{productId or ERID}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1products\~1%7BproductId%7D/post) request updates to the existing base product. When updating a specific individual or base product, you must provide either a [productId](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md).&#x20;

{% hint style="info" %}
Do not use this request to update a product variation. Adding a variations object to the payload for this request will return an error. See [Adding or updating a product variation](adding-or-updating-a-product-variation.md) for instructions on managing product variations.
{% endhint %}

{% tabs %}
{% tab title="productId cURL" %}
The following example adds or updates an individual or base product with a `productId`.  See the [products ](../../../general-resources/admin-apis-reference/products.md#products-resource)resource for a description of the attributes.&#x20;

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{productId}' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "localizations": [    
        {      
            "locale": "en_US",      
            "isDefault": "true",      
            "groups": [        
                {          
                    "groupId": "ignored",          
                    "groupName": "ignored",          
                    "attributes": {            
                        "displayName": "display-name-en_US-1234567890"          
                    }        
                }      
            ]    
        }  
    ] 
}'
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{ERID}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
--data-raw '{
    "localizations": [    
        {      
            "locale": "en_US",      
            "isDefault": "true",      
            "groups": [        
                {          
                    "groupId": "ignored",          
                    "groupName": "ignored",          
                    "attributes": {            
                        "displayName": "display-name-en_US-1234567890"          
                    }        
                }      
            ]    
        }  
    ] 
}'
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

{% code overflow="wrap" %}
```json
{    
    "taskId": "b3c006fd-b7b8-4d91-932c-ca6da7f71f1f",    
    "requestType": "UPDATE_PRODUCT",    
    "taskStatus": "PUBLISHED",    
    "receivedTime": "2022-08-23T20:17:19.827Z" 
}
```
{% endcode %}

Use the `taskId` in the response to verify the successful completion of the request.  You can also verify the successful completion of the task by [checking the product history](creating-or-updating-a-product.md#product-history-attributes) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Note that there may be a delay before these chances appear in Global Commerce.&#x20;
{% endtab %}
{% endtabs %}

## Viewing a product's history

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.&#x20;
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID in the **Search For** field, and then click **Search**.&#x20;
4. Click the link for the product under the **Internal Product Name** column. The Edit Product page appears.&#x20;
5. Click **View History**. The Product History window shows the product's history.

<figure><img src="../../../.gitbook/assets/Product History.jpg" alt=""><figcaption></figcaption></figure>

## Reverting changes to products

If you change a deployed product, the product's status changes to Design. If you decide you do not want those changes, you can revert the product to how it appeared when you last deployed the product.

{% hint style="warning" %}
Reverting a change removes any modifications applied to the product since you last deployed it.
{% endhint %}

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Deploy Products**. The Deploy Products page appears.
3. Select **Products** and click **All Products**. The Products page appears.
4. Click **View Products to Deploy**. The Deploy Products page appears.
5. Select the catalog and locale associated with the product changes you want to revert from the **Catalog** and **Locale** lists.
6. From the **Undeployed Changes** tab, select the changed products you want to revert. Or select all products by clicking the **Select All** check to the left of the **Deploy** button.
7. Click **Revert Changes**. A message appears informing you that reverted changes cannot be recovered.
8. Click **OK** to continue.
