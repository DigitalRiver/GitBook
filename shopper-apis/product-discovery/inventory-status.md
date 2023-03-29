---
description: Learn how to retrieve a product's inventory status.
---

# Inventory status

## Getting the inventory status for one or more products

The following [`GET /v1/shoppers/me/products/inventory-status`](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Inventory-Status/paths/\~1v1\~1shoppers\~1me\~1products\~1inventory-status/get) request gets the inventory for a specific product. You can use either the [product identifier](../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or an [external reference identifier](../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) as a query parameter. Passing an invalid product identifier or external reference identifier will be ignored. If you do not provide an identifier, the request returns an empty collection with a 200 status.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/products/inventory-status' \
--header 'authorization: bearer ***\ 
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
<pre class="language-json" data-overflow="wrap"><code class="lang-json">{  
    "products": {    
<strong>        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/inventorystatus",    
</strong><strong>        "inventoryStatus": [
</strong><strong>          {
</strong><strong>              "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/inventory-status",
</strong><strong>              "product": [
</strong><strong>                {
</strong><strong>                    "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",            
</strong><strong>                    "id": 64578500,
</strong><strong>                    "externalReferenceId": "Test External Reference Number",            
</strong><strong>                    "companyId": "demosft1"
</strong><strong>                  }
</strong><strong>              ],        
</strong><strong>              "availableQuantity": 2147483647,        
</strong><strong>              "availableQuantityIsEstimated": "false",        
</strong><strong>              "productIsInStock": "true",
</strong><strong>              "productIsAllowsBackorders": "true",
</strong><strong>              "productIsTracked": "false",
</strong><strong>              "requestedQuantityAvailable": "true",
</strong><strong>              "status": "PRODUCT_INVENTORY_IN_STOCK", 
</strong><strong>             "statusIsEstimated": "false",        
</strong><strong>             "expectedInStockDate": "string",        
</strong><strong>             "customStockMessage": "string"      
</strong><strong>         }    
</strong><strong>     ]  
</strong><strong> } 
</strong><strong>}
</strong></code></pre>
{% endtab %}
{% endtabs %}

## Getting the inventory status for a specific product

The following [GET /v1/shoppers/me/products/{productId}/inventory-status](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Inventory-Status/paths/\~1v1\~1shoppers\~1me\~1products\~1%7BproductId%7D\~1inventory-status/get) request gets the inventory for a specific product identifier (`productId`). You must provide the `productId`.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```html
curl --location --request GET 'https://api.digitalriver.com/v1/shoppers/me/products/{productId}/inventorystatus' \
--header 'Authorization: Basic ***' \ 
...
```
{% endcode %}
{% endtab %}

{% tab title="Second Tab" %}
{% code overflow="wrap" %}
```json
{  
    "inventoryStatus": {    
        "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500/inventory-status",    
        "product": [      
            {        
                "uri": "https://api.digitalriver.com/v1/shoppers/me/products/64578500",        
                "id": 64578500,        
                "externalReferenceId": "Test External Reference Number",        
                "companyId": "demosft1"      
            }    
        ],    
        "availableQuantity": 2147483647,    
        "availableQuantityIsEstimated": "false",    
        "productIsInStock": "true",    
        "productIsAllowsBackorders": "true",    
        "productIsTracked": "false",    
        "requestedQuantityAvailable": "true",    
        "status": "PRODUCT_INVENTORY_IN_STOCK",    
        "statusIsEstimated": "false",    
        "expectedInStockDate": "string",    
        "customStockMessage": "string"  
    } 
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
