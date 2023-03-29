---
description: Learn how to apply a live change to a deployed product.
---

# Applying live changes

You can [apply live changes](applying-live-changes.md#applying-a-live-change-to-a-base-product) to [key attributes](../../../general-resources/admin-apis-reference/live-changes.md#live-changes-resource) associated with a deployed product or product variation. The following list summarizes the actions that prompt a live change to the product in your store:&#x20;

* Adding, editing, or removing a [category ](../../../general-resources/admin-apis-reference/live-changes.md#categories)assignment for a product.
* Adding, editing, or removing [pricing](../../../general-resources/admin-apis-reference/live-changes.md#prices).&#x20;

If there are any [errors or warnings](broken-reference) when you apply a live change, they will appear in the response.

## Applying a live change to a base or individual product

The following [`POST /v1/products/{productId or ERID}/live-changes`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1products\~1%7BproductId%7D\~1live-changes/post) request applies a change to a [base product](../../../general-resources/admin-apis-reference/products.md#base-product) or [individual product](../../../general-resources/admin-apis-reference/products.md#individual-product). To apply a live change to a specific base or individual product, you must provide either a [`productId` ](broken-reference)or [`ERID`](broken-reference).&#x20;

{% tabs %}
{% tab title="cURL" %}
The following example applies live changes to a product with a `productId`. See the [live-changes](../../../general-resources/admin-apis-reference/live-changes.md#live-changes-resource) resource for a description of the attributes.

<pre class="language-http" data-overflow="wrap"><code class="lang-http">curl --location --request POST 'https://api.digitalriver.com/v1/products/{productId}/live-chhanges' \
--header 'Authorization: Bearer &#x3C;API_key>' \
--data-raw '{
<strong>{
</strong>  "externalReferenceId": "sku-1234-5678-xyz",
  "catalogs": [
    {
      "catalogId": "123456000",
      "categories": [
        {
          "categoryId": "19000000"
        }
      ],
      "prices": [
        {
          "type": "listPrice",
          "prices": [
            {
              "currency": "USD",
              "locale": "en_US",
              "configuredPrice": 15.99
            }
          ]
        }
      ]
    }
  ]
}
}
</code></pre>

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{ERID}/live-changes' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
--data-raw '{
{
  "externalReferenceId": "sku-1234-5678-xyz",
  "catalogs": [
    {
      "catalogId": "123456000",
      "categories": [
        {
          "categoryId": "19000000"
        }
      ],
      "prices": [
        {
          "type": "listPrice",
          "prices": [
            {
              "currency": "USD",
              "locale": "en_US",
              "configuredPrice": 15.99
            }
          ]
        }
      ]
    }
  ]
}
}
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

{% code overflow="wrap" %}
```json
{
  "taskId": "d8a81162-aaaa-bbbb-cccc-ea513d1afa82",
  "receivedTime": "2022-05-01T23:00:21.123Z",
  "taskStatus": "PUBLISHED",
  "requestType": "CREATE_PRODUCT"
}
```
{% endcode %}

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/).
{% endtab %}
{% endtabs %}

## Applying a live change to a product variation

The following [`POST /v1/products/product/variations/{variationProductId or variationERID}/live-changes`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D\~1live-changes/post) request applies a change to a [product variation](../../../general-resources/admin-apis-reference/products.md#product-variations). To apply a live change to a specific product variation, you must provide either a [`productId`](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md).&#x20;

{% tabs %}
{% tab title="cURL" %}
The following example applies live changes to a product variation with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/product/variations/{variationProductId}/live-changes' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
    "externalReferenceId": "{newVariationProductERID}"
}
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/product/variations/{variationERID}/live-changes' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
--data-raw '{
    "externalReferenceId": "{newVariationProductERID}"
}
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted Response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

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

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/).
{% endtab %}
{% endtabs %}
