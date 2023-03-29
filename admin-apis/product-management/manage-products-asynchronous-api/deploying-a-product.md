---
description: Learn how to deploy a product programmatically.
---

# Deploying a product

The following [`POST /v1/products/{productId or ERID}/deploy`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Manage-Product-\(Asynchronous-API\)/paths/\~1v1\~1products\~1%7BproductId%7D\~1deploy/post) request deploys the specified product.  Note that you can only deploy an individual or base product. If the product is already retired, the response will return an error. To deploy a specific product, you must provide either a [`productId` ](../../../general-resources/common-shoppers-and-admin-apis-reference/product-identifier.md)or [`ERID`](deploying-a-product.md#externalreferenceid).&#x20;

{% tabs %}
{% tab title="cURL" %}
The following example deploys a product with a `productId`.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{productId}/deploy' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request POST 'https://api.digitalriver.com/v1/products/{productId}/deploy' \
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
    "taskId": "c714a17d-64f7-4ca5-810c-b4123b3083fa",
    "requestType": "DEPLOY_PRODUCT",
    "taskStatus": "PUBLISHED",
    "receivedTime": "2022-11-28T17:19:40.610Z"
}
```
{% endcode %}

Use the `taskId` in the response to [verify the successful completion of the request](../get-the-task-status-for-a-product-synchronous-api/).
{% endtab %}
{% endtabs %}

There are two ways to verify the deployment of an individual or base product. You can either [verify the product is marked as deployed in Global Commerce](deploying-a-product.md#verifying-the-deployment-of-a-product-in-global-commerce), or you can [get the deployed product](../retrieve-products-synchronous-api/getting-a-base-or-individual-product.md#getting-the-deployed-or-retired-versions-of-a-product).

## Verifying the deployment of a product in Global Commerce

1. Sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do).
2. Select **Catalog**, select **Products**, and then click **Manage Products**. The Products page appears.
3. Click the **Search** tab, select **Product** from the **Search In** dropdown list, and select **ID** from the **Search By** dropdown list. Enter the product identifier or ERID in the **Search For** field, and then click **Search**.
4. Click the link for the product under the **Internal Product Name column**. The Edit Product page appears and **(Deployed)** will appear after the product name at the top of the page.

##
