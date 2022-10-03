---
description: Learn how to retire a product programmatically.
---

# Retiring a product

You can retire a base or individual product when you no longer need it. However, you cannot delete them. You can only [delete product variations](deleting-a-product-variation.md) associated with a base product.

Once retired, you can still search for the retired product by using `GET /products/{productId}` request or within [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). The shoppers visiting your store cannot see or purchase the retired product. <mark style="background-color:orange;">??? Is the statement about searching for a retired product in Global Commerce still true in this instance? ???</mark>

{% hint style="info" %}
Here are a few notes regarding retired products:

* You cannot edit a retired product. The retired product remains in your catalog where you can [get the product's attributes](broken-reference). You can use the attributes in the response to [create ](creating-or-updating-a-product.md#creating-an-individual-or-base-product)and [deploy a new product](deploying-a-product.md) with similar details.
* [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) does not maintain the stock status for a retired product. Therefore, it does not display the current inventory number for the retired product. <mark style="background-color:orange;">??? Is this still a valid statement? ???</mark>
{% endhint %}

The following `POST /products/{productId or ERID}/retire` request retires the specified product. <mark style="background-color:orange;">??? TODO: Add a link to the POST request. ???</mark>

To retire a specific product, you must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-and-the-shopper-resource). If the request finds multiple products associated with the `ERID`, the response will return all of them.

{% tabs %}
{% tab title="productId request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{productID}/retire' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
```
curl --location --request POST 'https://api.digitalriver.com/products/{ERID}/retire' \
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
    "taskId": "4ea32c9b-2019-4421-863c-1acfb794033c",
    "requestType": "RETIRE_PRODUCT",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-08-24T19:31:56.434Z"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md).



### Verifying the retirement of a product in Global Commerce

When you retire an individual or base product, that product will be marked as retired in Global Commerce.

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID in the **Search For** field, and then click **Search**.
4. Click the link for the product under the **Internal Product Name column**. The Edit Product page appears and **(Retired)** will appear after the product name at the top of the page.

