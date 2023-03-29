---
description: Learn how to delete a product programmatically.
---

# Deleting a product variation

{% hint style="info" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response. You cannot delete a base or individual product. To make a base or individual product unavailable to the shopper, you must [retire the product](retiring-a-product.md). However, you can delete a [product variation](../../../general-resources/admin-apis-reference/products.md#product-variations) or [locale](deleting-a-base-or-individual-products-locale.md).&#x20;
{% endhint %}

## Deleting a specific product variation

The following [`DELETE /v1/products/variations/{variationProductId or variationERID}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BbaseProductId%7D\~1variations\~1%7BvariationId%7D/delete) request deletes the specified product variation. To delete a product variation for a specific base product, you must provide the  `variationProductId` or `variationERID`. If the request finds multiple products associated with the `variationERID`, the response will delete all of them.&#x20;

{% hint style="info" %}
Duplicate ERIDs are not allowed. To prevent duplicate ERIDs, [enable the Enforce Unique Value](broken-reference) when [configuring company settings](https://help.digitalriver.com/internal-help/gc/Administration/Company/Configuring-company-settings.htm) in Global Commerce. This ensures that you won't accidentally provide an ERID that would result in duplicate products in the response if you searched for a product by ERID.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
The following example deletes a specific product variation with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request DELETE 'https://api.digitalriver.com/v1/products/variations/{variationProductId}' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```
curl --location --request DELETE 'https://api.digitalriver.com/v1/products//variations/{variationERID}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

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

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/).
{% endtab %}
{% endtabs %}

## Verifying the deletion of a product variation in Global Commerce

When you delete a product variation, that product variation will no longer appear associated with the base product in Global Commerce.

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID for the base product in the **Search For** field, and then click **Search**.
4. Click the link for the base product under the **Internal Product Name column**. The Edit Product page appears.
5. Click the **Details** tab and verify the deleted product variation no longer appears under the **Choose a Product** column.
