---
description: Learn how to delete a product programmatically.
---

# Deleting a product variation

{% hint style="info" %}
You cannot delete a base or individual product. To make a base or individual product unavailable to the shopper, you must [retire the product](retiring-a-product.md). However, you can delete a [product variation](deleting-a-product-variation.md) or [locale](deleting-a-base-or-individual-products-locale.md).&#x20;
{% endhint %}

The following `DELETE /products/product/variations/{variationId` or `variationERID}` request deletes the specified variation ID (`vid`). <mark style="background-color:orange;">??? TODO: Add a link to the DELETE request.???</mark>

To delete a product variation for a specific base product, you must provide the  [`variationId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md)or [ERID](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid). If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% tabs %}
{% tab title="variationId request" %}
{% code overflow="wrap" %}
```http
curl --location --request DELETE 'https://api.digitalriver.com/products/product/variations/{variationId}' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
```
curl --location --request DELETE 'https://api.digitalriver.com/products/product/variations/{variationERID}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endtab %}
{% endtabs %}

The request returns a task identifier (`taskId`) in the response.&#x20;

{% tabs %}
{% tab title="202 Accepted response" %}
{% code overflow="wrap" %}
```json
{
    "taskId": "2496da1d-4ba7-4396-880c-760b57e732ea",
    "requestType": "DELETE_VARIATION",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-08-24T19:55:51.690Z"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md).

### Verifying the deletion of a product variation in Global Commerce

When you delete a product variation, that product variation will no longer appear associated with the base product in Global Commerce.

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID for the base product in the **Search For** field, and then click **Search**.
4. Click the link for the base product under the **Internal Product Name column**. The Edit Product page appears.
5. Click the **Details** tab and verify the deleted product variation no longer appears under the **Choose a Product** column.
