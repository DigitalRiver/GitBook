---
description: Learn how to apply a live change to a deployed product.
---

# Applying live changes

You can [apply live changes](applying-live-changes.md#applying-a-live-change-to-a-base-product) to [key attributes](applying-live-changes.md#key-attributes) associated with a deployed product or product variation. The following list summarizes the actions that prompt a live change to the product in your store:&#x20;

* Adding or removing a [category ](applying-live-changes.md#categories)assignment for a product.
* Enabling, disabling, or modifying digital rights settings. <mark style="background-color:orange;">??? Where is the attribute for digital rights settings? I don't see it in the</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`liveChanges`</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">object. Is this planned for a later release? ???</mark>
* Adding, editing, or removing [pricing](applying-live-changes.md#prices).&#x20;
* Enabling or disabling any of the product options (also called "families") such as software, preorder, volume license pricing, subscription, trial, digital rights, and so on. <mark style="background-color:orange;">??? Where are the attributes for software, preorder, volume license pricing, subscription, trial, and digital rights? I don't see it in the</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`liveChanges`</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">object. Is this planned for a later release? ???</mark>

{% hint style="info" %}
When you apply changes to a supported locale, those changes will also trigger a live change.
{% endhint %}

If there are any [errors or warnings](../../error-codes/product-admin-api-error-format/warning-objects.md#live-change-warnings) when you apply a live change, they will appear in the response.

## Applying a live change to a base product or individual product

The following `POST /products/{productId or ERID}/live-changes` request applies a change to a [base product](../administrator-browser-experience/product-basics/product-types.md#base-product) or [individual product](../administrator-browser-experience/product-basics/product-types.md#individual-product). <mark style="background-color:orange;">??? TODO: Add a link to the POST request. ???</mark> To apply a live change to a specific base product, you must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid).

{% tabs %}
{% tab title="productId request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{baseProductId}' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{baseProductId}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following payload applies live catalog changes to a deployed product.

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
    "catalogs": [
      {
        "catalogId": "13889200",
        "categories": [
          {
            "categoryId": "55767800"
          },
          {
            "categoryId": "4834703900"
          },
          {
            "categoryId": "4834703700"
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
    "taskId": "754a4d49-6e07-4d44-87da-8288d7075718",
    "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-08-23T20:58:57.726Z"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md).

## Applying a live change to a product variation

The following `POST /products/product/variations/{variationProductId or ERID}/live-changes` request applies a change to a [product variation](../administrator-browser-experience/product-basics/product-types.md#product-variations). <mark style="background-color:orange;">??? TODO: Add a link to the POST request. ???</mark>

To apply a live change to a specific base product, you must provide either a  [`variationProductId`](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier) or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid).

{% tabs %}
{% tab title="variationProductId request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/product/variations/{variationProductId}/live-changes' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/product/variations/{variationERID}/live-changes' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

The following payload applies live catalog changes to a deployed product variation.

{% tabs %}
{% tab title="Payload" %}
{% code overflow="wrap" %}
```json
{
    "externalId": "{newVariationProductId}"
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
    "taskId": "ea310126-cba4-46be-9cff-82dded915dbf",
    "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-08-24T17:10:09.864Z"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md).

## Key attributes

The following details describe the key attributes when applying live changes. For a complete list, refer to the <mark style="background-color:orange;">??? TODO: Add links to updating live changes ???</mark> in the API Reference document.

### externalReferenceId

The external reference identifier. A unique identifier for the product from the Digital River client.

### catalogs

The collection of products for sale on your site. A catalog contains categories to organize your products.

#### calalogId

The catalog identifier.

#### categories

Categories are used to organize products within a catalog and often appear on the store to help shoppers locate products and navigate the store/site.

* **categoryId**: The category identifier.

#### prices

The price of a product by currency and locale.

* **type**: The type of the price list. Used to classify the prices in a price list. A price list type may also indicate how the price list or pricing will be used. For example, you can create an MSRP list, a subscription renewal price list, and so on.
* **prices**: The prices of a product.&#x20;
  * **currency**: A three-letter [ISO 4217](https://www.xe.com/iso4217.php) currency code.
  * **locale**: Optional. If your store supports multiple locales, your price list will contain space for you to enter pricing in currencies used by the locales supported by your store. The price you enter for a product in a currency will be used by any locale that uses the currency in which you entered the price.
  * **configuredPrice**: The configured price for the product.
