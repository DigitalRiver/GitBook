---
description: Learn how to retire a product programmatically.
---

# Retiring a product

You can retire a base or individual product when you no longer need it. However, you cannot delete them. You can only [delete product variations](deleting-a-product-variation.md) associated with a base product.

You can find a retired product by sending a [`GET /v1/products/{productId or ERID}`](../retrieve-products-synchronous-api/getting-a-base-or-individual-product.md) ?version=RETIRED request or [searching for the retired product](https://help.digitalriver.com/help/gc/Products/All-Products/Editing-a-product.htm#HowToSearchForProduct) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). The shoppers visiting your store cannot see or purchase the retired product.&#x20;

{% hint style="info" %}
Here are a few notes regarding retired products:

* The retired product remains in your catalog, where you can [get the product's attributes](../retrieve-products-synchronous-api/getting-a-base-or-individual-product.md). You can use the attributes in the response to [create](creating-or-updating-a-product.md) and [deploy a new product](deploying-a-product.md) with similar details. If you edit a retired product, it goes into a design state where you can apply the change and then deploy the updated product.&#x20;
* [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) does not maintain the stock status for a retired product. Therefore, it does not display the current inventory number for the retired product.
{% endhint %}

The following [`POST /v1/products/{productId or ERID}/retire`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BproductId%7D\~1retire/post) request retires the specified product. To retire a specific product, you must provide either a  [`productId`](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md) or [`ERID`](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md).&#x20;

{% hint style="info" %}
Duplicate ERIDs are not allowed. To prevent duplicate ERIDs, [enable the Enforce Unique Value](../../../general-resources/common-shoppers-and-admin-apis-reference/external-reference-identifier-erid.md#enabling-the-enforce-unique-value) when [configuring company settings](https://help.digitalriver.com/internal-help/gc/Administration/Company/Configuring-company-settings.htm) in Global Commerce. This ensures that you won't accidentally provide an ERID that would result in duplicate products in the response if you searched for a product by ERID.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
The following example retires a specific product with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{productID}/retire' \
--header 'Authorization: Basic <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{ERID}/retire' \
--header 'Authorization: Basic <API_key>' \
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
    "taskId": "4ea32c9b-2019-4421-863c-1acfb794033c",
    "requestType": "RETIRE_PRODUCT",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-08-24T19:31:56.434Z"
}
```
{% endcode %}

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/getting-the-latest-information-on-a-product-task.md). You can also verify the successful completion of the task by [checking the product history](retiring-a-product.md#product-history-attributes) in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). Note that there may be a delay before these changes appear in Global Commerce.&#x20;
{% endtab %}
{% endtabs %}

## Verifying the retirement of a product in Global Commerce

When you retire an individual or base product, that product will be marked as retired in Global Commerce.

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and choose **ID** from the **Search By** dropdown list. Enter the product identifier or ERID in the **Search For** field, then click **Search**.
4. Click the link for the product under the **Internal Product Name column**. The Edit Product page appears, and **(Retired)** will appear after the product name at the top of the page.
