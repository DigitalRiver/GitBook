---
description: Learn how to delete locale for a base or individual product programmatically.
---

# Deleting a base or individual product's locale

When deleting a locale from an individual product or base product note that:

* You can only delete a locale from an individual or base product. You cannot delete multiple locales at the same time. When you delete a locale from a base product, you also delete that locale from all of its product variations.
* You can't delete a default locale. Attempting to do so will result in an error. To delete a default locale, you must change the default locale by [updating the product](creating-or-updating-a-product.md#adding-or-updating-a-products-locale) before you can delete the original default locale.

The following [`DELETE /v1/products/{productId or ERID}/locales/{locale}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BproductId%7D\~1locales\~1%7Blocale%7D/delete) request deletes the locale from a base or individual product.&#x20;

{% hint style="info" %}
You cannot delete a locale from a product variation.
{% endhint %}

To delete a locale  for a base product or individual product, you must provide either a [`productId`](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md) and the [`locale`](../../../general-resources/common-shoppers-and-admin-apis-reference/locale-and-currency.md) (for example, `en_GB`).&#x20;

{% hint style="info" %}
Duplicate ERIDs are not allowed. To prevent duplicate ERIDs, [enable the Enforce Unique Value](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md#enabling-the-enforce-unique-value) when [configuring company settings](https://help.digitalriver.com/internal-help/gc/Administration/Company/Configuring-company-settings.htm) in Global Commerce. This ensures that you won't accidentally provide an ERID that would result in duplicate products in the response if you searched for a product by ERID.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
The following example deletes a locale with a specific base or individual product with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request DELETE 'https://api.digitalriver.com/products/v1/{productId}/locales/{locale}' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```
curl --location --request DELETE 'https://api.digitalriver.com/v1/products/{ERID}/locales/{locale}' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
```
{% endcode %}
{% endtab %}

{% tab title="202 Accepted response" %}
The request returns a task identifier (`taskId`) in the [asynchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

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

## Verifying the deletion of a product's locale in Global Commerce

When you delete a locale associated with an individual or base product, that locale will no longer appear associated with the product in Global Commerce.

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID in the **Search For** field, and then click **Search**.
4. Click the link for the product under the **Internal Product Name column**. The Edit Product page appears.
5. Click the **Details** tab and verify the deleted locale no longer appears under the **Choose a Locale** column.
