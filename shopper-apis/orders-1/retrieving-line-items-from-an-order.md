---
description: Learn how to retrieve line items from an order.
---

# Retrieving line items from an order

You can retrieve all line items or specific line items from an order using the [Orders ](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Orders)resource.

## Retrieving all line items from an order

To retrieve all line items, use the [`GET /shoppers/me/orders/{orderId}/line-items`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1{orderId}\~1line-items/get) resource.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/line-items' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{"lineItem": {
   "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/line-items/1111111111",
   "id": 1111111111,
   "quantity": 1,
   "product":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/product_ID",
      "id": product_ID,
      "name": "Class III",
      "displayName": "Class III",
      "shortDescription": "Class III adds the ability to export waypoints, routes, and tracks from your GPS device. With Class II, all GPS data is converted to .shp, .shx, and .dbf files for further use in a GIS environment.",
      "longDescription": "Class III adds the ability to transfer waypoints, routes, and tracks between GPS devices. With Class II, all GPS data can be saved as .shp, .shx, and .dbf files for further use in a GIS environment. In addition, Class III can import shapefiles and convert attributes from the .dbf file into waypoint names and comments. Shapefile import currently supports geometric projection (lat/lon) only.",
      "productType": "DOWNLOAD",
      "sku": "Class III",
      "externalReferenceId": "GPS-XFSD",
      "companyId": "demosft1",
      "displayableProduct": "true",
      "purchasable": "true",
      "manufacturerName": null,
      "manufacturerPartNumber": null,
      "thumbnailImage": "https://domain_ID.digitalriver.com/path/images/product/thumbnail/classIIIThumb_v2.jpg",
      "productImage": "https://domain_ID.digitalriver.com/path/images/product/detail/classIIIBox_v2.jpg",
      "keywords": null,
      "customAttributes": {"attribute":       [
                  {
            "name": "applicationFiles",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "numberOfDownloads",
            "type": "Integer",
            "value": "5"
         },
                  {
            "name": "gameRating",
            "type": "String",
            "value": "Adults Only"
         },
                  {
            "name": "downloadDisplayName",
            "type": "String",
            "value": "WaterLilies.jpg"
         },
                  {
            "name": "eula",
            "type": "String",
            "value": "Adipiscing, dolore amet magna feugait eum ea, nisl, wisi suscipit lobortis zzril, quis nulla et blandit. Diam dignissim, ex vulputate ullamcorper dolore qui, in, ut. Sit accumsan minim, nulla suscipit magna wisi eros volutpat, vulputate vero eum elit iriure. Ex, iusto duis dolore, ea praesent et vulputate vel ut molestie, lorem tincidunt augue consequat duis vel nulla nostrud exerci, blandit enim duis vero tation in. Facilisis eu in esse molestie nostrud consectetuer suscipit duis at wisi illum nostrud tincidunt vero nulla dolore."
         },
                  {
            "name": "downloadDisplayNames",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "fileSizes",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "platform",
            "type": "String",
            "value": "1 User License"
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
            "name": "systemRequirements",
            "type": "String",
            "value": "Exerci ad nisl commodo esse facilisis consequat in vel laoreet vel tation praesent molestie zzril, ut. At accumsan, ex autem illum volutpat eu veniam enim eu eu, nisl augue suscipit dolore aliquam iusto. Et te dolor ut ad magna tation quis at at augue dolore, aliquip lorem wisi, hendrerit praesent facilisi consectetuer commodo nostrud ut blandit odio et. Eum qui velit odio lobortis vel autem ad consequat lorem praesent facilisis dolore et eros, aliquip aliquip, velit, vel, praesent, ex. Vel, dolor nostrud eu vel delenit et eu qui et commodo dolore consequat ut augue duis."
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
            "name": "downloadAdapter",
            "type": "String",
            "value": "com.digitalriver.downloads.adapters.DRHDownloadAdapter"
         }
      ]}
   },
   "lineItemState": "Complete",
   "lineItemStateDetails":    {
      "description": "Downloadable - 1,Pending Refund - 1",
      "backOrdered": 0,
      "shipped": 0,
      "returned": 0,
      "pendingReturn": 1
   },
   "pricing":    {
      "listPrice":       {
         "currency": "USD",
         "value": 39.99
      },
      "listPriceWithQuantity":       {
         "currency": "USD",
         "value": 39.99
      },
      "salePriceWithQuantity":       {
         "currency": "USD",
         "value": 39.99
      },
      "formattedListPrice": "$39.99",
      "formattedListPriceWithQuantity": "$39.99",
      "formattedSalePriceWithQuantity": "$39.99"
   },
   "downloads": {"downloadUri": ["http://domain_ID.digitalriver.com/path/WaterLilies.jpg"]},
   "digitalRights": {"serialNumber": serial_number}
}}</span>

{"lineItem": {
   "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/line-items/1111111111",
   "id": 1111111111,
   "quantity": 1,
   "product":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/product_ID",
      "id": product_ID,
      "name": "Class III",
      "displayName": "Class III",
      "shortDescription": "Class III adds the ability to export waypoints, routes, and tracks from your GPS device. With Class II, all GPS data is converted to .shp, .shx, and .dbf files for further use in a GIS environment.",
      "longDescription": "Class III adds the ability to transfer waypoints, routes, and tracks between GPS devices. With Class II, all GPS data can be saved as .shp, .shx, and .dbf files for further use in a GIS environment. In addition, Class III can import shapefiles and convert attributes from the .dbf file into waypoint names and comments. Shapefile import currently supports geometric projection (lat/lon) only.",
      "productType": "DOWNLOAD",
      "sku": "Class III",
      "externalReferenceId": "GPS-XFSD",
      "companyId": "demosft1",
      "displayableProduct": "true",
      "purchasable": "true",
      "manufacturerName": null,
      "manufacturerPartNumber": null,
      "thumbnailImage": "https://domain_ID.digitalriver.com/path/images/product/thumbnail/classIIIThumb_v2.jpg",
      "productImage": "https://domain_ID.digitalriver.com/path/images/product/detail/classIIIBox_v2.jpg",
      "keywords": null,
      "customAttributes": {"attribute":       [
                  {
            "name": "applicationFiles",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "numberOfDownloads",
            "type": "Integer",
            "value": "5"
         },
                  {
            "name": "gameRating",
            "type": "String",
            "value": "Adults Only"
         },
                  {
            "name": "downloadDisplayName",
            "type": "String",
            "value": "WaterLilies.jpg"
         },
                  {
            "name": "eula",
            "type": "String",
            "value": "Adipiscing, dolore amet magna feugait eum ea, nisl, wisi suscipit lobortis zzril, quis nulla et blandit. Diam dignissim, ex vulputate ullamcorper dolore qui, in, ut. Sit accumsan minim, nulla suscipit magna wisi eros volutpat, vulputate vero eum elit iriure. Ex, iusto duis dolore, ea praesent et vulputate vel ut molestie, lorem tincidunt augue consequat duis vel nulla nostrud exerci, blandit enim duis vero tation in. Facilisis eu in esse molestie nostrud consectetuer suscipit duis at wisi illum nostrud tincidunt vero nulla dolore."
         },
                  {
            "name": "downloadDisplayNames",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "fileSizes",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "platform",
            "type": "String",
            "value": "1 User License"
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
            "name": "systemRequirements",
            "type": "String",
            "value": "Exerci ad nisl commodo esse facilisis consequat in vel laoreet vel tation praesent molestie zzril, ut. At accumsan, ex autem illum volutpat eu veniam enim eu eu, nisl augue suscipit dolore aliquam iusto. Et te dolor ut ad magna tation quis at at augue dolore, aliquip lorem wisi, hendrerit praesent facilisi consectetuer commodo nostrud ut blandit odio et. Eum qui velit odio lobortis vel autem ad consequat lorem praesent facilisis dolore et eros, aliquip aliquip, velit, vel, praesent, ex. Vel, dolor nostrud eu vel delenit et eu qui et commodo dolore consequat ut augue duis."
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
            "name": "downloadAdapter",
            "type": "String",
            "value": "com.digitalriver.downloads.adapters.DRHDownloadAdapter"
         }
      ]}
   },
   "lineItemState": "Complete",
   "lineItemStateDetails":    {
      "description": "Downloadable - 1,Pending Refund - 1",
      "backOrdered": 0,
      "shipped": 0,
      "returned": 0,
      "pendingReturn": 1
   },
   "pricing":    {
      "listPrice":       {
         "currency": "USD",
         "value": 39.99
      },
      "listPriceWithQuantity":       {
         "currency": "USD",
         "value": 39.99
      },
      "salePriceWithQuantity":       {
         "currency": "USD",
         "value": 39.99
      },
      "formattedListPrice": "$39.99",
      "formattedListPriceWithQuantity": "$39.99",
      "formattedSalePriceWithQuantity": "$39.99"
   },
   "downloads": {"downloadUri": ["http://domain_ID.digitalriver.com/path/WaterLilies.jpg"]},
   "digitalRights": {"serialNumber": serial_number}
}}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Retrieving a line item from an order

To retrieve a specific line item, use the [`GET /shoppers/me/orders/{orderId}/line-items/{lineItemId}`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Line-Items/paths/\~1v1\~1shoppers\~1me\~1orders\~1{orderId}\~1line-items\~1{lineItemId}/get) resource. The second URI path parameter (`lineItemId`) specifies the line-item ID.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/line-items/1111111111?expand=all' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{"lineItem": {
   "uri": "https://api.digitalriver.com/v1/shoppers/me/orders/9999999999/line-items/1111111111",
   "id": 1111111111,
   "quantity": 1,
   "product":    {
      "uri": "https://api.digitalriver.com/v1/shoppers/me/products/product_ID",
      "id": product_ID,
      "name": "Class III",
      "displayName": "Class III",
      "shortDescription": "Class III adds the ability to export waypoints, routes, and tracks from your GPS device. With Class II, all GPS data is converted to .shp, .shx, and .dbf files for further use in a GIS environment.",
      "longDescription": "Class III adds the ability to transfer waypoints, routes, and tracks between GPS devices. With Class II, all GPS data can be saved as .shp, .shx, and .dbf files for further use in a GIS environment. In addition, Class III can import shapefiles and convert attributes from the .dbf file into waypoint names and comments. Shapefile import currently supports geometric projection (lat/lon) only.",
      "productType": "DOWNLOAD",
      "sku": "Class III",
      "externalReferenceId": "GPS-XFSD",
      "companyId": "demosft1",
      "displayableProduct": "true",
      "purchasable": "true",
      "manufacturerName": null,
      "manufacturerPartNumber": null,
      "thumbnailImage": "https://domain_ID.digitalriver.com/path/images/product/thumbnail/classIIIThumb_v2.jpg",
      "productImage": "https://domain_ID.digitalriver.com/path/images/product/detail/classIIIBox_v2.jpg",
      "keywords": null,
      "customAttributes": {"attribute":       [
                  {
            "name": "applicationFiles",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "numberOfDownloads",
            "type": "Integer",
            "value": "5"
         },
                  {
            "name": "gameRating",
            "type": "String",
            "value": "Adults Only"
         },
                  {
            "name": "downloadDisplayName",
            "type": "String",
            "value": "WaterLilies.jpg"
         },
                  {
            "name": "eula",
            "type": "String",
            "value": "Adipiscing, dolore amet magna feugait eum ea, nisl, wisi suscipit lobortis zzril, quis nulla et blandit. Diam dignissim, ex vulputate ullamcorper dolore qui, in, ut. Sit accumsan minim, nulla suscipit magna wisi eros volutpat, vulputate vero eum elit iriure. Ex, iusto duis dolore, ea praesent et vulputate vel ut molestie, lorem tincidunt augue consequat duis vel nulla nostrud exerci, blandit enim duis vero tation in. Facilisis eu in esse molestie nostrud consectetuer suscipit duis at wisi illum nostrud tincidunt vero nulla dolore."
         },
                  {
            "name": "downloadDisplayNames",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "fileSizes",
            "type": "List",
            "value": "[]"
         },
                  {
            "name": "platform",
            "type": "String",
            "value": "1 User License"
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
            "name": "systemRequirements",
            "type": "String",
            "value": "Exerci ad nisl commodo esse facilisis consequat in vel laoreet vel tation praesent molestie zzril, ut. At accumsan, ex autem illum volutpat eu veniam enim eu eu, nisl augue suscipit dolore aliquam iusto. Et te dolor ut ad magna tation quis at at augue dolore, aliquip lorem wisi, hendrerit praesent facilisi consectetuer commodo nostrud ut blandit odio et. Eum qui velit odio lobortis vel autem ad consequat lorem praesent facilisis dolore et eros, aliquip aliquip, velit, vel, praesent, ex. Vel, dolor nostrud eu vel delenit et eu qui et commodo dolore consequat ut augue duis."
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
            "name": "downloadAdapter",
            "type": "String",
            "value": "com.digitalriver.downloads.adapters.DRHDownloadAdapter"
         }
      ]}
   },
   "lineItemState": "Complete",
   "lineItemStateDetails":    {
      "description": "Downloadable - 1,Pending Refund - 1",
      "backOrdered": 0,
      "shipped": 0,
      "returned": 0,
      "pendingReturn": 1
   },
   "pricing":    {
      "listPrice":       {
         "currency": "USD",
         "value": 39.99
      },
      "listPriceWithQuantity":       {
         "currency": "USD",
         "value": 39.99
      },
      "salePriceWithQuantity":       {
         "currency": "USD",
         "value": 39.99
      },
      "formattedListPrice": "$39.99",
      "formattedListPriceWithQuantity": "$39.99",
      "formattedSalePriceWithQuantity": "$39.99"
   },
   "downloads": {"downloadUri": ["http://domain_ID.digitalriver.com/path/WaterLilies.jpg"]},
   "digitalRights": {"serialNumber": serial_number}
}}
```
{% endcode %}
{% endtab %}
{% endtabs %}
