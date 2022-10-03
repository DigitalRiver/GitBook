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

* You can [create a base product with variations](creating-or-updating-a-product.md#creating-an-individual-or-base-product) by adding the `variations` object to the payload. When you create[ a product without a `variations` object](creating-or-updating-a-product.md#creating-an-individual-or-base-product), it is an individual product.
* The request automatically adds the `locales` object from the base product to each product variation. An error appears in the response if the locales are not consistent between the base product and the product variations.
  * If `en_GB` and `en_US` exist in the base product and only `en_US` exists in the product variation, the request copies `en_GB` to the product variation.
  * if `en_GB` and `en_US` exist in the base product and `ja_JP` exists in the product variation,  the response returns an error.
* The request updates the correct attribute value even if the attribute value is in the wrong group. For example, if you put the `eccn` attribute for export control in the storefront setting group, the request will update the `eccn` attribute as long as the value is correct, but the response will put the attribute in the export control group where it belongs.

## Creating an individual or base product&#x20;

You can create the base product and all of its product variations using one call. When doing so, the request copies the base product attributes to each product variation. You can update the attributes for a product variation by providing the modified attributes for the product variation in the product variation request payload.

The following `POST /products` request creates [base product](../administrator-browser-experience/product-basics/product-types.md#base-product) with [product variations](../administrator-browser-experience/product-basics/product-types.md#product-variations). <mark style="background-color:orange;">??? TODO: Add a link to the POST request. ???</mark> When creating an individual or base product, you must provide either a [`productId`](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier) or [`ERID` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid)for the `id` attribute in the payload. If you are creating a base product with variations, include the [variations ](creating-or-updating-a-product.md#variations)object in the payload.

{% tabs %}
{% tab title="Request" %}
{% code overflow="wrap" %}
```
curl --location --request POST 'https://api.digitalriver.com/products' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following payload creates a new base product with variations.

{% tabs %}
{% tab title="productId payload" %}
{% code overflow="wrap" %}
```json
{
  "productType": "BASE",
  "companyId": "cast",
  "id": "{productId},
  "liveChanges": {
  },
  "variations": [
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var1",
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
      "liveChanges": {
      }
    },
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var2",
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
      "liveChanges": {
      }
    }
  ]
}
```
{% endcode %}
{% endtab %}

{% tab title="ERID payload" %}
<pre class="language-json" data-overflow="wrap"><code class="lang-json"><strong>{
</strong>  "productType": "BASE",
  "companyId": "cast",
  "id": "{ERID},
  "liveChanges": {
  },
  "variations": [
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var1",
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
      "liveChanges": {
      }
    },
    {
      "productType": "VARIATION",
      "companyId": "cast",
      "id": "var2",
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
      "liveChanges": {
      }
    }
  ]
}</code></pre>
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you want to add a locale to a product, you must [add the locale data](creating-or-updating-a-product.md#adding-or-updating-a-products-locale) in the payload using the `POST /products/{productid}` request.
{% endhint %}

The request returns a task identifier (`taskId`) in the response.&#x20;

{% tabs %}
{% tab title="202 Accepted response" %}
{% code overflow="wrap" %}
```json
{
    "taskId": "7aec3f23-3c12-479c-9d1f-4e34d498234b",
    "requestType": "CREATE_PRODUCT",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-08-11T16:32:26.547Z"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md). You can also verify the successful completion of the task by checking the product history in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). <mark style="background-color:orange;">??? Add a task describing how to access the product history. Product Admin changes are marked as Modified by API. Note that there may be a delay before these chances in Global Commerce. ???</mark>

## Updating an individual or  base product

You can send a request to update any supported attribute, such as the [locale](creating-or-updating-a-product.md#adding-or-updating-a-products-locale), for a [base product](../administrator-browser-experience/product-basics/product-types.md#base-product) or [individual product](../administrator-browser-experience/product-basics/product-types.md#individual-product). The change will be visible to the shopper when you deploy the updated product. &#x20;

The following `POST /products/{productId}` request updates the existing base product. When updating a specific individual or base product, you must provide either a [`productId`](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier) or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid).

{% hint style="info" %}
Do not use this request to update a product variation. Adding a `variations` object to the payload for this request will return an error. See [Adding or updating a product variation](adding-or-updating-a-product-variation.md) for instructions on managing product variations.
{% endhint %}

{% tabs %}
{% tab title="productId request" %}
<pre data-overflow="wrap"><code><strong>curl --location --request POST 'https://api.digitalriver.com/products/{productId}' \
</strong>--header 'Authorization: Bearer &#x3C;API_key>' \</code></pre>
{% endtab %}

{% tab title="ERID request" %}
```
curl --location --request POST 'https://api.digitalriver.com/products/{ERID}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endtab %}
{% endtabs %}

In the payload, add the new attributes and/or replace the locale attributes. For example, you can [add or replace locales for a product variation](creating-or-updating-a-product.md#adding-or-updating-a-products-locale).

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
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
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

The request returns a task identifier (`taskId`) in the response.&#x20;

{% tabs %}
{% tab title="202 Accepted response" %}
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
{% endtab %}
{% endtabs %}

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md). You can also verify the successful completion of the task by checking the product history in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). <mark style="background-color:orange;">??? Add a task describing how to add the product history. Product Admin changes are marked as Modified by API. Note that there may be a delay before these changes appear in Global Commerce.  ???</mark>

### Viewing a product's history

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID in the **Search For** field, and then click **Search**.
4. Click the link for the product under the **Internal Product Name column**. The Edit Product page appears.
5. Click **View History**. The Product History window shows the [product's history](creating-or-updating-a-product.md#product-history-attributes).

### Product History attributes

The following table describes the product history attributes.

| Attribute            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| To Date              | The beginning of the search date range.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| From Date            | The end of the search date range.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Change Type          | <p>A brief description of the change applied to the product. Some of the possible change type values are as follows: </p><ul><li><strong>Copied</strong>—Indicates a user copied the current product from another product. When a user copies an existing product, the Product History page shows the product ID and name of the original product on which the new product is based. </li><li><strong>Revert</strong>—Indicates a user reverted the product to a previous version (and indicates the previous version). For more about reverting a product, see Reverting changes to products. </li><li><p><strong>Save or Save (Including Live Change)</strong>—Indicates you or another user saved a change to the product. Save indicates you must deploy the product before shoppers can see the change in your store. Save (Live Change) indicates the system automatically applied the change to your store, and you do not need to deploy the product.<br><br>You can click the plus (+) sign next to a save event to see additional information for that event. One or more of the following columns appear with every save event: </p><ul><li><strong>Locale</strong>—Indicates the locales where the change occurred. </li><li><strong>Area</strong>—Indicates the general area in the editor the change occurred. <br>Example: If you change the name, the area lists "Storefront Settings" as the area where you can find the name.</li><li>Field—Displays the changed field. <br><strong>Example</strong>: You can use this field name and the content displayed in the Area column to locate the attribute in Global Commerce.</li><li><strong>Old Value</strong>—Displays the old value. If a value is not present, no content appears in this column. </li><li><strong>New Value</strong>—Displays the new value.<br><strong>Note</strong>: Save does not always mean the item changed. If you view the item and click the Save button without applying any changes, the system logs that change.</li></ul></li></ul><ul><li><strong>Status Changed to Deployed</strong>—Indicates the state of the product changed to the Live state. The changes now appear in your store. </li><li><strong>Status Changed to Design</strong>—Indicates the status of the product changed to the Design state. </li><li><strong>Status Changed to New</strong>—Indicates the status of the product changes to the New state when you create a product. </li><li><strong>Took Ownership</strong>—Indicates that the right to edit a product belongs to a new user. The name of the new user appears in the Modified By column. Ownership means that this user was the last person to edit the product, and no other user can edit the product until they take ownership of the product. Ownership prevents two users from editing the product at the same time. </li><li><strong>Variation Added</strong>—A user added a variation to the product. The variation ID, as well as the varying attributes, also appear in the Change Type column. </li><li><strong>Variation Deleted</strong>—A user deleted product variation. The variation ID, as well as the varying attributes, also appear in the Change Type column.</li></ul> |
| Product/Variation ID | Displays the product identifier or variation identifier for the product. If the product is an individual product, only the product ID appears. If the product is a base product, (Base) appears after the ID. If the product is a variation, the name of the variation and the varying attributes (in parentheses) appears after the ID.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Modified By          | The name of the person or application who last modified the product. API indicates the Product Admin API. For example: `jdoe` or `API (ZDIOODJi***)`. Where `jdoe` is the Global Commerce username and  `ZDIOODJi***` is the first 8 digits of the API key for a Product Admin API request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Modified On          | The date and time when the product was last modified.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

## Adding or updating a product's locale

You can localize your products so that shoppers see product information in their native language, date format, time format, and currency. You can also localize themes and styles to create a look and feel for a specific locale or region.

A locale is a designator that combines the two-letter [ISO 639-1](https://en.wikipedia.org/wiki/ISO\_639-1) language code with the [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code (such as `en-US`). For example, `en_GB` represents the English language and the country of Great Britain.&#x20;

You can choose the locales you want to support when you create or update a product. You can configure a product to use a specific locale and then enter localized content for that product. When choosing locales, note the following:

* When you enter text for the product in the default locale, the same text appears for all supported locales until you either "override" or "specify" the default in a specific locale folder. You can override the default locales by adding a product variation after creating a base product. Or you can specify the default locales when you create a base product and its product variations at the same time. Changing the default locale for the product does not affect the global default locale settings in your store.
* You can provide localized content for a product. An object appears for each supported locale where you can enter the localized information. <mark style="background-color:orange;">??? What kind of object? Localizations? ???</mark> You do not have to enter localized content for all supported locales.
* By default, shoppers can purchase products in any locale (within any defined export controls). You should restrict the purchasing products to only supported locales. See [Limiting purchases to supported locales](https://help.digitalriver.com/internal-help/gc/Products/All-Products/About-localized-products.htm?Highlight=base%20product#Limit) for more information.

Ideally, you should localize a product when you first create it. However, you can localize a product after you create and deploy it to your store. If the fields and options on a locale tab are disabled in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), the supported locale uses the default locale setting. See [Overriding the default locale](https://help.digitalriver.com/internal-help/gc/Products/All-Products/About-localized-products.htm?Highlight=base%20product#Override) for more information.

The following `POST /products/{productid}` request updates an existing product. You must provide either a [`productId`](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier) or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid).

{% tabs %}
{% tab title="productId request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{productId}' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{ERID}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

Add new attributes and/or replace locale attributes in the payload. For example, you can add or replace locales for a product variation in the payload.

{% hint style="info" %}
Replace the product's current locales by adding new locales in the payload. For example, if the current locale is `zh_TW` and you include `en_US`, `en_GB`, and `ja_JP` in the payload, the locales will change to `en_US`, `en_GB`, and `ja_JP`.
{% endhint %}

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
  "localizations": [
    {
      "locale": "en_US",
      "isDefault": "true",
      "groups": [
        {
          "groupId": "ignored",
          "groupName": "ignored",
          "attributes": {
            "displayName": "display-name-{{defaultLocale}}-updated-{{baseProductId}}"
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

The request returns a task identifier (`taskId`) in the response.&#x20;

{% tabs %}
{% tab title="202 Accepted Response" %}
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
{% endtab %}
{% endtabs %}

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md). You can also verify an updated locale in Global Commerce. <mark style="background-color:orange;">??? Add task for verifying the updated locale in Global Commerce. Note that there may be a delay before these chances in Global Commerce.  ???</mark>

## Key attributes

The following details describe the key attributes when creating or updating a product. For a complete list, refer to the <mark style="background-color:orange;">??? add links to creating and updating a product ???</mark> in the API Reference document.

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

The changed attributes under this object will go live immediately. You do not need to deploy these changes. You can use these attributes to insert live changes when creating a product. After creating the product, the fields are read-only. You can apply live changes by using the POST /products/{productId}/live-changes API. This object is available with when you update a product. This object includes the following attributes:

#### externalReferenceId

The external reference identifier. A unique identifier for the product from the Digital River client.

#### catalogs

The collection of products for sale on your site. A catalog contains categories to organize your products.

* **calalogId**: The catalog identifier.
* **categories**: Categories are used to organize products within a catalog and often appear on the store to help shoppers locate products and navigate the store/site.
  * **categoryId**: The category identifier.\\
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
        * **downloadFulfillment**: The download fulfillment type. This attribute is required when you are creating a digital product. The valid values are `digitalRiver` or `thirdParty`. If you don't provide this attribute when you create or update a product, the default value is `digitalRiver`.

### variations

Different variations of the product. Only required for a base product. This attribute is available when you create a base product.

#### varyingAttributes

These attributes distinguish the product variation from the base product.

* **attributeName**: <mark style="background-color:orange;">??? How do we want to talk about the</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`attributeName`</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">and</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`attributeValue`</mark><mark style="background-color:orange;">? Are they customizable. Can you provide examples? ???</mark>
* **attributeValue**:

#### [deploymentRequiredChanges](creating-or-updating-a-product.md#deploymentrequiredchanges)

#### [liveChanges](creating-or-updating-a-product.md#livechanges)

#### [Localizations](creating-or-updating-a-product.md#localizations)
