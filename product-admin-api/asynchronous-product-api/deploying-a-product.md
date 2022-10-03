---
description: Learn how to deploy a product programmatically.
---

# Deploying a product

The following `POST /products/{productId or ERID}/deploy` request deploys the specified product. <mark style="background-color:orange;">??? TODO: Add a link to the POST request. ???</mark> Note that you can only deploy an individual or base product. If the product is already retired, the response will return an error. To deploy a specific product, you must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid).&#x20;

{% tabs %}
{% tab title="productId request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{productId}/deploy' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/products/{productId}/deploy' \
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

The request returns a task identifier (`taskId`) in the response.&#x20;

{% tabs %}
{% tab title="202 Accepted request" %}
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

Use the `taskId` in the response to [verify the successful completion of the request](verifying-the-successful-completion-of-a-request.md).



### Verifying the deployment of a product in Global Commerce

When you deploy an individual or base product, that product will be marked as deployed in Global Commerce.

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID in the **Search For** field, and then click **Search**.
4. Click the link for the product under the **Internal Product Name column**. The Edit Product page appears and **(Deployed)** will appear after the product name at the top of the page.
