---
description: Learn how to add or update a product variation
---

# Adding or updating a product variation

You can [add ](adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product)or [update a product variation](adding-or-updating-a-product-variation.md#updating-a-specific-product-variation-for-a-base-product) for a base product. Both calls result in the same response when specifying the same `productId`. As long as you know the `productId` for the product variation, you only need to update that product variation.

When adding or updating a product variation, note that:

* The response returns an error if you add an attribute to a product variation that does not exist in the base product.
* The request automatically adds the `locales` object from the base product to each product variation. The response returns an error if the locales are not consistent between the base product and the product variations. For example:
  * If `en_GB` and `en_US` exist in the base product and only `en_US` exists in the product variation, the request will copy `en_GB` to the product variation.
  * if `en_GB` and `en_US` exist in the base product and `ja_JP` exists in the product variation,  the request will return an error in the response

## Adding a product variation to a base product

The following [`POST /v1/products/{baseProductId or baseERID}/variations`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D/post) request creates a product variation for an existing product. To add a product variation, you must provide either the base product's [`productId`](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md).&#x20;

{% hint style="info" %}
Do not use this request to change the default locale in the payload. Changing the default locale in the payload of this request will result in an error. See [Adding or updating a product's locale](creating-or-updating-a-product.md#adding-or-updating-a-products-locale) for instructions on changing the default locale.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
The following example adds a product variation to a base product with a `baseProductId`. It also adds a product variation without setting any data. See the `variations` resource for a description of the attributes.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{baseProductId}/variations' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
  "varyingAttributes": [
    {
      "attributeName": "color",
      "attributeValue": "red"
    },
    {
      "attributeName": "size",
      "attributeValue": "large"
    }
  ],
  "deploymentRequiredChanges": {},
  "liveChanges": {},
  "localizations": []
}'
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header. It also adds a product variation without setting any data.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{baseERID}/variations' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
--data-raw '{
  "varyingAttributes": [
    {
      "attributeName": "color",
      "attributeValue": "red"
    },
    {
      "attributeName": "size",
      "attributeValue": "large"
    }
  ],
  "deploymentRequiredChanges": {},
  "liveChanges": {},
  "localizations": []
}'
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

{% code overflow="wrap" %}
```json
{
    "taskId": "eac67608-2fd6-4156-88f1-8ecb98aad9b0",
    "requestType": "UPDATE_VARIATION",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-08-11T21:59:28.089Z"
}
```
{% endcode %}

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/#verifying-the-successful-completion-of-multiple-products).&#x20;
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You must [add an attribute to the base product](creating-or-updating-a-product.md) before you add the attribute to the product variation. An error occurs when the attributes don't match the locale data in the base product. Use the `POST /v1/products/{baseProductId or baseERID}/variations` request to add an attribute such as locale to a product variation.
{% endhint %}

## Updating a specific product variation

The following [`POST /v1/products/{baseProductId or baseERID}/variations/{productVariationId or variationERID}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D/post) request updates on any supported attribute, such as the [locale](creating-or-updating-a-product.md#adding-or-updating-a-products-locale), for a specific product variation. To update a specific product variation, you must provide either the product variation identifier (`productVariationId`) or the variation ERID (`variationERID`).

{% tabs %}
{% tab title="cURL" %}
The following example updates a specific product variation with a `productVariationId`. See the `variations` resource for a description of the attributes.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{baseProductId}/variations/{productVariationId}' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
 "localizations": [
    {
      "locale": "en_US",
      "isDefault": "true",
      "groups": [
        {
          "groupId": "11",
          "groupName": "Software",
          "attributes": {
            "name": "UpdatedVariation_-{{uuid}}",
            "displayName": "UpdatedVariation_-display-{{uuid}}",
            "sku": "Variation_-sku-{{uuid}}",
            "manufacturer": "Variation_manufacturer-20220308-01",
            "mfrPartNumber": "Variation_mfrPartNumber-20220308-01",
            "returnMethod": "LOD",
            "productReturnMethod": "ByAgentAndSelfService",
            "taxableUnspscCode": "43210000",
            "taxableProductCode": "4321_C",
            "isViewable": true,
            "isOrderable": true,
            "nonSolr": true,
            "shortDescription": "Variation_shortDescription-{{uuid}}",
            "longDescription": "Variation_longDescription-{{uuid}}",
            "keywords": "Variation_keywords-{{uuid}}",
            "emailAddlInfoText": "emailAddlInfoText-{{uuid}}",
            "emailAddlInfo": "emailAddlInfo-{{uuid}}",
            "confirmAddlInfo": "confirmAddlInfo-{{uuid}}"
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
    ]   
}'
```
{% endcode %}

An `ERID` request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{baseERID}/variations/{variationERID}' \
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
          "groupId": "11",
          "groupName": "Software",
          "attributes": {
            "name": "UpdatedVariation_-{{uuid}}",
            "displayName": "UpdatedVariation_-display-{{uuid}}",
            "sku": "Variation_-sku-{{uuid}}",
            "manufacturer": "Variation_manufacturer-20220308-01",
            "mfrPartNumber": "Variation_mfrPartNumber-20220308-01",
            "returnMethod": "LOD",
            "productReturnMethod": "ByAgentAndSelfService",
            "taxableUnspscCode": "43210000",
            "taxableProductCode": "4321_C",
            "isViewable": true,
            "isOrderable": true,
            "nonSolr": true,
            "shortDescription": "Variation_shortDescription-{{uuid}}",
            "longDescription": "Variation_longDescription-{{uuid}}",
            "keywords": "Variation_keywords-{{uuid}}",
            "emailAddlInfoText": "emailAddlInfoText-{{uuid}}",
            "emailAddlInfo": "emailAddlInfo-{{uuid}}",
            "confirmAddlInfo": "confirmAddlInfo-{{uuid}}"
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
    "taskId": "9e3dbe0e-98fc-4c88-8868-03fdde5fcdb6",
    "requestType": "UPDATE_VARIATION",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-11-28T21:02:58.187Z"
}
```
{% endcode %}

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/#verifying-the-successful-completion-of-multiple-products).&#x20;
{% endtab %}
{% endtabs %}

Add the new attributes and/or replace existing attributes in the payload. For example, you can [add or replace locales for a product variation](adding-or-updating-a-product-variation.md#updating-a-specific-product-variation-for-a-base-product).

{% hint style="info" %}
You must [add an attribute to the base product](creating-or-updating-a-product.md) before you add the attribute to the product variation. An error occurs when the attributes don't match the locale data in the base product. Use the `POST /v1/products/{baseProductId or baseERID}/variations` request to add an attribute such as locale to a product variation.
{% endhint %}

## Updating a specific product variation for a base product

The following [`POST /v1/products/{baseProductId or baseERID}/variations/{productVariationId or variationERID}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D/post) request updates on any supported attribute, such as the [locale](creating-or-updating-a-product.md#adding-or-updating-a-products-locale), for a product variation associated with a specific base product ID. To update a specific product variation, you must provide either a unique [`productId` ](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md)or [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md).   for both the base product and product variation.

{% hint style="info" %}
The base product and the product variation must use the same product identifier type. For example, they both use `productId`. You cannot  use `productIds` and `ERIDs` interchangeably when updating a product variation for a specific base product.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
The following example updates a specific product variation with a `productId` for a base product. See the `variations` resource for a description of the attributes.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{baseProductId}/variations/{productVariationId}' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
 "localizations": [
    {
      "locale": "en_US",
      "isDefault": "true",
      "groups": [
        {
          "groupId": "11",
          "groupName": "Software",
          "attributes": {
            "name": "UpdatedVariation_-{{uuid}}",
            "displayName": "UpdatedVariation_-display-{{uuid}}",
            "sku": "Variation_-sku-{{uuid}}",
            "manufacturer": "Variation_manufacturer-20220308-01",
            "mfrPartNumber": "Variation_mfrPartNumber-20220308-01",
            "returnMethod": "LOD",
            "productReturnMethod": "ByAgentAndSelfService",
            "taxableUnspscCode": "43210000",
            "taxableProductCode": "4321_C",
            "isViewable": true,
            "isOrderable": true,
            "nonSolr": true,
            "shortDescription": "Variation_shortDescription-{{uuid}}",
            "longDescription": "Variation_longDescription-{{uuid}}",
            "keywords": "Variation_keywords-{{uuid}}",
            "emailAddlInfoText": "emailAddlInfoText-{{uuid}}",
            "emailAddlInfo": "emailAddlInfo-{{uuid}}",
            "confirmAddlInfo": "confirmAddlInfo-{{uuid}}"
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
    ]   
}'
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{baseERID}/variations/{variationERID}' \
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
          "groupId": "11",
          "groupName": "Software",
          "attributes": {
            "name": "UpdatedVariation_-{{uuid}}",
            "displayName": "UpdatedVariation_-display-{{uuid}}",
            "sku": "Variation_-sku-{{uuid}}",
            "manufacturer": "Variation_manufacturer-20220308-01",
            "mfrPartNumber": "Variation_mfrPartNumber-20220308-01",
            "returnMethod": "LOD",
            "productReturnMethod": "ByAgentAndSelfService",
            "taxableUnspscCode": "43210000",
            "taxableProductCode": "4321_C",
            "isViewable": true,
            "isOrderable": true,
            "nonSolr": true,
            "shortDescription": "Variation_shortDescription-{{uuid}}",
            "longDescription": "Variation_longDescription-{{uuid}}",
            "keywords": "Variation_keywords-{{uuid}}",
            "emailAddlInfoText": "emailAddlInfoText-{{uuid}}",
            "emailAddlInfo": "emailAddlInfo-{{uuid}}",
            "confirmAddlInfo": "confirmAddlInfo-{{uuid}}"
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
    ]   
}'
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

```
{
    "taskId": "9e3dbe0e-98fc-4c88-8868-03fdde5fcdb6",
    "requestType": "UPDATE_VARIATION",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-11-28T21:02:58.187Z"
}
```

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/#verifying-the-successful-completion-of-multiple-products).&#x20;
{% endtab %}
{% endtabs %}

Add the new attributes and/or replace existing attributes in the payload. For example, you can [add or replace locales for a product variation](adding-or-updating-a-product-variation.md#updating-a-specific-product-variation-for-a-base-product).

{% hint style="info" %}
You must [add an attribute to the base product](creating-or-updating-a-product.md) before you add the attribute to the product variation. An error occurs when the attributes don't match the locale data in the base product. Use the `POST /v1/products/{baseProductId}/variations` request to add an attribute such as locale to a product variation.
{% endhint %}
