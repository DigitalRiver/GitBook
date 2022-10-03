---
description: Learn how to delete locale for a base or individual product programmatically.
---

# Deleting a base or individual product's locale

When deleting a locale from an individual product or base product note that:

* You can only delete a locale from an individual or base product. You cannot delete multiple locales at the same time. When you delete a locale from a base product, you also delete that locale from all of its product variations.
* You can't delete a default locale. Attempting to do so will result in an error. To delete a default locale, you must change the default locale by [updating the product](creating-or-updating-a-product.md#updating-an-individual-or-base-product) before you can delete the original default locale.

The following `DELETE /products/{productId or ERID}/locales/{locale}` request deletes the locale from a base or individual product. <mark style="background-color:orange;">??? TODO: Add a link to the DELETE request. ???</mark>

{% hint style="info" %}
You cannot delete a locale from a product variation.
{% endhint %}

To delete a locale  for a base product or individual product, you must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-and-the-shopper-resource) and the locale (for example, `en_GB`). If the request finds multiple products associated with the `ERID`, the response will delete all of them. <mark style="background-color:orange;">??? Is this last sentence true? ???</mark>

{% tabs %}
{% tab title="ProductId request" %}
{% code overflow="wrap" %}
```http
curl --location --request DELETE 'https://api.digitalriver.com/products/{productid}/locales/en_GB' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
```
curl --location --request DELETE 'https://api.digitalriver.com/products/{ERID}/locales/en_GB' \
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

### Verifying the deletion of a product's locale in Global Commerce

When you delete a locale associated with an individual or base product, that locale will no longer appear associated with the product in Global Commerce.

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID in the **Search For** field, and then click **Search**.
4. Click the link for the product under the **Internal Product Name column**. The Edit Product page appears.
5. Click the **Details** tab and verify the deleted locale no longer appears under the **Choose a Locale** column.
