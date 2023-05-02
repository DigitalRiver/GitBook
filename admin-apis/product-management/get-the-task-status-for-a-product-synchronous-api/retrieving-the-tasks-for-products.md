---
description: Learn how to retrieve the tasks for products.
---

# Retrieving the tasks for products

## Retrieving the tasks for all products

The following [`GET /v1/products/tasks`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Get-Product-Task-Status-\(Synchronous-API\)/paths/\~1v1\~1products\~1tasks\~1/get)  request retrieves all tasks. You can use [query parameters](../../../general-resources/admin-apis-reference/tasks.md#tasks-query-parameters) to filter the results.&#x20;

{% tabs %}
{% tab title="tasks cURL" %}
The following example retrieves the tasks for all products.&#x20;

{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/tasks' \
--header 'Authorization: Basic Basic <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The request returns the [product data](../../../general-resources/admin-apis-reference/tasks.md#products), the [task identifier (`taskId`)](../../../general-resources/admin-apis-reference/tasks.md#task-identifier), the [request type (`requestType`)](../../../general-resources/admin-apis-reference/tasks.md#request-type), and [task status (`taskStatus`)](../../../general-resources/admin-apis-reference/tasks.md#task-status) for all products in the [synchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.

{% code overflow="wrap" %}
```json
{
    "tasks": [
        {
            "taskId": "147a8ac0-7f11-496b-a5d7-72007c88fb05",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "PUBLISHED",
            "receivedTime": "2022-11-04T02:31:28.427Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/147a8ac0-7f11-496b-a5d7-72007c88fb05"
        },
        {
            "taskId": "a7bdd623-9521-44cb-b55b-a98de0a76ebe",
            "products": [
                {
                    "id": "51473680080",
                    "externalReferenceId": "external-reference-id-ebda949f-2018-4cde-b9b3-7dbab294f5f9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:36:55.361Z",
            "finishedTime": "2022-11-04T02:36:56.580Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/a7bdd623-9521-44cb-b55b-a98de0a76ebe"
        },
        {
            "taskId": "1a85d25f-88de-47e0-ba2c-daf271ec8ee1",
            "products": [
                {
                    "id": "51473680080",
                    "externalReferenceId": "external-reference-id-ebda949f-2018-4cde-b9b3-7dbab294f5f9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:38:12.655Z",
            "finishedTime": "2022-11-04T02:38:13.046Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/1a85d25f-88de-47e0-ba2c-daf271ec8ee1"
        },
        {
            "taskId": "249c0cfa-ea07-4737-ab48-4e383d97f781",
            "products": [
                {
                    "id": "51473680080",
                    "externalReferenceId": "external-reference-id-ebda949f-2018-4cde-b9b3-7dbab294f5f9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "RETIRE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:38:52.529Z",
            "finishedTime": "2022-11-04T02:38:52.970Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/249c0cfa-ea07-4737-ab48-4e383d97f781"
        },
        {
            "taskId": "70227cbb-3900-4756-a181-b5d1034e21fc",
            "products": [
                {
                    "id": "51473680080",
                    "externalReferenceId": "external-reference-id-ebda949f-2018-4cde-b9b3-7dbab294f5f9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:38:59.768Z",
            "finishedTime": "2022-11-04T02:39:00.335Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/70227cbb-3900-4756-a181-b5d1034e21fc"
        },
        {
            "taskId": "a6bccbf5-96ae-46fc-8bbf-21c46399d02b",
            "products": [
                {
                    "id": "51473680080",
                    "externalReferenceId": "123xt456ernal-reference-id-ebda949f-2018-4cde-b9b3-7dbab294f5f9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:39:13.554Z",
            "finishedTime": "2022-11-04T02:39:15.838Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/a6bccbf5-96ae-46fc-8bbf-21c46399d02b"
        },
        {
            "taskId": "a3362e04-25a9-47fe-80d3-661c30d6511d",
            "products": [
                {
                    "id": "51473680080",
                    "externalReferenceId": "123xt456ernal-reference-id-ebda949f-2018-4cde-b9b3-7dbab294f5f9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DELETE_LOCALE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-11-04T02:39:58.490Z",
            "finishedTime": "2022-11-04T02:39:58.808Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/a3362e04-25a9-47fe-80d3-661c30d6511d"
        },
        {
            "taskId": "b68de590-2e09-483d-8744-eb4582d3323f",
            "products": [
                {
                    "id": "51656880080",
                    "externalReferenceId": "BASE_ERID_4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "BASE"
                },
                {
                    "id": "51656890080",
                    "externalReferenceId": "Variation_ERID_4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:40:31.971Z",
            "finishedTime": "2022-11-04T02:40:32.763Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/b68de590-2e09-483d-8744-eb4582d3323f"
        },
        {
            "taskId": "ad7d91f7-0886-43a3-8722-aa3dfa063387",
            "products": [
                {
                    "id": "51656880080",
                    "externalReferenceId": "BASE_ERID_4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:42:11.583Z",
            "finishedTime": "2022-11-04T02:42:12.439Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ad7d91f7-0886-43a3-8722-aa3dfa063387"
        },
        {
            "taskId": "b65ed7f9-0c0b-4be1-bd79-0670e6fdb1c1",
            "products": [
                {
                    "id": "51656880080",
                    "externalReferenceId": "BASE_ERID_4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:42:31.791Z",
            "finishedTime": "2022-11-04T02:42:32.094Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/b65ed7f9-0c0b-4be1-bd79-0670e6fdb1c1"
        },
        {
            "taskId": "b828619c-976e-4695-964c-a4a222d5437a",
            "products": [
                {
                    "id": "51656880080",
                    "externalReferenceId": "Update_Base_By_ERID-4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:43:22.000Z",
            "finishedTime": "2022-11-04T02:43:22.501Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/b828619c-976e-4695-964c-a4a222d5437a"
        },
        {
            "taskId": "0c1e17e4-ac29-436c-983f-41c8419cdf07",
            "products": [
                {
                    "id": "51644720080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:43:43.744Z",
            "finishedTime": "2022-11-04T02:43:44.070Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/0c1e17e4-ac29-436c-983f-41c8419cdf07"
        },
        {
            "taskId": "e5484a58-5feb-4e32-bbc1-4ca400547a3e",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-11-04T02:45:31.633Z",
            "finishedTime": "2022-11-04T02:45:31.927Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/e5484a58-5feb-4e32-bbc1-4ca400547a3e"
        },
        {
            "taskId": "58e8a550-069c-47df-93c1-2754cb8cd803",
            "products": [
                {
                    "id": "51656880080",
                    "externalReferenceId": "Update_Base_By_ERID-4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:45:44.383Z",
            "finishedTime": "2022-11-04T02:45:44.630Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/58e8a550-069c-47df-93c1-2754cb8cd803"
        },
        {
            "taskId": "4789dcc9-2b17-494e-ba09-38b47245a1a8",
            "products": [
                {
                    "id": "51656890080",
                    "externalReferenceId": "Variation_ERID_4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:46:11.858Z",
            "finishedTime": "2022-11-04T02:46:12.400Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/4789dcc9-2b17-494e-ba09-38b47245a1a8"
        },
        {
            "taskId": "a61a962f-75e8-4fa9-be0d-d98bda58b2e6",
            "products": [
                {
                    "id": "51656890080",
                    "externalReferenceId": "Variation_ERID_4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:46:24.900Z",
            "finishedTime": "2022-11-04T02:46:25.241Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/a61a962f-75e8-4fa9-be0d-d98bda58b2e6"
        },
        {
            "taskId": "7dd9483d-3615-4e84-ab07-cd464890ff0d",
            "products": [
                {
                    "id": "51656890080",
                    "externalReferenceId": "UpdateVariation2-4c07253a-7a1a-4ae2-9fbf-a9462ab4aeb6",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:46:49.188Z",
            "finishedTime": "2022-11-04T02:46:49.420Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7dd9483d-3615-4e84-ab07-cd464890ff0d"
        },
        {
            "taskId": "b1e9cb30-0555-4e33-a052-9bd7142d5665",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-11-04T02:49:04.742Z",
            "finishedTime": "2022-11-04T02:49:05.171Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/b1e9cb30-0555-4e33-a052-9bd7142d5665"
        },
        {
            "taskId": "714bc570-fdca-415e-b0a4-83ca8afcc58c",
            "products": [
                {
                    "id": "51635860080",
                    "externalReferenceId": "BASE_ERID_ef7626c3-92a5-4032-8c82-16ba901d9ab7",
                    "productType": "BASE"
                },
                {
                    "id": "51635870080",
                    "externalReferenceId": "Variation_ERID_ef7626c3-92a5-4032-8c82-16ba901d9ab7",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:49:14.019Z",
            "finishedTime": "2022-11-04T02:49:14.494Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/714bc570-fdca-415e-b0a4-83ca8afcc58c"
        },
        {
            "taskId": "f55a936f-751f-48a0-857f-1272f5ebb6d2",
            "products": [
                {
                    "id": "51658020080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:49:23.168Z",
            "finishedTime": "2022-11-04T02:49:23.350Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f55a936f-751f-48a0-857f-1272f5ebb6d2"
        },
        {
            "taskId": "17949da0-eaa0-480a-9bc6-bcdd0ed389cf",
            "products": [
                {
                    "id": "51635870080",
                    "externalReferenceId": "Variation_ERID_ef7626c3-92a5-4032-8c82-16ba901d9ab7",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "DELETE_VARIATION",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-04T02:50:28.137Z",
            "finishedTime": "2022-11-04T02:50:28.368Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/17949da0-eaa0-480a-9bc6-bcdd0ed389cf"
        },
        {
            "taskId": "f906e297-2275-4411-80d4-99b84c80ec69",
            "products": [
                {
                    "id": "51954990080",
                    "externalReferenceId": "external-reference-id-f7f6dcdc-a9dd-47c6-97fd-ffb340bcd399",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-11-28T13:43:59.692Z",
            "finishedTime": "2022-11-28T13:44:02.925Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f906e297-2275-4411-80d4-99b84c80ec69"
        }
    ],
    "totalSize": 22,
    "searchCriteria": {
        "beginReceivedTime": "2022-10-29T14:43:20.524Z",
        "endReceivedTime": "2022-11-28T14:43:20.524Z",
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

## Retrieving product tasks by status

To [retrieve a task by status](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Get-Product-Task-Status-\(Synchronous-API\)/paths/\~1v1\~1products\~1tasks\~1/get), use the [`taskStatus` query parameter](../../../general-resources/admin-apis-reference/tasks.md#taskstatus). See [Tasks query parameters](../../../general-resources/admin-apis-reference/tasks.md#tasks-query-parameters) for more information on the available query parameters.

{% tabs %}
{% tab title="cURL" %}
The following example gets all completed product tasks between 8 am and noon on March 6th, 2023

{% code overflow="wrap" %}
```html
curl --location --request GET 'https://api.digitalriver.com/v1/products/tasks?taskStatus=COMPLETED'?beginReceivedTime='2023-03-06T00:08:00.000Z?endReceivedTime='2023-03-06T12:00:00.000Z' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
````json

{
    "tasks": [
        {
            "taskId": "8baaf19d-31e5-4f94-9599-5cf379d4183d",
            "products": [
                {
                    "id": "52331470080",
                    "externalReferenceId": "external-reference-id-60e4661a-b6f5-49d2-9407-fcc41b57d147",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2023-03-06T04:29:48.179Z",
            "finishedTime": "2023-03-06T04:29:49.360Z",
            "uri": "https://dispatch-test.digitalriver.com/v1/products/tasks/8baaf19d-31e5-4f94-9599-5cf379d4183d"
        },
        {
            "taskId": "2717f937-b300-4690-8d8a-5523c9df239f",
            "products": [
                {
                    "id": "52331470080",
                    "externalReferenceId": "external-reference-id-60e4661a-b6f5-49d2-9407-fcc41b57d147",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2023-03-06T04:30:03.820Z",
            "finishedTime": "2023-03-06T04:30:04.370Z",
            "uri": "https://dispatch-test.digitalriver.com/v1/products/tasks/2717f937-b300-4690-8d8a-5523c9df239f"
        },
        {
            "taskId": "dc85a3db-1f97-4c37-acf7-5be6722bcffd",
            "products": [
                {
                    "id": "52331470080",
                    "externalReferenceId": "123xt456ernal-reference-id-60e4661a-b6f5-49d2-9407-fcc41b57d147",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2023-03-06T04:30:08.185Z",
            "finishedTime": "2023-03-06T04:30:08.369Z",
            "uri": "https://dispatch-test.digitalriver.com/v1/products/tasks/dc85a3db-1f97-4c37-acf7-5be6722bcffd"
        },
        {
            "taskId": "83431602-fca9-42ad-8c55-719de1f55424",
            "products": [
                {
                    "id": "52331470080",
                    "externalReferenceId": "external-reference-id-60e4661a-b6f5-49d2-9407-fcc41b57d147",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2023-03-06T04:30:09.251Z",
            "finishedTime": "2023-03-06T04:30:09.471Z",
            "uri": "https://dispatch-test.digitalriver.com/v1/products/tasks/83431602-fca9-42ad-8c55-719de1f55424"
        },
        {
            "taskId": "adf0df9b-0c68-486d-b6bb-ee2664609c7d",
            "products": [
                {
                    "id": "52331470080",
                    "externalReferenceId": "123xt456ernal-reference-id-60e4661a-b6f5-49d2-9407-fcc41b57d147",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "RETIRE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2023-03-07T04:30:10.205Z",
            "finishedTime": "2023-03-07T04:30:10.302Z",
            "uri": "https://dispatch-test.digitalriver.com/v1/products/tasks/adf0df9b-0c68-486d-b6bb-ee2664609c7d"
        },
    ],
    "totalSize": 5,
    "searchCriteria": {
        "beginReceivedTime": "2023-03-06T00:00:00.000Z",
        "endReceivedTime": "2023-03-06T09:15:55.346Z",
        "taskStatus": [
            "COMPLETED"
        ]
    },
    "pagination": {
        "limit": 50
    }
}
```
````
{% endcode %}
{% endtab %}
{% endtabs %}
