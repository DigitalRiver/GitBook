---
description: Learn how to add or update a product variation
---

# Adding or updating a product variation

You can [add ](adding-or-updating-a-product-variation.md#adding-a-product-variation-to-a-base-product)or [update a product variation](adding-or-updating-a-product-variation.md#updating-a-specific-product-variation-for-a-base-product) for a base product. Both calls result in the same response when specifying the same `variationId`. As long as you know the `variationId`, you only need to update a specific product variation for a base product.

When adding or updating a product variation, note that:

* The response returns an error if you add an attribute to a product variation that does not exist in the base product.
* The request automatically adds the `locales` object from the base product to each product variation. The response returns an error if the locales are not consistent between the base product and the product variations. For example:
  * If `en_GB` and `en_US` exist in the base product and only `en_US` exists in the product variation, the request will copy `en_GB` to the product variation.
  * if `en_GB` and `en_US` exist in the base product and `ja_JP` exists in the product variation,  the request will return an error in the response

## Adding a product variation to a base product

The following `POST /products/{baseProductId or baseERID}/variations` request creates a product variation for an existing product. <mark style="background-color:orange;">??? TODO: Add a link to the POST request. ???</mark> To add a product variation, you must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid).&#x20;

{% hint style="info" %}
If the base product has a `baseProductId`, the product variation must have a `baseProductId`. You cannot create a base product with variations that `productIds` and `ERIDs` interchangeably.
{% endhint %}

{% tabs %}
{% tab title="baseProductId request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{baseProductId}/variations' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="baseERID request " %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{ERID}/variations' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following payload adds a variation without setting any data.

{% hint style="info" %}
Do not use this request to change the default locale in the payload. Changing the default locale in the payload of this request will result in an error. See [Adding or updating a product's locale](creating-or-updating-a-product.md#adding-or-updating-a-products-locale) for instructions on changing the default locale.
{% endhint %}

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
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
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You must [add an attribute to the base product](creating-or-updating-a-product.md) before you add the attribute to the product variation. An error occurs when the attributes don't match the locale data in the base product. Use the `POST /products/{baseProductId}/variations` request to add an attribute such as locale to a product variation.
{% endhint %}

The request returns a task identifier (`taskId`) in the response.&#x20;

{% tabs %}
{% tab title="202 Accepted response" %}
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
{% endtab %}
{% endtabs %}

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md).&#x20;

## Updating a specific product variation for a base product

The following `POST /products/{baseProductId or baseERID}/variations/{variationId}` request updates any supported attribute, such as the [locale](broken-reference), for a product variation associated with a specific base product ID. <mark style="background-color:orange;">??? TODO: Add a link to the POST request. ???</mark> To update a specific product variation, you must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid)  and the variation identifier (`variationId`).

{% hint style="info" %}
The base product and the product variation must use the same product identifier type. For example, they both use `productId`. You cannot create a base product with variations that use `productIds` and `ERIDs` interchangeably.
{% endhint %}

{% tabs %}
{% tab title="baseProductId request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{baseProductId}/variations/{variationId}' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="baseERID request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{ERID}/variations/{variationId}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

Add the new attributes and/or replace existing attributes in the payload. For example, you can [add or replace locales for a product variation](broken-reference).

{% hint style="info" %}
You must [add an attribute to the base product](creating-or-updating-a-product.md) before you add the attribute to the product variation. An error occurs when the attributes don't match the locale data in the base product. Use the `POST /products/{baseProductId}/variations` request to add an attribute such as locale to a product variation.
{% endhint %}

## Key attributes

The following details describe the key attributes when adding or updating a product variation. For a complete list, refer to the <mark style="background-color:orange;">??? TODO: Add links to creating a new product variation ???</mark> in the API Reference document.

### varyingAttributes

These attributes distinguish the product variation from the base product.

#### attributeName

<mark style="background-color:orange;">??? How do we want to talk about the</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`attributeName`</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">and</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`attributeValue`</mark><mark style="background-color:orange;">? Are they customizable? Can you provide examples? ???</mark>

#### attributeValue

### deploymentRequiredChanges

Any changed attributes in this object will not go live until you deploy the product. This object includes the following attributes:

#### fulfillmentTypes

A fulfillment type defines how products are delivered or sent to shoppers. The options are `physical` or `digital`.&#x20;

#### otherFulfillmentIntegration

The Other Fulfillment Integration setting allows you to provide a unique fulfillment for your products. If you have special fulfillment needs that you think could benefit from Other Fulfillment Requirements and integrations, contact your Store Operations team.

* **fulfillerIds**: The fulfiller's identifier.

#### transferProduct

The transfer product identifier. This is a subscription product term. You can use the product identifier (productID) or the external reference identifier (ERID). The base product cannot be a transfer product.

#### upgradeProducts

The upgrade product identifier. This is a subscription product term. You can use the product identifier (productID) or the external reference identifier (ERID). The base product cannot be an upgrade product.

#### downgradeProducts

The downgrade product identifier. This is a subscription product term. You can use the product identifier (productID) or the external reference identifier (ERID). The base product cannot be a downgraded product.

### liveChanges

The changed attributes under this object will go live immediately. You do not need to deploy these changes. You can use these attributes to insert live changes when creating a product. After creating the product, the fields are read-only. You can apply live changes by using the POST /products/{productId}/live-changes API. This object is available when you update a product. This object includes the following attributes:

#### externalReferenceId

The external reference identifier. A unique identifier for the product from the Digital River client.

#### catalogs

The collection of products for sale on your site. A catalog contains categories to organize your products.

* **calalogId**: The catalog identifier.
* **categories**: Categories are used to organize products within a catalog and often appear on the store to help shoppers locate products and navigate the store/site.
  * **categoryId**: The category identifier.
* **pricing**: The price of a product by currency and locale.
* **type**: The type of the price list. Used to classify the prices in a price list. A price list type may also indicate how the price list or pricing will be used. For example, you can create an MSRP list, a subscription renewal price list, and so on.
* **prices**: The prices of a product.&#x20;
  * **currency**: A three-letter [ISO 4217](https://www.xe.com/iso4217.php) currency code.
  * **locale**: Optional. If your store supports multiple locales, your price list will contain space for you to enter pricing in currencies used by the locales supported by your store. The price you enter for a product in a currency will be used by any locale that uses the currency in which you entered the price.
  * **configuredPrice**: The configured price for the product.

### localizations

The supported locales for the product.

#### locale

The product's supported locale.

#### isDefault

When set to `true`, the locale is the default locale.

#### groups

An array of grouped attributes is associated with the locale. <mark style="background-color:orange;">??? Dev needs to add the missing attributes to the YAML file. I filled in the gaps here where I could. ???</mark>

* **groupId**: The group identifier for the attributes (for example, 1100). This field is read-only. You do not need to provide this attribute in the request. It will be ignored when creating or updating the product
* **groupName**: The group name for the attributes. This field is read-only. You do not need to provide this attribute in the request. It will be ignored when creating or updating the product.
*   **attributes**: An array of properties associated with the group. \


    The possible attributes are as follows:

    * **Name**: The name of a product as it appears in reports, offers, and other places within Global Commerce. Shoppers will not see this name in your store. For example: `sys-acme-test-name-{{defaultLocale}}`
    * **displayName**: The public-facing product name as it appears in your store. Shoppers can see this name when they browse your store or use this name when they search your store. For example: `display-name-{{defaultLocale}}`
    * **sku**: The stock keeping unit (SKU) or product name. For example: `sku-test-{{defaultLocale}}`
    * **shortDescription**: A brief description of the product. For example: `shortDescription-{{defaultLocale}}`
    *   **eccn**: A SKU's `eccn` represents its [Export Control Classification Number](https://www.bis.doc.gov/index.php/licensing/commerce-control-list-classification/export-control-classification-number-eccn) (ECCN). For example: `EAR990`\
        \
        This value determines whether:

        * A product requires a U.S. export/re-export license
        * A product contains any other license requirements/restrictions
        * A product has an end-use that is prohibited by applicable export control laws

        Digital River's [legal documentation](https://www.digitalriver.com/legal-information/) lists [ECCNs pre-approved](https://www.digitalriver.com/legal-other/approved-eccns/) for use in the Product Admin APIs. In the table's description field, you may find additional requirements and restrictions that further limit the use of the ECCN.

        {% hint style="danger" %}
        Digital River can only resell products with these listed ECCNs. If you have a product with an ECCN that you'd like to be considered for addition to the list, please contact [Legal-compliance@digitalriver.com](mailto:Legal-compliance@digitalriver.com)**.**
        {% endhint %}

        * **manufacturingCountry**:
        * **taxableUnspscCode**: For example: `43230000` <mark style="background-color:orange;">??? What is this code? I found it in the Postman collection. ???</mark>
        * **taxableProductCode**: For example: `4323.320_A` <mark style="background-color:orange;">??? What is this code? I found it in the Postman collection. ???</mark>
        * **downloadFulfillment**: For example: `thirdParty` <mark style="background-color:orange;">??? What is this attributte? I found it in the Postman collection. ???</mark>

<mark style="background-color:orange;"></mark>
