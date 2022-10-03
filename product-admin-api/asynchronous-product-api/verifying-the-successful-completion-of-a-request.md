---
description: Learn how to get a task identifier.
---

# Verifying the successful completion of a request

The Product Admin API sends asynchronous API requests to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). When Global Commerce receives the [create or update product request](creating-or-updating-a-product.md), it returns the task identifier (`taskId`) in the response and puts the request in a queue. This allows you to send multiple requests in a small timeframe without waiting for the request to complete or worrying about timeouts. Most products will complete successfully within a few seconds. However, creating or updating a base product with multiple variations and locales without limiting the number of variations and locales will take longer to complete the creation or update process. For example, creating a base product with 10 variations and 55 locales will take 30 seconds to a minute to complete. You can use the `taskId` to get the current status of the task.

## Verifying the successful completion of multiple products

The following `GET /products/tasks/{taskId}` request tells you whether the [create or update product request](creating-or-updating-a-product.md) was successful. This request requires the task identifier (`taskId`) provided in the response when you created or updated the product.

&#x20;<mark style="background-color:orange;">??? Add a link to the GET request. ???</mark>

{% tabs %}
{% tab title="Request" %}
{% code overflow="wrap" %}
```
curl --location --request GET 'https://api.digitalriver.com/products/tasks/{taskId}'
' \
--header 'Authorization: Bearer <API_key>' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You cannot [change or modify a product](verifying-the-successful-completion-of-a-request.md#updating-a-product) until the [create product request](verifying-the-successful-completion-of-a-request.md#creating-a-base-or-individual-product) completes successfully.
{% endhint %}

The request returns the product data associated with  the task identifier (`taskId`) in the response. The possible request types are `CREATE_PRODUCT`, `CREATE_VARIATION`, `UPDATE_PRODUCT`, `UPDATE_VARIATION`, `DELETE_VARIATION`, `DELETE_LOCALE`, `DEPLOY_PRODUCT`, `RETIRE_PRODUCT`, `UPDATE_PRODUCT_LIVE_CHANGE`, and `UPDATE_VARIATION_LIVE_CHANGE`.

{% tabs %}
{% tab title="200 OK Response" %}
{% code overflow="wrap" %}
```json
{
    "taskId": "ea310126-cba4-46be-9cff-82dded915dbf",
    "products": [
        {
            "id": "50792700080",
            "externalReferenceId": "47f3e694-f638-4263-b97d-f0f921ae20d3",
            "productType": "BASE"
        },
        {
            "id": "50792710080",
            "externalReferenceId": "9f00245b-ccfa-4ca0-805b-13d01b685dfb",
            "productType": "VARIATION"
        },
        {
            "id": "50792720080",
            "externalReferenceId": "43c0d80d-82fe-418f-ad57-0a8688bd7c2f",
            "productType": "VARIATION"
        }
    ],
    "requestType": "CREATE_PRODUCT",
    "taskStatus": "COMPLETED",
    "receivedTime": "2022-08-11T16:32:26.547Z",
    "finishedTime": "2022-08-11T16:32:31.185Z"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

## Verifying the successful completion of a specific product

The following `GET /product/tasks?productId={productId or ERID}` request indicates whether the [create or update product request](creating-or-updating-a-product.md) for a specific product was successful. You must provide either a [`productId` ](../administrator-browser-experience/product-basics/unique-product-identifier.md#product-identifier)or [`ERID`](../administrator-browser-experience/product-basics/unique-product-identifier.md#external-reference-identifier-erid).  <mark style="background-color:orange;">??? Add a link to the GET request. ???</mark>

{% tabs %}
{% tab title="productId request" %}
{% code overflow="wrap" %}
```http
curl --location --request 
POST 'https://api.digitalriver.com/product/tasks?productId={productId}'
```
{% endcode %}
{% endtab %}

{% tab title="ERID request" %}
{% code overflow="wrap" %}
```http
curl --location --request 
POST 'https://api.digitalriver.com/product/tasks?productId=50432680080'
--header 'header x-erid-as-pid=true' \
```
{% endcode %}
{% endtab %}
{% endtabs %}

The request returns the product data associated with  the task identifier (`taskId`) in the response. <mark style="background-color:orange;">??? Verify the following example is correct. ???</mark>

{% tabs %}
{% tab title="200 OK Response" %}
{% code overflow="wrap" %}
```json
{
    "tasks": [
        {
            "taskId": "49751317-ff82-4638-8bf1-de5d7eb4ebdb",
            "products": [
                {
                    "id": "50432680080",
                    "externalReferenceId": "d02e9e41-4d54-4e68-a696-3048adb485e7",
                    "productType": "BASE"
                },
                {
                    "id": "50432690080",
                    "externalReferenceId": "b0dfc13e-284b-4d98-a835-73ee15c37448",
                    "productType": "VARIATION"
                },
                {
                    "id": "50432700080",
                    "externalReferenceId": "31c644e5-0b40-45a6-bd95-955acf6cbc5f",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-08-23T20:15:47.449Z",
            "finishedTime": "2022-08-23T20:15:53.037Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/49751317-ff82-4638-8bf1-de5d7eb4ebdb"
        },
        {
            "taskId": "b3c006fd-b7b8-4d91-932c-ca6da7f71f1f",
            "products": [
                {
                    "id": "50432680080",
                    "externalReferenceId": "d02e9e41-4d54-4e68-a696-3048adb485e7",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-08-23T20:17:19.827Z",
            "finishedTime": "2022-08-23T20:17:20.584Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/b3c006fd-b7b8-4d91-932c-ca6da7f71f1f"
        },
        {
            "taskId": "754a4d49-6e07-4d44-87da-8288d7075718",
            "products": [
                {
                    "id": "50432680080",
                    "externalReferenceId": "d02e9e41-4d54-4e68-a696-3048adb485e7",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-08-23T20:58:57.726Z",
            "finishedTime": "2022-08-23T20:58:58.125Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/754a4d49-6e07-4d44-87da-8288d7075718"
        },
        {
            "taskId": "80f1e1eb-4144-4030-82cd-f3817d8cc0f9",
            "products": [
                {
                    "id": "50505980080",
                    "externalReferenceId": "3f29d287-f6c9-4c82-ac4c-452af405333a",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-08-24T16:13:12.575Z",
            "finishedTime": "2022-08-24T16:13:14.763Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/80f1e1eb-4144-4030-82cd-f3817d8cc0f9"
        }
    ],
    "totalSize": 4,
    "searchCriteria": {
        "beginReceivedTime": "2022-07-25T17:29:22.050Z",
        "endReceivedTime": "2022-08-24T17:29:22.050Z",
        "productId": "50432680080",
        "taskStatus": [
            "COMPLETED",
            "FAILED",
            "PROCESSING",
            "PUBLISHED"
        ]
    },
    "pagination": {
        "limit": 50
    }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
