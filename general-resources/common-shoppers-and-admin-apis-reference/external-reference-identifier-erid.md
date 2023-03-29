---
description: Understand the ERID.
---

# External reference identifier (ERID)

Some companies have internal identifiers for their products. We call them external reference identifiers to distinguish them from our product identifiers. These external reference identifiers may or may not match the product identifier in Global Commerce.&#x20;

You can use an external reference ID (`ERID`) to refer to either a [product](external-reference-identifier-erid.md#best-practices) or a [customer](customer-identifier.md).&#x20;

## Best practices

If you want to use the external reference identifier (ERID) when creating or updating a product or product variation, we recommend that you:

* [Enable the Enforce Unique Value](external-reference-identifier-erid.md#enabling-the-enforce-unique-value) when [configuring company settings](https://help.digitalriver.com/internal-help/gc/Administration/Company/Configuring-company-settings.htm) in Global Commerce. When the Enforce Unique Value is enabled, duplicate ERIDs are not allowed. This ensures that you won't accidentally provide an ERID that would result in duplicate products in the response if you searched for a product by ERID.
* Use the `x-erid-as-pid=true` in your HTTP requests when you provide an ERID. We use the value to identify the ID of the product as either a product identifier (`productId`) or an ERID. A false value indicates the product uses a product identifier. The value is `false` by default.
* Use unique ERIDs for both the base product and its product variations. Don't mix ERIDs and product identifiers in a request.

## Enabling the Enforce Unique Value

To enable the Enforce Unique Value:

1. Sign in to Global Commerce.
2. Select **Administration**, select **Company**, and then click **Configure Company Settings**. The Configure Company Settings page appears.
3. Scroll down to **Product External Reference Number** and select **Yes** next to **Enforce Unique Value**.\
   <img src="../../.gitbook/assets/image (1).png" alt="" data-size="original">
4. Click **Save**.

## Admin APIs and ERID

The `ERID` variable can be one of the following values: an [individual](../admin-apis-reference/products.md#individual-product), [base](../admin-apis-reference/products.md#base-product), or [product variation](../admin-apis-reference/products.md#product-variations) identifier. You can use an ERID when creating a product or updating a product.&#x20;

### Creating a product with an ERID

An ERID request requires the `x-erid-as-pid=true` header. The following example creates a new base product with an `ERID` and product variations using an `variationERID`.

{% hint style="warning" %}
You must [enable the Enforce Unique value](external-reference-identifier-erid.md#enabling-the-enforce-unique-value) before you can use an ERID.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
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
{% endcode %}
{% endtab %}
{% endtabs %}

## Shopper APIs and ERID

You can use an ERID to search for a product or add a product to a cart. The following examples demonstrate how you can use the `externalReferenceId` with the product-related resource.

### Retrieve specific products from the default catalog

The following request gets products with an `externalReferenceId` of `30`, `35`, and `40`.iiiiiiiiiiiii

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 
'https://api.digitalriver.com/v1/shoppers/me/products?externalReferenceId=30,35,40' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Add a product to a shopping cart using the external reference identifier

The following request example adds a product to a cart using the `externalReferenceId` query parameter.

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```json
curl --location --request GET 
'https://api.digitalriver.com/v1/shoppers/me/carts/active/line-items?externalReferenceId=0123456789' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you do not provide a company identifier, The API uses the company identifier associated with the API key.
{% endhint %}

### Add a product by external reference identifier to the shopping cart and redirect to the storefront page

In a typical anonymous customer workflow, you can add products to a cart by external reference identifier, making a single POST call with a payload to the [Web Checkout](https://www.digitalriver.com/docs/commerce-shopper-api/#tag/Web-Checkout) resource. The following payload (request entity) adds a product with the `externalReferenceId` of `123456789`, with a `quantity` of `2`, to a cart.

{% tabs %}
{% tab title="Payload example" %}
{% code overflow="wrap" %}
```json
 {
   "webCheckout": {
     "cart": {
       "lineItems": {
         "lineItem": {
           "quantity": "2",
           "product": {
             "externalReferenceId": "123456789"
            }
              ... more closing curly braces ...
```
{% endcode %}
{% endtab %}
{% endtabs %}

A successful request with this particular API results in a `302 redirect` to a Digital River-hosted guest checkout page.&#x20;
