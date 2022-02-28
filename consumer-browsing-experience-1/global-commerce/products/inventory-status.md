---
description: Learn how to retrieve a product's inventory status.
---

# Inventory status

The following [`GET /v1/shoppers/me/products/{productId}/inventory-status`](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Inventory-Status/paths/\~1v1\~1shoppers\~1me\~1products\~1{productId}\~1inventory-status/get) request gets the inventory for a specific product. You must provide the product `id`.

{% tabs %}
{% tab title="cURL" %}
```javascript

curl --location --request GET 'http://{host}/v1/shoppers/me/products/{productId}/inventory-status' \
--header 'Content-Type: application/json' \
--header 'Authorization: Basic ***' \
```
{% endtab %}
{% endtabs %}

You will receive a `200 OK` response.

{% tabs %}
{% tab title="JSON" %}
```
{
   "inventoryStatus": {
      "product": {
         "id": "{productId}",
         "externalReferenceId": "{externalReferenceId}",
         "companyId": "{companyId}",
         "_uri": "https://api.digitalriver.com/v1/shoppers/me/products/{productId}"
      },
      "availableQuantity": "0",
      "availableQuantityIsEstimated": "false",
      "productIsInStock": "false",
      "productIsAllowsBackorders": "false",
      "productIsTracked": "true",
      "requestedQuantityAvailable": "false",
      "status": "PRODUCT_INVENTORY_OUT_OF_STOCK",
      "statusIsEstimated": "false",
      "expectedInStockDate": "2021-08-12T00:00:00.000Z",
      "customStockMessage": "",
      "_uri": "https://api.digitalriver.com/v1/shoppers/me/products/{productId}/inventory-status"
   }
}
```
{% endtab %}
{% endtabs %}
