---
description: Learn about individual products.
---

# Individual products

An individual product is a single sellable SKU. The following image shows an example of a SKU:

![](<../../../.gitbook/assets/individual\_product (1).png>)

Individual products are very common, but there are times when a product with variants makes more sense for the store, product line, or business.

{% hint style="info" %}
**Example**: If a product comes in different colors, sizes, or versions, it is easier and less time consuming to maintain one product with variants than to maintain a handful of individual products that are nearly the same.
{% endhint %}

You can get individual products, products within a category, or all possible products with API calls.

Get a product by an identifier with the GET request:

{% tabs %}
{% tab title="URI" %}
```http
GET shoppers/me/products/55555555?expand=all
```
{% endtab %}

{% tab title="Request Header" %}
```
Host: api.digitalriver.com
User-Agent: Apache-HttpClient/4.1.1 (java 1.5)
Accept: application/json
Authorization: bearer your_access_token
```
{% endtab %}

{% tab title="Payload" %}
```
The request body should be empty.
```
{% endtab %}

{% tab title="Response Body" %}
```javascript
{"product": {
   "uri": "https://api.digitalriver.com/v1/shoppers/me/products/55555555",
   "relation": "https://developers.digitalriver.com/v1/shoppers/ProductsResource",
   "parentProduct":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/88888888",
      "relation": "https://developers.digitalriver.com/v1/shoppers/ProductsResource"
   },
   "categories":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/55555555/categories",
      "relation": "https://developers.digitalriver.com/v1/shoppers/CategoriesResource"
   },
   "familyAttributes":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/55555555/family-attributes",
      "relation": "https://developers.digitalriver.com/v1/shoppers/ProductsResource"
   },
   "id": 55555555,
   "name": "Class I",
   "displayName": "Class I",
   "shortDescription": "Class I is the perfect GPS waypoint and route manager for the beginning or occasional GPS user.",
   "longDescription": "Class I is the fast and easy way to create, edit, and transfer waypoints and routes between your computer and your Garmin, Magellan, or Lowrance GPS. Using Class I, you can manage all of your waypoints and routes, and display them in lists sorted by name, elevation, or distance. Class I connects your GPS to the best mapping and information sites on the Internet, giving you one-click access to street and topo maps, aerial photos, weather forecasts, and nearby attractions.",
   "productType": "DOWNLOAD",
   "sku": "Class I",
   "externalReferenceId": null,
   "companyId": "demosft3",
   "displayableProduct": "true",
   "purchasable": "true",
   "manufacturerName": null,
   "manufacturerPartNumber": null,
   "minimumQuantity": null,
   "maximumQuantity": null,
   "thumbnailImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft3/images/product/thumbnail/classIThumb.jpg",
   "productImage": "https://drh-sys-ora.img.digitalriver.com/Storefront/Company/demosft3/images/product/detail/classIBox.jpg",
   "keywords": null,
   "baseProduct": "false",
   "customAttributes": {"attribute":    [
            {
         "name": "displayFinancePricing",
         "type": "Boolean",
         "value": "false"
      },
            {
         "name": "nonSolr",
         "type": "Boolean",
         "value": "false"
      },
            {
         "name": "numberOfDownloads",
         "type": "Integer",
         "value": "5"
      },
            {
         "name": "originalIsOrderable",
         "type": "Boolean",
         "value": "true"
      },
            {
         "name": "downloadDisplayed",
         "type": "Boolean",
         "value": "true"
      },
            {
         "name": "downloadDisplayName",
         "type": "String",
         "value": "WaterLilies.jpg"
      },
            {
         "name": "downloadDisplayNames",
         "type": "List",
         "value": "[]"
      },
            {
         "name": "applicationFile",
         "type": "String",
         "value": "WaterLilies.jpg"
      },
            {
         "name": "numberOfIPAddresses",
         "type": "Integer",
         "value": "10"
      },
            {
         "name": "timeFrame",
         "type": "Integer",
         "value": "30"
      },
            {
         "name": "points",
         "type": "Integer",
         "value": "1"
      },
            {
         "name": "financeLenderID",
         "type": "String",
         "value": "API1"
      },
            {
         "name": "fileSize",
         "type": "Integer",
         "value": "82"
      },
            {
         "name": "downloadType",
         "type": "String",
         "value": "HTTP"
      },
            {
         "name": "fileSizeValidatedDate",
         "type": "Date",
         "value": "Thu Sep 13 14:49:28 CDT 2007"
      },
            {
         "name": "fileOnBackupMedia",
         "type": "Boolean",
         "value": "true"
      },
            {
         "name": "originalIsViewable",
         "type": "Boolean",
         "value": "true"
      },
            {
         "name": "downloadAdapter",
         "type": "String",
         "value": "com.digitalriver.downloads.adapters.DRHDownloadAdapter"
      },
            {
         "name": "financeTermCode",
         "type": "String",
         "value": "FAFB0CC6D-EAA1-7E77-4675-1F8E040B2CFB"
      }
   ]},
   "financing":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/55555555/financing",
      "financingTerm": [      {
         "id": 50010080,
         "totalRepayable":          {
            "currency": "USD",
            "value": 7.6
         },
         "formattedTotalRepayable": "$7.60",
         "creditAmount":          {
            "currency": "USD",
            "value": 7.2
         },
         "formattedCreditAmount": "$7.20",
         "monthlyPaymentAmount":          {
            "currency": "USD",
            "value": 0.64
         },
         "formattedMonthlyPaymentAmount": "$0.64",
         "durationInMonths": 12,
         "interestRatePct": 0.099,
         "interestRatePctForDisplay": 9.9,
         "description": "9.9% for 12 months"
      }]
   },
   "pricing":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/55555555/pricing",
      "listPrice":       {
         "currency": "USD",
         "value": 8
      },
      "listPriceWithQuantity":       {
         "currency": "USD",
         "value": 8
      },
      "salePriceWithQuantity":       {
         "currency": "USD",
         "value": 7.2
      },
      "formattedListPrice": "$8.00",
      "formattedListPriceWithQuantity": "$8.00",
      "formattedSalePriceWithQuantity": "$7.20",
      "totalDiscountWithQuantity":       {
         "currency": "USD",
         "value": 0.8
      },
      "formattedTotalDiscountWithQuantity": "$0.80",
      "discountDescription": "10%",
      "tax": {"vatPercentage": 0},
      "feePricing":       {
         "salePriceWithFeesAndQuantity":          {
            "currency": "USD",
            "value": 7.2
         },
         "formattedSalePriceWithFeesAndQuantity": "$7.20"
      },
      "listPriceIncludesTax": "false",
      "msrpPrice": null,
      "formattedMsrpPrice": null,
      "volumePricing":       {
         "uri": "https://api.digitalriver.com/v1/shoppers/me/products/55555555/pricing/volume-pricing",
         "tier":          [
                        {
               "from": 1,
               "to": 5,
               "pricing":                {
                  "listPrice":                   {
                     "currency": "USD",
                     "value": 8
                  },
                  "listPriceWithQuantity":                   {
                     "currency": "USD",
                     "value": 8
                  },
                  "salePriceWithQuantity":                   {
                     "currency": "USD",
                     "value": 8
                  },
                  "formattedListPrice": "$8.00",
                  "formattedListPriceWithQuantity": "$8.00",
                  "formattedSalePriceWithQuantity": "$8.00",
                  "totalDiscountWithQuantity":                   {
                     "currency": "USD",
                     "value": 0
                  },
                  "formattedTotalDiscountWithQuantity": "$0.00",
                  "discountDescription": null,
                  "feePricing":                   {
                     "salePriceWithFeesAndQuantity":                      {
                        "currency": "USD",
                        "value": 8
                     },
                     "formattedSalePriceWithFeesAndQuantity": "$8.00"
                  },
                  "listPriceIncludesTax": "false",
                  "msrpPrice": null,
                  "formattedMsrpPrice": null
               }
            },
                        {
               "from": 6,
               "to": 10,
               "pricing":                {
                  "listPrice":                   {
                     "currency": "USD",
                     "value": 7
                  },
                  "listPriceWithQuantity":                   {
                     "currency": "USD",
                     "value": 7
                  },
                  "salePriceWithQuantity":                   {
                     "currency": "USD",
                     "value": 7
                  },
                  "formattedListPrice": "$7.00",
                  "formattedListPriceWithQuantity": "$7.00",
                  "formattedSalePriceWithQuantity": "$7.00",
                  "totalDiscountWithQuantity":                   {
                     "currency": "USD",
                     "value": 0
                  },
                  "formattedTotalDiscountWithQuantity": "$0.00",
                  "discountDescription": null,
                  "feePricing":                   {
                     "salePriceWithFeesAndQuantity":                      {
                        "currency": "USD",
                        "value": 7
                     },
                     "formattedSalePriceWithFeesAndQuantity": "$7.00"
                  },
                  "listPriceIncludesTax": "false",
                  "msrpPrice": null,
                  "formattedMsrpPrice": null
               }
            },
                        {
               "from": 11,
               "to": 15,
               "pricing":                {
                  "listPrice":                   {
                     "currency": "USD",
                     "value": 6
                  },
                  "listPriceWithQuantity":                   {
                     "currency": "USD",
                     "value": 6
                  },
                  "salePriceWithQuantity":                   {
                     "currency": "USD",
                     "value": 6
                  },
                  "formattedListPrice": "$6.00",
                  "formattedListPriceWithQuantity": "$6.00",
                  "formattedSalePriceWithQuantity": "$6.00",
                  "totalDiscountWithQuantity":                   {
                     "currency": "USD",
                     "value": 0
                  },
                  "formattedTotalDiscountWithQuantity": "$0.00",
                  "discountDescription": null,
                  "feePricing":                   {
                     "salePriceWithFeesAndQuantity":                      {
                        "currency": "USD",
                        "value": 6
                     },
                     "formattedSalePriceWithFeesAndQuantity": "$6.00"
                  },
                  "listPriceIncludesTax": "false",
                  "msrpPrice": null,
                  "formattedMsrpPrice": null
               }
            },
                        {
               "from": 16,
               "to": null,
               "pricing":                {
                  "listPrice":                   {
                     "currency": "USD",
                     "value": 5
                  },
                  "listPriceWithQuantity":                   {
                     "currency": "USD",
                     "value": 5
                  },
                  "salePriceWithQuantity":                   {
                     "currency": "USD",
                     "value": 5
                  },
                  "formattedListPrice": "$5.00",
                  "formattedListPriceWithQuantity": "$5.00",
                  "formattedSalePriceWithQuantity": "$5.00",
                  "totalDiscountWithQuantity":                   {
                     "currency": "USD",
                     "value": 0
                  },
                  "formattedTotalDiscountWithQuantity": "$0.00",
                  "discountDescription": null,
                  "feePricing":                   {
                     "salePriceWithFeesAndQuantity":                      {
                        "currency": "USD",
                        "value": 5
                     },
                     "formattedSalePriceWithFeesAndQuantity": "$5.00"
                  },
                  "listPriceIncludesTax": "false",
                  "msrpPrice": null,
                  "formattedMsrpPrice": null
               }
            }
         ],
         "formattedSalesPriceRange": "$5.00-$8.00"
      }
   },
   "inventoryStatus":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/55555555/inventory-status",
      "relation": "https://developers.digitalriver.com/v1/shoppers/InventoryStatusResource",
      "availableQuantity": 2147483647,
      "availableQuantityIsEstimated": "false",
      "productIsInStock": "true",
      "productIsAllowsBackorders": "true",
      "productIsTracked": "false",
      "requestedQuantityAvailable": "true",
      "status": "PRODUCT_INVENTORY_IN_STOCK",
      "statusIsEstimated": "false",
      "expectedInStockDate": null,
      "customStockMessage": null
   },
   "addProductToCart":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?productId=55555555",
      "relation": "https://developers.digitalriver.com/v1/shoppers/LineItemsResource",
      "cartUri": "https://api.digitalriver.com/v1/shoppers/me/carts/active?productId=55555555"
   }
}}
```
{% endtab %}
{% endtabs %}
