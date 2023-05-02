---
description: Understand the basics of products.
---

# Products

A product (a stock keeping unit or SKU) is a sellable item or service. Products in your Digital River catalog contain all required attributes to complete an end-consumer transaction (payments, tax, and fulfillment). You can generally configure the product in one of two ways:

* An [individual product](products.md#individual-product) (single sellable SKU)
* A [base product](products.md#base-product) with [product variations](products.md#product-variations) (base product with multiple sellable SKU variants)

You can retrieve the catalog product information, including applicable discounted prices, by leveraging the available product endpoints.

## Individual product

An individual product is a single item, such as a downloadable song, or a collection of items, such as a box set. Use the `POST /v1/products` request to [create an individual product](../../admin-apis/product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) and the `POST /products/{productId}` request to [update an individual product](../../admin-apis/product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product). There are no [product variations](products.md#product-variations) associated with it.

{% hint style="info" %}
To [convert an individual product to a base product or a base product to an individual product](https://help.digitalriver.com/help/gc/Products/All-Products/Editing-a-product.htm#AddingRemovingVariations), use [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
{% endhint %}

An individual product is a single sellable stock keeping unit (SKU). The following image shows an example of a SKU:

![](<../../.gitbook/assets/individual\_product (1).png>)

## Base product

&#x20;If a product comes in different colors, sizes, or versions, it is easier to maintain a base product with [product variations ](products.md#product-variations)than a handful of nearly identical products.

You can [create a base product](../../admin-apis/product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) (parent) that contains the common attributes for all product variations (children) of that product. All product variations inherit common attributes. For example, if two variations of a base product require the same product images, add those images to the base product before creating your variations.

{% hint style="info" %}
**Note**: A shopper cannot add a base product to a cart. They can only add the [product variation](products.md#product-variations) to the cart. For example, a shopper can go to the Digital River-hosted storefront and choose a product variation from an interstitial page. The store template automates and controls this behavior.
{% endhint %}

Use the `POST /v1/products` request to [create a base product](../../admin-apis/product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) and the `POST /v1/products/{productId}` request to [update a base product](../../admin-apis/product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#updating-an-individual-or-base-product).&#x20;

## Product variations

Product variations are different versions of a base product that a shopper can purchase, such as different versions, sizes, or capacities. When you [add a product variation](../../admin-apis/product-management/manage-products-asynchronous-api/adding-or-updating-a-product-variation.md), the request copies the common attributes from the base product to the variation. You must change the appropriate attributes and settings to make that variation unique. Each product variation contains attributes and settings that are unique to that product variation.&#x20;

You must change at least one common attribute to make the product variation unique. Only change those settings or attributes that are unique to the variation to reduce operational maintenance.

The following image shows an example of a product variant on a store's website:

![](<../../.gitbook/assets/product-with-variants (1).png>)

## Creating a base product with variations

You can choose to either:

* [Create a base product first and add the product variations later](products.md#create-the-base-product-first)
* [Create the base products and product variations in one call](products.md#create-the-base-product-and-product-variations-simultaneously)

### Create the base product first

[Create the base product](../../admin-apis/product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) first and include the common attributes. If you choose not to define some of the common attributes, those attributes will not be available when you [add a product variation](../../admin-apis/product-management/manage-products-asynchronous-api/adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product).

{% hint style="success" %}
Define as many common attributes as possible for the base product before you create a product variation.
{% endhint %}

You can add the product variations to that base product later.

### Create the base product and product variations simultaneously

You can [create a base product and all its product variations](../../admin-apis/product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) using one call by adding the [`variations`](../../admin-apis/product-management/manage-products-asynchronous-api/creating-or-updating-a-product.md#creating-an-individual-or-base-product) object to the payload. The request copies the common attributes from the base product to each product variation. You modify the attributes for each product variation in the payload when you [update the product variation](../../admin-apis/product-management/manage-products-asynchronous-api/adding-or-updating-a-product-variation.md#updating-a-specific-product-variation).&#x20;

{% tabs %}
{% tab title="cURL example 1" %}
The following example adds or updates a base product and its product variations.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "companyId":"digitalriver",
    "deploymentRequiredChanges": {
        "fulfillmentTypes": ["Download","Physical"]
    },
    "liveChanges": {
        "externalId": "external-reference-id-{{uuid}}",
        "catalogs" : [ {
            "catalogId" : "4783669800",
            "pricing" : [ {
                "type": "listPrice",
                "prices": [{
                    "currency": "USD",
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
            "name": "product-name",
            "displayName": "Product Display Name",
            "sku": "product-sku",
            "manufacturer": "manufacturer-20220308-01",
            "mfrPartNumber": "mfrPartNumber-20220308-01",
            "returnMethod": "LOD",
            "productReturnMethod": "ByAgentAndSelfService",
            "taxableUnspscCode": "43210000",
            "taxableProductCode": "4321_C",
            "privateStoreOnly": true,
            "isViewable": true,
            "isOrderable": true,
            "nonSolr": true,
            "shortDescription": "shortDescription",
            "longDescription": "longDescription",
            "keywords": "keywords",
            "emailAddlInfoText": "emailAddlInfoText",
            "emailAddlInfo": "emailAddlInfo",
            "confirmAddlInfo": "confirmAddlInfo"
          }           
        },
        {
          "groupId": "16",
          "groupName": "Export Controls",
          "attributes": {
            "eccn": "3A992",
            "ccats": "display-name-1234test",
            "licenseException": "APP",
            "harmonizeCode": "hcode",
            "manufactureCountry": "US"
          }
        }   
      ]
    }
    ],
     "variations": [
         {
            "productType": "VARIATION",
            "companyId": "cast",
            "deploymentRequiredChanges": {
            },
            "varyingAttributes": [
                {
                    "attributeName": "platform",
                    "attributeValue": "1 user"
                },
                {
                    "attributeName": "fulfillmentType",
                    "attributeValue": "Download"
                }
            ],
             "localizations": [
                {
                    "locale": "en_US",
                    "isDefault": "true",
                    "groups": [
                        {
                            "groupId": "11",
                            "groupName": "Software",
                            "attributes": {
                                "name": "product-name-V1",
                                "displayName": "Product-display-V1",
                                "sku": "demo-sku-AAAA-V1",
                                "taxableUnspscCode": "43210000",
                                "taxableProductCode": "4321_C",
                                "isViewable": true,
                                "isOrderable": true,
                                "nonSolr": true
                            }
                        },
                        {
                            "groupId": "16",
                            "groupName": "Export Controls",
                            "attributes": {
                                "eccn": "3A992",
                                "ccats": "V1{{uuid}}",
                                "licenseException": "APP",
                                "harmonizeCode": "hcode",
                                "manufactureCountry": "US"
                            }
                        }
                    ]
                }
            ]
        }
        
     ]
}'
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted Response" %}
The request returns a task identifier (`taskId`) in the response.

{% code overflow="wrap" %}
```json
{
    "taskId": "add1797e-2f98-4e7a-9894-c71d6b5640bb",
    "requestType": "CREATE_PRODUCT",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-12-13T09:13:24.370Z"
}
```
{% endcode %}

Use the `taskId` in the response to verify the successful completion of the request.  You can also verify the successful completion of the task by [checking the product history](products.md#product-history-attributes) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Note that there may be a delay before these chances appear in Global Commerce.&#x20;
{% endtab %}
{% endtabs %}

The following example verifies the successful completion of the request shown above.

{% tabs %}
{% tab title="cURL example 2" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 
'https://api.digitalriver.com/v1/products/tasks/add1797e-2f98-4e7a-9894-c71d6b5640bb' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
    "taskId": "add1797e-2f98-4e7a-9894-c71d6b5640bb",
    "products": [
        {
            "id": "51762690080",
            "productType": "BASE"
        },
        {
            "id": "51762700080",
            "productType": "VARIATION"
        }
    ],
    "requestType": "CREATE_PRODUCT",
    "taskStatus": "COMPLETED",
    "receivedTime": "2022-12-13T09:13:24.370Z",
    "finishedTime": "2022-12-13T09:13:25.019Z"
}

```
{% endcode %}
{% endtab %}
{% endtabs %}

## Physical and digital products

Use the Admin API fulfillment types (`fulfillmentTypes`) to define how to deliver products to shoppers. The options are empty (`""`), `physical` or `download`. When the value is empty, the product is neither physical nor download. The empty value reflects the Other setting in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) for service, warranty, entitlement, and so on. Digital River supports two types of digital products: subscription and download.

## Products resources

In this topic, you'll find information on some of the `products` attributes used when [creating ](products.md#creating-an-individual-or-base-product)or [updating a product](products.md#adding-or-updating-a-products-locale). For a complete list, refer to [Create a new individual or base product with variations](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1products/post) in the [Admin APIs](https://www.digitalriver.com/docs/commerce-admin-api/) reference documentation&#x20;

### Deployment required changes&#x20;

Any changed attributes in the `deploymentRequiredChanges` object will not go live until you deploy the product. This object includes the following attributes:&#x20;

#### Fulfillment types&#x20;

A `fulfillmentType` defines how products are delivered to shoppers. The options are empty (`""`), `physical` or `download`. When the value is empty, the fulfillment type is neither a physical nor a  download product. The empty value reflects the Other setting in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) for service, warranty, entitlement, and so on. Digital River supports two types of digital products: subscription and download.

#### Other fulfillment integration&#x20;

The `otherFulfillmentIntegration` setting allows you to provide a unique fulfillment for your products. Contact your Store Operations team if you have special fulfillment needs that could benefit from Other Fulfillment Requirements and integrations.

* **`fulfillerIds`**: The fulfiller's identifier.&#x20;

#### Transfer product

The `transferProduct` is the upgraded product identifier. This is a subscription product term. You can use the product identifier (`productID`) or the external reference identifier (`ERID`) The base product cannot be a transfer product.&#x20;

#### Upgrade products&#x20;

The `upgradeProducts` is the upgraded product identifier for a subscription product. You can use the product identifier (`productID`) or the external reference identifier (`ERID`). You cannot upgrade a base product.

#### Downgrade products&#x20;

The downgradeProducts is the downgrade product identifier for a subscription product. You can use the product identifier (`productID`) or the external reference identifier (`ERID`). You cannot downgrade a base product.

### Localizations

This `localizations` object defines the locales supported by the product.

#### locale&#x20;

The product's supported locale.&#x20;

#### Is default&#x20;

When `isDefault` is set to `true`, the locale is the default locale.

#### groups

The `groups` is an array of grouped attributes associated with the locale.&#x20;

* **`groupId`**: The group identifier for the attributes (for example, 1100). This field is read-only. You do not need to provide this attribute in the request. The request will ignore this attribute when creating or updating the product.
* **`groupName`**: The group name for the attributes. This field is read-only. You do not need to provide this attribute in the request. The request will ignore this attribute when creating or updating the product.
*   **`attributes`**: An array of properties associated with the group. \


    The possible attributes are as follows:

    * **`Name`**: The name of a product as it appears in reports, offers, and other places within Global Commerce. Shoppers will not see this name in your store. For example: `Maverick Sneakers`
    * **`displayName`**: The public-facing product name as it appears in your store. Shoppers can see this name when they browse your store or use it when searching for it. For example: `F-18 Hornet Fighter Jet`
    * **`sku`**: The stock keeping unit (SKU) or product name. For example: `f18`
    * **`shortDescription`**: A brief description of the product. For example: `The Boeing F/A-18E and F/A-18F`` `_`Super`_` ``Hornet are twin-engine, carrier-capable, multirole fighter aircraft...`
    *   **`eccn`**: A SKU's `eccn` represents its [Export Control Classification Number](https://www.bis.doc.gov/index.php/licensing/commerce-control-list-classification/export-control-classification-number-eccn) (ECCN). For example: `EAR990`\
        \
        This value determines whether:

        * A product requires a US export/re-export license
        * A product contains any other license requirements/restrictions
        * A product has an end-use that is prohibited by applicable export control laws

        Digital River's [legal documentation](https://www.digitalriver.com/legal-information/) lists [ECCNs pre-approved](https://www.digitalriver.com/legal-other/approved-eccns/) for use in the Admin APIs. In the table's description field, you may find additional requirements and restrictions that further limit the use of the ECCN.

        {% hint style="danger" %}
        Digital River can only resell products with these listed ECCNs. If you have a product with an ECCN that you'd like to be considered for addition to the list, e contact [Legal-compliance@digitalriver.com](mailto:Legal-compliance@digitalriver.com)**.**
        {% endhint %}

        * **`downloadFulfillment`**: The download fulfillment type. This attribute is required when you are creating a digital product. The valid values are `digitalRiver` or `thirdParty`. If you don't provide this attribute when you create or update a product, the default value is `digitalRiver`.

### Product identifier

The `productId` is the [product identifier](products.md#product-identifier).

### Variations

This `variations` object defines the variation of a base product. This attribute is available when you create a base product. It's only required when you want to create variations of a base product.

#### Varying attributes

These attributes for the `varyingAttributes` object distinguish the product variation from the base product.

* **`attributeName`**: The name of the attribute, such as size.
* **attributeValue**: The attribute's value, such as small, medium, or large.

## Products query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of products. The following topics describe the available query parameters for the `products` request. For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Version

The version string gets the specific version of the product by state. The enums are `DEPLOYED` and `RETIRED`. If you do not specify the version query parameter, the response will contain the latest version. For example, if the product history is as follows:

* Version 1 is **retired**: This product version is retired. Shoppers can no longer see or purchase this product in the store.
* Version 2 is **deployed**: This product version is available in the store. Shoppers can see and purchase this product from your store.&#x20;
* Version 3 is in **design**: This new product version is not yet available in the store. You are planning to deploy this new version eventually. Shoppers cannot see or purchase this product from your store.

Use the following calls can get the different versions:

* If you want to get the retired version (version 1), use the following call:\
  \
  `GET /v1/products/{productId}?version=retired`
* If you want to get the deployed version (version 2), use the following call:\
  \
  `GET /v1/products/{productId}?version=deployed`
* If you want to get the latest unreleased version, use the following call:\
  \
  `GET /v1/products/{productId}`

See [Getting the deployed version of a product](../../admin-apis/product-management/manage-products-asynchronous-api/deploying-a-product.md#getting-the-deployed-version-of-a-product) for more information.

## Variations resource

The following details describe the key attributes when adding or updating a product variation. Refer to the [Update a product variation](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D/post) in the [Admin APIs Reference](https://www.digitalriver.com/docs/commerce-admin-api/) document for a complete list.

#### Varying attributes

These attributes distinguish the product variation from the base product.

* **`attributeName`**: The name of the attribute, such as size.
* **`attributeValue`**: The attribute's value, such as small, medium, or large.

### Deployment required changes

Any changed attributes in the `deploymentRequiredChanges` object will not go live until you deploy the product. This object includes the following attributes:&#x20;

#### Fulfillment types&#x20;

A `fulfillmentType` defines how products are delivered to shoppers. The options are empty (`""`), `physical` or `download`. When the value is empty, the product is neither a physical nor a download. The empty value reflects the Other setting in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) for service, warranty, entitlement, and so on. Digital River supports two types of digital products: subscription and download.

#### Other fulfillment integration&#x20;

The `otherFulfillmentIntegration` setting allows you to provide a unique fulfillment for your products. If you have special fulfillment needs that could benefit from Other Fulfillment Requirements and integrationsContact your Store Operations team if.

* **`fulfillerIds`**: The fulfiller's identifier.&#x20;

#### Transfer product

The `transferProduct` is the upgraded product identifier. This is a subscription product term. You can use the product identifier (`productID`) or the external reference identifier (`ERID`) The base product cannot be a transfer product.&#x20;

#### Upgrade products&#x20;

The `upgradeProducts` is the upgraded product identifier for a subscription product. You can use the product identifier (`productID`) or the external reference identifier (`ERID`). You cannot upgrade a base product.

#### Downgrade products&#x20;

The `downgradeProducts` is the downgrade product identifier for a subscription product. You can use the product identifier (`productID`) or the external reference identifier (`ERID`). You cannot downgrade a base product.

### Live changes&#x20;

The changed attributes under the `liveChanges` object will go live immediately. You do not need to deploy these changes. When creating a product, you can use the following attributes to insert live changes. After creating the product, the fields are read-only. You can apply live changes by using the `POST /v1/products/{productId}/live-changes` API. This object is available when you update a product. This object includes the following attributes:

#### External reference ID&#x20;

The `externalReferenceId` is the product's [external reference identifier](products.md#externalreferenceid). It's your company's unique identifier for the product.&#x20;

#### Catalogs&#x20;

A `catalog` is a collection of products for sale on your site. A catalog contains categories to organize your products.&#x20;

* **`cattlogId`**: The catalog identifier. The variation catalog and category are inherited from the [base product](products.md#base-product). The information will be provided in the [product variation](products.md#product-variations) but ignored if you insert that information in a product variation request.
* **`categories`**: Use categories to organize products within a catalog, often appearing in the store to help shoppers locate products and navigate the store or site.
  * **`categoryId`**: The category identifier.
* **`pricing`**: The price of a product by currency and locale.&#x20;
  * **`type`**: The price list type. Used to classify the prices in a price list. A price list type may also indicate how the price list or pricing will be used. For example, you can create an MSRP list, a subscription renewal price list, and so on.&#x20;
  * **`prices`**: The prices of a product.&#x20;
    * **`currency`**: A three-letter [ISO 4217](https://www.xe.com/iso4217.php) currency code.&#x20;
    * **`locale`**: Optional. If your store supports multiple locales, your price list will contain the currency for each of the supported locales. When you enter a price for a product by currency, any locale that uses that currency will use the price you provided.
    * **`configuredPrice`**: The configured price for the product.&#x20;

### Localizations

This `localizations` object defines the locales supported by the product.

#### locale&#x20;

The product's supported locale.&#x20;

#### Is default&#x20;

When `isDefault` is set to `true`, the locale is the default locale.

#### groups

The `groups` is an array of grouped attributes associated with the locale.&#x20;

* **`groupId`**: The group identifier for the attributes (for example, 1100). This field is read-only. You do not need to provide this attribute in the request. The request will ignore this attribute when creating or updating the product.
* **`groupName`**: The group name for the attributes. This field is read-only. You do not need to provide this attribute in the request. The request will ignore this attribute when creating or updating the product.
*   **`attributes`**: An array of properties associated with the group. \


    The possible attributes are as follows:

    * **`Name`**: The name of a product as it appears in reports, offers, and other places within Global Commerce. Shoppers will not see this name in your store. For example: `sys-acme-test-name-{{defaultLocale}}`
    * **`displayName`**: The public-facing product name as it appears in your store. Shoppers can see this name when they browse your store or use it when searching it. For example: `display-name-{{defaultLocale}}`
    * **`sku`**: The stock keeping unit (SKU) or product name. For example: `sku-test-{{defaultLocale}}`
    * **`shortDescription`**: A brief description of the product. For example: `shortDescription-{{defaultLocale}}`
    * **eccn**: SKU's `eccn` represents its [Export Control Classification Number](https://www.bis.doc.gov/index.php/licensing/commerce-control-list-classification/export-control-classification-number-eccn) (ECCN). For example: `EAR990`\
      \
      This value determines whether:
    *

        * A product requires a US export/re-export license
        * A product contains any other license requirements/restrictions
        * A product has an end-use that is prohibited by applicable export control laws

        Digital River's [legal documentation](https://www.digitalriver.com/legal-information/) lists [ECCNs pre-approved](https://www.digitalriver.com/legal-other/approved-eccns/) for use in the Admin APIs. In the table's description field, you may find additional requirements and restrictions that further limit the use of the ECCN.

        {% hint style="danger" %}
        Digital River can only resell products with these listed ECCNs. If you have a product with an ECCN that you'd like to be considered for addition to the list, contact [Legal-compliance@digitalriver.com](mailto:Legal-compliance@digitalriver.com)**.**
        {% endhint %}

        * **`downloadFulfillment`**: The download fulfillment type. This attribute is required when you are creating a digital product. The valid values are `digitalRiver` or `thirdParty`. If you don't provide this attribute when you create or update a product, the default value is `digitalRiver`.
