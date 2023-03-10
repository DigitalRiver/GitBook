---
description: Lear how retrieve the tasks for a specific product.
---

# Retrieving the tasks for a specific product

The response to the following [`GET /v1/products/tasks?productId={productId or ERID}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Get-Product-Task-Status-\(Synchronous-API\)/paths/\~1products\~1tasks\~1/get) request retrieves the tasks for a specific `productId` or `ERID`.&#x20;

{% tabs %}
{% tab title="cURL" %}
The following example verifies the completion of  a product for a specific [`productId`](../../../general-resources/admin-apis-reference/tasks.md#product-identifier).&#x20;

{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/tasks?productId={productId}'
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}

An ERID request requires the `x-erid-as-pid=true` header.

{% code overflow="wrap" %}
```http
curl --location --request 
POST 'https://api.digitalriver.com/v1/products/tasks?productId={ERID}'
--header 'Authorization: Bearer <API_key>' \
--header 'header x-erid-as-pid=true' \
...
```
{% endcode %}

To filter the results in the response, use [query parameters](../../../general-resources/admin-apis-reference/tasks.md#tasks-query-parameters).
{% endtab %}

{% tab title="200 OK Response" %}
The request returns the [product data](../../../general-resources/admin-apis-reference/tasks.md#products), the [task identifier (`taskId`)](../../../general-resources/admin-apis-reference/tasks.md#task-identifier), the [request type (`requestType`)](../../../general-resources/admin-apis-reference/tasks.md#request-type), and [task status (`taskStatus`)](../../../general-resources/admin-apis-reference/tasks.md#task-status) in the [synchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.&#x20;

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
