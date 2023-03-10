---
description: Understand the basics of tasks.
---

# Tasks

## The tasks object

### Task identifier

A `taskId` is a unique identifier. You can use this identifier to retrieve a task.&#x20;

### Products

The products object provides the product identifier (`productId`) and/or External Reference Identifier (`externalReferenceId`), and product type (`productType`). The valid product types are `INDIVIDUAL`, `BASE`, `VARIATION`.

### Task status

The `taskStatus` attribute identifies the type of status associated with the task. The valid task values are `PUBLISHED`, `COMPLETED`, `FAILED`, `PROCESSING`, `PUBLISHED`.

### Received time and finished time

A task always contains `receivedTime` and `finishedTime` fields. The `receiveTime` field indicates the date and time when the task began and the `finishedTime` field indicates when the task is completed. You can use the `beginReceivedTime` or `endReceivedTime` [query parameters](tasks.md#setting-task-query-parameters) in the URI to search for all tasks associated with a specific `receivedTime` or `finishedTime`.

### Request type

The `requestType` attribute identifies the type of request associated with the task. The valid request types are `CREATE_PRODUCT`, `CREATE_VARIATION`, `UPDATE_PRODUCT`, `UPDATE_VARIATION`, `DELETE_VARIATION`, `DELETE_LOCALE`, `DEPLOY_PRODUCT`, `RETIRE_PRODUCT`, `UPDATE_PRODUCT_LIVE_CHANGE`, and `UPDATE_VARIATION_LIVE_CHANGE`.

### URI

A `uri` is the web address for a specific task.&#x20;

## Tasks query parameters

You can specify one or more query parameters separated by an ampersand (&) to return a filtered list of tasks. The following topics describe the available query parameters for the `tasks` request. For more information on how to use query parameters, see [Fields and query parameters](../common-shoppers-and-admin-apis-reference/fields-and-expand-query-parameters.md).

### Begin received time

The `beginReceivedTime` query parameter filters a list based on the `receivedTime` field. A filter on a list based on the `receivedTime` field. The value can be a string with an ISO-8601 UTC format `optional` (for example, `yyyy-mm-ddT00:00:00.000Z`). The response displays results for 30 days starting from the specified date. The response displays results for 30 days starting from the specified date.\
\
`GET 'https://api.digitalriver.com/v1/products/tasks?beginReceivedTime=2022-10-01T00:00:00.000Z'`

#### Getting a task by `beginReceivedTime`

The following [`GET /v1/products/tasks?beginReceivedTime={yyyy-mm-ddT00:00:00.000Z}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Get-Product-Task-Status-\(Synchronous-API\)/paths/\~1products\~1tasks\~1/get) request filters tasks by the [`receivedTime`](tasks.md#received-and-finished-time) (for example, `2022-0901dT00:00:00.000Z`). The begin received time includes everything starting on the specified received time date and going forward. See [Setting the task query parameters](tasks.md#setting-task-query-parameters) for more information. &#x20;

{% tabs %}
{% tab title="beginReceivedTime cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/tasks?beginReceivedTime=2022-09-01T00:00:00.00/v10Z' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The request list the tasks by `beginReceivedTime` in the [synchronous ](../../admin-apis/product-management/getting-started.md#asynchronous-and-synchronous-calls)response

{% code overflow="wrap" %}
```json
{
    "tasks": [
        {
            "taskId": "eeacb15c-b3f8-494d-9b6f-fb4e9f4c42f7",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-19T17:22:11.415Z",
            "finishedTime": "2022-09-19T17:22:13.030Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/eeacb15c-b3f8-494d-9b6f-fb4e9f4c42f7"
        },
        {
            "taskId": "81192428-c98f-472d-99ea-fdbd79319cf8",
            "products": [
                {
                    "id": "50205470080",
                    "externalReferenceId": "external-reference-id-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:27:02.206Z",
            "finishedTime": "2022-09-20T08:27:03.833Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/81192428-c98f-472d-99ea-fdbd79319cf8"
        },
        {
            "taskId": "897391ee-941a-435b-9f54-bf97edb9fa49",
            "products": [
                {
                    "id": "50205480080",
                    "externalReferenceId": "external-reference-id-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "BASE"
                },
                {
                    "id": "50205490080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:28:17.554Z",
            "finishedTime": "2022-09-20T08:28:18.198Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/897391ee-941a-435b-9f54-bf97edb9fa49"
        },
        {
            "taskId": "42d617cc-7a35-4d44-93d5-028b26899fe2",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:28:51.100Z",
            "finishedTime": "2022-09-20T08:28:51.788Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/42d617cc-7a35-4d44-93d5-028b26899fe2"
        },
        {
            "taskId": "085e3321-a79e-4228-b612-7a6b874f2cbc",
            "products": [
                {
                    "id": "50205500080",
                    "externalReferenceId": "external-reference-id-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "BASE"
                },
                {
                    "id": "50205510080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:29:26.480Z",
            "finishedTime": "2022-09-20T08:29:26.792Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/085e3321-a79e-4228-b612-7a6b874f2cbc"
        },
        {
            "taskId": "a16cc310-a93c-47d7-800a-2cad7c7e8427",
            "products": [
                {
                    "id": "50205500080",
                    "externalReferenceId": "UpdateBasereference-id-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:29:32.829Z",
            "finishedTime": "2022-09-20T08:29:33.005Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/a16cc310-a93c-47d7-800a-2cad7c7e8427"
        },
        {
            "taskId": "ac8d32a0-ed4d-4027-b720-9c905af2ac44",
            "products": [
                {
                    "id": "50205510080",
                    "externalReferenceId": "UpdateVariation-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:29:39.530Z",
            "finishedTime": "2022-09-20T08:29:39.692Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ac8d32a0-ed4d-4027-b720-9c905af2ac44"
        },
        {
            "taskId": "f02ad711-5431-4ebc-8f92-d9f204047a64",
            "products": [
                {
                    "id": "50205480080",
                    "externalReferenceId": "UpdateVariation-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:30:12.143Z",
            "finishedTime": "2022-09-20T08:30:12.708Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f02ad711-5431-4ebc-8f92-d9f204047a64"
        },
        {
            "taskId": "5aba9cc0-9657-43d7-9cb9-8ab5df0efe34",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:30:52.462Z",
            "finishedTime": "2022-09-20T08:30:52.672Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/5aba9cc0-9657-43d7-9cb9-8ab5df0efe34"
        },
        {
            "taskId": "2102c363-c5b6-4ef0-a25b-3865be6b0af3",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:31:33.015Z",
            "finishedTime": "2022-09-20T08:31:33.364Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/2102c363-c5b6-4ef0-a25b-3865be6b0af3"
        },
        {
            "taskId": "3ba3b612-a9a2-4f38-b657-cbe7d7c6b330",
            "products": [
                {
                    "id": "50243780080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:31:49.899Z",
            "finishedTime": "2022-09-20T08:31:50.236Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/3ba3b612-a9a2-4f38-b657-cbe7d7c6b330"
        },
        {
            "taskId": "41903158-7e18-4d5e-ad75-3ad4462ddb37",
            "products": [
                {
                    "id": "50243790080",
                    "externalReferenceId": "external-reference-id-a4e2db25-3568-4933-9508-59db068bad9f",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:32:20.538Z",
            "finishedTime": "2022-09-20T08:32:21.085Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/41903158-7e18-4d5e-ad75-3ad4462ddb37"
        },
        {
            "taskId": "d7c9e5a9-0d7e-4684-bbfd-9c70c3aad449",
            "products": [
                {
                    "id": "50243800080",
                    "externalReferenceId": "external-reference-id-a4e2db25-3568-4933-9508-59db068bad9f",
                    "productType": "BASE"
                },
                {
                    "id": "50243810080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:32:33.962Z",
            "finishedTime": "2022-09-20T08:32:34.275Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/d7c9e5a9-0d7e-4684-bbfd-9c70c3aad449"
        },
        {
            "taskId": "824b98a4-d50c-462c-9ed8-05d9b8872e55",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:32:51.817Z",
            "finishedTime": "2022-09-20T08:32:52.052Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/824b98a4-d50c-462c-9ed8-05d9b8872e55"
        },
        {
            "taskId": "1d0da4e9-fb60-4f53-ade5-ce25098336a1",
            "products": [
                {
                    "id": "50205520080",
                    "externalReferenceId": "external-reference-id-a4e2db25-3568-4933-9508-59db068bad9f",
                    "productType": "BASE"
                },
                {
                    "id": "50205530080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:33:22.582Z",
            "finishedTime": "2022-09-20T08:33:23.027Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/1d0da4e9-fb60-4f53-ade5-ce25098336a1"
        },
        {
            "taskId": "b7130a34-997b-4267-995a-1f91abedaa79",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:33:53.018Z",
            "finishedTime": "2022-09-20T08:33:53.169Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/b7130a34-997b-4267-995a-1f91abedaa79"
        },
        {
            "taskId": "1a2a378a-a26f-497f-b0a8-019606ee702a",
            "products": [
                {
                    "id": "50205540080",
                    "externalReferenceId": "external-reference-id-864fa6bc-d85d-4ce8-9d37-4dcb34211caf",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:44:54.715Z",
            "finishedTime": "2022-09-20T08:44:55.116Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/1a2a378a-a26f-497f-b0a8-019606ee702a"
        },
        {
            "taskId": "382b3c3a-fd68-4edf-a9f9-fea04abad77b",
            "products": [
                {
                    "id": "50205540080",
                    "externalReferenceId": "external-reference-id-864fa6bc-d85d-4ce8-9d37-4dcb34211caf",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:45:01.633Z",
            "finishedTime": "2022-09-20T08:45:01.959Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/382b3c3a-fd68-4edf-a9f9-fea04abad77b"
        },
        {
            "taskId": "9d93801d-aede-418f-b22b-c4fe49e9594f",
            "products": [
                {
                    "id": "50205540080",
                    "externalReferenceId": "external-reference-id-864fa6bc-d85d-4ce8-9d37-4dcb34211caf",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:45:38.748Z",
            "finishedTime": "2022-09-20T08:45:38.899Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/9d93801d-aede-418f-b22b-c4fe49e9594f"
        },
        {
            "taskId": "ad78a645-23ac-4302-845d-dcd63298201f",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:46:32.746Z",
            "finishedTime": "2022-09-20T08:46:32.998Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ad78a645-23ac-4302-845d-dcd63298201f"
        },
        {
            "taskId": "7e985af6-428b-4aaf-b07f-8df7be69c34f",
            "products": [
                {
                    "id": "50205580080",
                    "externalReferenceId": "external-reference-id-6918b6ea-ee26-4475-a50b-6a7d69a67af9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:47:15.361Z",
            "finishedTime": "2022-09-20T08:47:15.853Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7e985af6-428b-4aaf-b07f-8df7be69c34f"
        },
        {
            "taskId": "4a52927e-b805-407f-b1e0-5f8f09854948",
            "products": [
                {
                    "id": "50205580080",
                    "externalReferenceId": "external-reference-id-6918b6ea-ee26-4475-a50b-6a7d69a67af9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:47:25.272Z",
            "finishedTime": "2022-09-20T08:47:25.510Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/4a52927e-b805-407f-b1e0-5f8f09854948"
        },
        {
            "taskId": "7e8a2b5b-3c52-42b6-aa38-b54563f2c607",
            "products": [
                {
                    "id": "50205590080",
                    "externalReferenceId": "external-reference-id-245f1188-48ad-4782-9df6-174d18137556",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:51:27.726Z",
            "finishedTime": "2022-09-20T08:51:28.182Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7e8a2b5b-3c52-42b6-aa38-b54563f2c607"
        },
        {
            "taskId": "673a7e51-6d42-49e5-b368-9f3e95eaf41a",
            "products": [
                {
                    "id": "50205590080",
                    "externalReferenceId": "external-reference-id-245f1188-48ad-4782-9df6-174d18137556",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:51:35.129Z",
            "finishedTime": "2022-09-20T08:51:35.468Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/673a7e51-6d42-49e5-b368-9f3e95eaf41a"
        },
        {
            "taskId": "7d840529-c4ab-4301-b9a4-566debbc2441",
            "products": [
                {
                    "id": "50205590080",
                    "externalReferenceId": "external-reference-id-245f1188-48ad-4782-9df6-174d18137556",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "RETIRE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:51:51.198Z",
            "finishedTime": "2022-09-20T08:51:51.347Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7d840529-c4ab-4301-b9a4-566debbc2441"
        },
        {
            "taskId": "e8ab9e99-1e78-4cd9-8ba0-261c91378b78",
            "products": [
                {
                    "id": "50205600080",
                    "externalReferenceId": "external-reference-id-52b3071f-7705-4311-bbb9-332c282460b2",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:52:26.762Z",
            "finishedTime": "2022-09-20T08:52:27.165Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/e8ab9e99-1e78-4cd9-8ba0-261c91378b78"
        },
        {
            "taskId": "138d1c2a-0d55-417a-b9f8-cd6a2717f70d",
            "products": [
                {
                    "id": "50205600080",
                    "externalReferenceId": "external-reference-id-52b3071f-7705-4311-bbb9-332c282460b2",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:52:33.796Z",
            "finishedTime": "2022-09-20T08:52:33.921Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/138d1c2a-0d55-417a-b9f8-cd6a2717f70d"
        },
        {
            "taskId": "432db185-e0d3-4565-a8da-220904a47ec2",
            "products": [
                {
                    "id": "50205610080",
                    "externalReferenceId": "external-reference-id-65473354-f908-4286-a22d-5eb994090ca6",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:53:01.523Z",
            "finishedTime": "2022-09-20T08:53:01.908Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/432db185-e0d3-4565-a8da-220904a47ec2"
        },
        {
            "taskId": "5cbfdd0d-3f7f-49f7-a163-4f46150989ae",
            "products": [
                {
                    "id": "50205610080",
                    "externalReferenceId": "external-reference-id-65473354-f908-4286-a22d-5eb994090ca6",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:53:19.463Z",
            "finishedTime": "2022-09-20T08:53:19.799Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/5cbfdd0d-3f7f-49f7-a163-4f46150989ae"
        },
        {
            "taskId": "8ce994fd-2cb9-45e4-ab78-71d38daa5dd9",
            "products": [
                {
                    "id": "50205610080",
                    "externalReferenceId": "external-reference-id-65473354-f908-4286-a22d-5eb994090ca6",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:53:29.140Z",
            "finishedTime": "2022-09-20T08:53:29.466Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/8ce994fd-2cb9-45e4-ab78-71d38daa5dd9"
        },
        {
            "taskId": "ea2a26b6-c0c8-4c60-856b-12cdf5773d67",
            "products": [
                {
                    "id": "50243820080",
                    "externalReferenceId": "external-reference-id-dafa9fef-df0c-4a6d-95d7-4ec56fe8f34e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:54:20.695Z",
            "finishedTime": "2022-09-20T08:54:21.031Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ea2a26b6-c0c8-4c60-856b-12cdf5773d67"
        },
        {
            "taskId": "ba2d0c03-33e2-4e9f-9836-2567d838c7b8",
            "products": [
                {
                    "id": "50243820080",
                    "externalReferenceId": "external-reference-id-dafa9fef-df0c-4a6d-95d7-4ec56fe8f34e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:54:27.140Z",
            "finishedTime": "2022-09-20T08:54:27.474Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ba2d0c03-33e2-4e9f-9836-2567d838c7b8"
        },
        {
            "taskId": "55eaf467-d892-4b01-90f0-585d8dc47ded",
            "products": [
                {
                    "id": "50243820080",
                    "externalReferenceId": "external-reference-id-dafa9fef-df0c-4a6d-95d7-4ec56fe8f34e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:54:30.839Z",
            "finishedTime": "2022-09-20T08:54:31.337Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/55eaf467-d892-4b01-90f0-585d8dc47ded"
        },
        {
            "taskId": "cce86178-81de-4cb9-88ea-eba525c6daba",
            "products": [
                {
                    "id": "50243820080",
                    "externalReferenceId": "external-reference-id-dafa9fef-df0c-4a6d-95d7-4ec56fe8f34e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:54:37.964Z",
            "finishedTime": "2022-09-20T08:54:38.111Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/cce86178-81de-4cb9-88ea-eba525c6daba"
        },
        {
            "taskId": "91a4aca3-dedd-4f85-8d2e-e64a148a8ac6",
            "products": [
                {
                    "id": "50205620080",
                    "externalReferenceId": "external-reference-id-d55cd70e-7860-4d74-9301-9ca225d5c14e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:55:48.727Z",
            "finishedTime": "2022-09-20T08:55:49.256Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/91a4aca3-dedd-4f85-8d2e-e64a148a8ac6"
        },
        {
            "taskId": "7db25652-fbf1-4c69-bae7-58a4aff5848e",
            "products": [
                {
                    "id": "50243830080",
                    "externalReferenceId": "external-reference-id-d2aea4bb-0c0f-4ee4-831f-82d7f3780423",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:56:31.353Z",
            "finishedTime": "2022-09-20T08:56:31.831Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7db25652-fbf1-4c69-bae7-58a4aff5848e"
        },
        {
            "taskId": "0ccad12b-a335-4686-9591-34c871b59009",
            "products": [
                {
                    "id": "50243830080",
                    "externalReferenceId": "external-reference-id-d2aea4bb-0c0f-4ee4-831f-82d7f3780423",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:56:38.680Z",
            "finishedTime": "2022-09-20T08:56:38.826Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/0ccad12b-a335-4686-9591-34c871b59009"
        },
        {
            "taskId": "7ae75259-2f9c-4a25-9711-12778930e64f",
            "products": [
                {
                    "id": "50243830080",
                    "externalReferenceId": "external-reference-id-d2aea4bb-0c0f-4ee4-831f-82d7f3780423",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:56:47.269Z",
            "finishedTime": "2022-09-20T08:56:47.497Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7ae75259-2f9c-4a25-9711-12778930e64f"
        },
        {
            "taskId": "8d7fb2ec-023a-4854-947e-8a36d7e79194",
            "products": [
                {
                    "id": "50243840080",
                    "externalReferenceId": "external-reference-id-427dfda4-b69f-47a2-9410-be2cc8dd1040",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:57:14.374Z",
            "finishedTime": "2022-09-20T08:57:15.000Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/8d7fb2ec-023a-4854-947e-8a36d7e79194"
        },
        {
            "taskId": "f6bd3994-69c9-43cc-8911-a6b93866b8b1",
            "products": [
                {
                    "id": "50243840080",
                    "externalReferenceId": "external-reference-id-427dfda4-b69f-47a2-9410-be2cc8dd1040",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:57:25.267Z",
            "finishedTime": "2022-09-20T08:57:25.496Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f6bd3994-69c9-43cc-8911-a6b93866b8b1"
        },
        {
            "taskId": "7a745bfd-2e86-4b59-a58a-db2ecad3ea05",
            "products": [
                {
                    "id": "50243840080",
                    "externalReferenceId": "external-reference-id-427dfda4-b69f-47a2-9410-be2cc8dd1040",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:57:31.843Z",
            "finishedTime": "2022-09-20T08:57:32.056Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7a745bfd-2e86-4b59-a58a-db2ecad3ea05"
        },
        {
            "taskId": "5ec16dea-0505-42ab-9796-c603a0347e75",
            "products": [
                {
                    "id": "50243840080",
                    "externalReferenceId": "external-reference-id-427dfda4-b69f-47a2-9410-be2cc8dd1040",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:58:45.977Z",
            "finishedTime": "2022-09-20T08:58:46.373Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/5ec16dea-0505-42ab-9796-c603a0347e75"
        },
        {
            "taskId": "5dc976f0-8f53-42d9-b239-7a195b25d77c",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-22T18:58:28.495Z",
            "finishedTime": "2022-09-22T18:58:30.490Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/5dc976f0-8f53-42d9-b239-7a195b25d77c"
        },
        {
            "taskId": "7304115a-2123-4bff-93ff-584484805a4c",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-22T20:14:53.928Z",
            "finishedTime": "2022-09-22T20:14:55.434Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7304115a-2123-4bff-93ff-584484805a4c"
        },
        {
            "taskId": "80c2dff9-8e00-485e-b787-c60abd22343b",
            "products": [
                {
                    "id": "69888590080",
                    "externalReferenceId": "external-reference-id-7b2445a0-e291-40cf-aded-fc3f4b83d073",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:51:27.298Z",
            "finishedTime": "2022-09-28T08:51:29.002Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/80c2dff9-8e00-485e-b787-c60abd22343b"
        },
        {
            "taskId": "f7009158-4252-4eee-8235-9f6072fbcf90",
            "products": [
                {
                    "id": "69888600080",
                    "externalReferenceId": "external-reference-id-36aa954d-c91d-4abc-9aa0-2a568bab4c2c",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:51:45.401Z",
            "finishedTime": "2022-09-28T08:51:45.835Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f7009158-4252-4eee-8235-9f6072fbcf90"
        },
        {
            "taskId": "51768284-2d5b-4a90-97bc-40bd97fb8e4b",
            "products": [
                {
                    "id": "69888610080",
                    "externalReferenceId": "external-reference-id-36aa954d-c91d-4abc-9aa0-2a568bab4c2c",
                    "productType": "BASE"
                },
                {
                    "id": "69888620080",
                    "externalReferenceId": "external-reference-id-36aa954d-c91d-4abc-9aa0-2a568bab4c2c",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:52:13.864Z",
            "finishedTime": "2022-09-28T08:52:18.843Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/51768284-2d5b-4a90-97bc-40bd97fb8e4b"
        },
        {
            "taskId": "e541637c-72ff-4114-922f-400761496931",
            "products": [
                {
                    "id": "69888630080",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:52:34.916Z",
            "finishedTime": "2022-09-28T08:52:35.118Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/e541637c-72ff-4114-922f-400761496931"
        },
        {
            "taskId": "3c783b6d-dc37-4551-9a33-5b3c02942d42",
            "products": [
                {
                    "id": "69888640080",
                    "externalReferenceId": "external-reference-id-eaea54a6-8049-4c1d-bfc1-47f46258e8d6",
                    "productType": "BASE"
                },
                {
                    "id": "69888650080",
                    "externalReferenceId": "external-reference-id-eaea54a6-8049-4c1d-bfc1-47f46258e8d6",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:53:00.190Z",
            "finishedTime": "2022-09-28T08:53:01.522Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/3c783b6d-dc37-4551-9a33-5b3c02942d42"
        },
        {
            "taskId": "aba616d0-7db8-43ce-8df2-3bf3bc4b01e5",
            "products": [
                {
                    "id": "69888630080",
                    "externalReferenceId": "UpdateVariation2-eaea54a6-8049-4c1d-bfc1-47f46258e8d6",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:53:45.236Z",
            "finishedTime": "2022-09-28T08:53:47.088Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/aba616d0-7db8-43ce-8df2-3bf3bc4b01e5"
        }
    ],
    "totalSize": 61,
    "nextPage": {
        "startingAfter": "aba616d0-7db8-43ce-8df2-3bf3bc4b01e5"
    },
    "searchCriteria": {
        "beginReceivedTime": "2022-09-01T00:00:00.000Z",
        "endReceivedTime": "2022-10-01T00:00:00.000Z",
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

#### Getting the next page

Use the `beginReceivedTime` parameter to filter dates based on the date when the task was received. The following example shows how to display the next page.

{% tabs %}
{% tab title="beginReceivedTime cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/tasks?beginReceivedTime=2022-09-01T00:00:00.000Z' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
This request displays the next page by `beginReceivedTime` in the [synchronous ](../../admin-apis/product-management/getting-started.md#asynchronous-and-synchronous-calls)response.

{% code overflow="wrap" %}
```json
{
    "tasks": [
        {
            "taskId": "eeacb15c-b3f8-494d-9b6f-fb4e9f4c42f7",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-19T17:22:11.415Z",
            "finishedTime": "2022-09-19T17:22:13.030Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/eeacb15c-b3f8-494d-9b6f-fb4e9f4c42f7"
        },
        {
            "taskId": "81192428-c98f-472d-99ea-fdbd79319cf8",
            "products": [
                {
                    "id": "50205470080",
                    "externalReferenceId": "external-reference-id-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:27:02.206Z",
            "finishedTime": "2022-09-20T08:27:03.833Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/81192428-c98f-472d-99ea-fdbd79319cf8"
        },
        {
            "taskId": "897391ee-941a-435b-9f54-bf97edb9fa49",
            "products": [
                {
                    "id": "50205480080",
                    "externalReferenceId": "external-reference-id-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "BASE"
                },
                {
                    "id": "50205490080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:28:17.554Z",
            "finishedTime": "2022-09-20T08:28:18.198Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/897391ee-941a-435b-9f54-bf97edb9fa49"
        },
        {
            "taskId": "42d617cc-7a35-4d44-93d5-028b26899fe2",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:28:51.100Z",
            "finishedTime": "2022-09-20T08:28:51.788Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/42d617cc-7a35-4d44-93d5-028b26899fe2"
        },
        {
            "taskId": "085e3321-a79e-4228-b612-7a6b874f2cbc",
            "products": [
                {
                    "id": "50205500080",
                    "externalReferenceId": "external-reference-id-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "BASE"
                },
                {
                    "id": "50205510080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:29:26.480Z",
            "finishedTime": "2022-09-20T08:29:26.792Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/085e3321-a79e-4228-b612-7a6b874f2cbc"
        },
        {
            "taskId": "a16cc310-a93c-47d7-800a-2cad7c7e8427",
            "products": [
                {
                    "id": "50205500080",
                    "externalReferenceId": "UpdateBasereference-id-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:29:32.829Z",
            "finishedTime": "2022-09-20T08:29:33.005Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/a16cc310-a93c-47d7-800a-2cad7c7e8427"
        },
        {
            "taskId": "ac8d32a0-ed4d-4027-b720-9c905af2ac44",
            "products": [
                {
                    "id": "50205510080",
                    "externalReferenceId": "UpdateVariation-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:29:39.530Z",
            "finishedTime": "2022-09-20T08:29:39.692Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ac8d32a0-ed4d-4027-b720-9c905af2ac44"
        },
        {
            "taskId": "f02ad711-5431-4ebc-8f92-d9f204047a64",
            "products": [
                {
                    "id": "50205480080",
                    "externalReferenceId": "UpdateVariation-eb3b4307-acd3-4657-a0aa-0df205ede4e9",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:30:12.143Z",
            "finishedTime": "2022-09-20T08:30:12.708Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f02ad711-5431-4ebc-8f92-d9f204047a64"
        },
        {
            "taskId": "5aba9cc0-9657-43d7-9cb9-8ab5df0efe34",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:30:52.462Z",
            "finishedTime": "2022-09-20T08:30:52.672Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/5aba9cc0-9657-43d7-9cb9-8ab5df0efe34"
        },
        {
            "taskId": "2102c363-c5b6-4ef0-a25b-3865be6b0af3",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:31:33.015Z",
            "finishedTime": "2022-09-20T08:31:33.364Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/2102c363-c5b6-4ef0-a25b-3865be6b0af3"
        },
        {
            "taskId": "3ba3b612-a9a2-4f38-b657-cbe7d7c6b330",
            "products": [
                {
                    "id": "50243780080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:31:49.899Z",
            "finishedTime": "2022-09-20T08:31:50.236Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/3ba3b612-a9a2-4f38-b657-cbe7d7c6b330"
        },
        {
            "taskId": "41903158-7e18-4d5e-ad75-3ad4462ddb37",
            "products": [
                {
                    "id": "50243790080",
                    "externalReferenceId": "external-reference-id-a4e2db25-3568-4933-9508-59db068bad9f",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:32:20.538Z",
            "finishedTime": "2022-09-20T08:32:21.085Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/41903158-7e18-4d5e-ad75-3ad4462ddb37"
        },
        {
            "taskId": "d7c9e5a9-0d7e-4684-bbfd-9c70c3aad449",
            "products": [
                {
                    "id": "50243800080",
                    "externalReferenceId": "external-reference-id-a4e2db25-3568-4933-9508-59db068bad9f",
                    "productType": "BASE"
                },
                {
                    "id": "50243810080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:32:33.962Z",
            "finishedTime": "2022-09-20T08:32:34.275Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/d7c9e5a9-0d7e-4684-bbfd-9c70c3aad449"
        },
        {
            "taskId": "824b98a4-d50c-462c-9ed8-05d9b8872e55",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:32:51.817Z",
            "finishedTime": "2022-09-20T08:32:52.052Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/824b98a4-d50c-462c-9ed8-05d9b8872e55"
        },
        {
            "taskId": "1d0da4e9-fb60-4f53-ade5-ce25098336a1",
            "products": [
                {
                    "id": "50205520080",
                    "externalReferenceId": "external-reference-id-a4e2db25-3568-4933-9508-59db068bad9f",
                    "productType": "BASE"
                },
                {
                    "id": "50205530080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:33:22.582Z",
            "finishedTime": "2022-09-20T08:33:23.027Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/1d0da4e9-fb60-4f53-ade5-ce25098336a1"
        },
        {
            "taskId": "b7130a34-997b-4267-995a-1f91abedaa79",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:33:53.018Z",
            "finishedTime": "2022-09-20T08:33:53.169Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/b7130a34-997b-4267-995a-1f91abedaa79"
        },
        {
            "taskId": "1a2a378a-a26f-497f-b0a8-019606ee702a",
            "products": [
                {
                    "id": "50205540080",
                    "externalReferenceId": "external-reference-id-864fa6bc-d85d-4ce8-9d37-4dcb34211caf",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:44:54.715Z",
            "finishedTime": "2022-09-20T08:44:55.116Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/1a2a378a-a26f-497f-b0a8-019606ee702a"
        },
        {
            "taskId": "382b3c3a-fd68-4edf-a9f9-fea04abad77b",
            "products": [
                {
                    "id": "50205540080",
                    "externalReferenceId": "external-reference-id-864fa6bc-d85d-4ce8-9d37-4dcb34211caf",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:45:01.633Z",
            "finishedTime": "2022-09-20T08:45:01.959Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/382b3c3a-fd68-4edf-a9f9-fea04abad77b"
        },
        {
            "taskId": "9d93801d-aede-418f-b22b-c4fe49e9594f",
            "products": [
                {
                    "id": "50205540080",
                    "externalReferenceId": "external-reference-id-864fa6bc-d85d-4ce8-9d37-4dcb34211caf",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:45:38.748Z",
            "finishedTime": "2022-09-20T08:45:38.899Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/9d93801d-aede-418f-b22b-c4fe49e9594f"
        },
        {
            "taskId": "ad78a645-23ac-4302-845d-dcd63298201f",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:46:32.746Z",
            "finishedTime": "2022-09-20T08:46:32.998Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ad78a645-23ac-4302-845d-dcd63298201f"
        },
        {
            "taskId": "7e985af6-428b-4aaf-b07f-8df7be69c34f",
            "products": [
                {
                    "id": "50205580080",
                    "externalReferenceId": "external-reference-id-6918b6ea-ee26-4475-a50b-6a7d69a67af9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:47:15.361Z",
            "finishedTime": "2022-09-20T08:47:15.853Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7e985af6-428b-4aaf-b07f-8df7be69c34f"
        },
        {
            "taskId": "4a52927e-b805-407f-b1e0-5f8f09854948",
            "products": [
                {
                    "id": "50205580080",
                    "externalReferenceId": "external-reference-id-6918b6ea-ee26-4475-a50b-6a7d69a67af9",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:47:25.272Z",
            "finishedTime": "2022-09-20T08:47:25.510Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/4a52927e-b805-407f-b1e0-5f8f09854948"
        },
        {
            "taskId": "7e8a2b5b-3c52-42b6-aa38-b54563f2c607",
            "products": [
                {
                    "id": "50205590080",
                    "externalReferenceId": "external-reference-id-245f1188-48ad-4782-9df6-174d18137556",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:51:27.726Z",
            "finishedTime": "2022-09-20T08:51:28.182Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7e8a2b5b-3c52-42b6-aa38-b54563f2c607"
        },
        {
            "taskId": "673a7e51-6d42-49e5-b368-9f3e95eaf41a",
            "products": [
                {
                    "id": "50205590080",
                    "externalReferenceId": "external-reference-id-245f1188-48ad-4782-9df6-174d18137556",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:51:35.129Z",
            "finishedTime": "2022-09-20T08:51:35.468Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/673a7e51-6d42-49e5-b368-9f3e95eaf41a"
        },
        {
            "taskId": "7d840529-c4ab-4301-b9a4-566debbc2441",
            "products": [
                {
                    "id": "50205590080",
                    "externalReferenceId": "external-reference-id-245f1188-48ad-4782-9df6-174d18137556",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "RETIRE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:51:51.198Z",
            "finishedTime": "2022-09-20T08:51:51.347Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7d840529-c4ab-4301-b9a4-566debbc2441"
        },
        {
            "taskId": "e8ab9e99-1e78-4cd9-8ba0-261c91378b78",
            "products": [
                {
                    "id": "50205600080",
                    "externalReferenceId": "external-reference-id-52b3071f-7705-4311-bbb9-332c282460b2",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:52:26.762Z",
            "finishedTime": "2022-09-20T08:52:27.165Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/e8ab9e99-1e78-4cd9-8ba0-261c91378b78"
        },
        {
            "taskId": "138d1c2a-0d55-417a-b9f8-cd6a2717f70d",
            "products": [
                {
                    "id": "50205600080",
                    "externalReferenceId": "external-reference-id-52b3071f-7705-4311-bbb9-332c282460b2",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:52:33.796Z",
            "finishedTime": "2022-09-20T08:52:33.921Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/138d1c2a-0d55-417a-b9f8-cd6a2717f70d"
        },
        {
            "taskId": "432db185-e0d3-4565-a8da-220904a47ec2",
            "products": [
                {
                    "id": "50205610080",
                    "externalReferenceId": "external-reference-id-65473354-f908-4286-a22d-5eb994090ca6",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:53:01.523Z",
            "finishedTime": "2022-09-20T08:53:01.908Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/432db185-e0d3-4565-a8da-220904a47ec2"
        },
        {
            "taskId": "5cbfdd0d-3f7f-49f7-a163-4f46150989ae",
            "products": [
                {
                    "id": "50205610080",
                    "externalReferenceId": "external-reference-id-65473354-f908-4286-a22d-5eb994090ca6",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:53:19.463Z",
            "finishedTime": "2022-09-20T08:53:19.799Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/5cbfdd0d-3f7f-49f7-a163-4f46150989ae"
        },
        {
            "taskId": "8ce994fd-2cb9-45e4-ab78-71d38daa5dd9",
            "products": [
                {
                    "id": "50205610080",
                    "externalReferenceId": "external-reference-id-65473354-f908-4286-a22d-5eb994090ca6",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:53:29.140Z",
            "finishedTime": "2022-09-20T08:53:29.466Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/8ce994fd-2cb9-45e4-ab78-71d38daa5dd9"
        },
        {
            "taskId": "ea2a26b6-c0c8-4c60-856b-12cdf5773d67",
            "products": [
                {
                    "id": "50243820080",
                    "externalReferenceId": "external-reference-id-dafa9fef-df0c-4a6d-95d7-4ec56fe8f34e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:54:20.695Z",
            "finishedTime": "2022-09-20T08:54:21.031Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ea2a26b6-c0c8-4c60-856b-12cdf5773d67"
        },
        {
            "taskId": "ba2d0c03-33e2-4e9f-9836-2567d838c7b8",
            "products": [
                {
                    "id": "50243820080",
                    "externalReferenceId": "external-reference-id-dafa9fef-df0c-4a6d-95d7-4ec56fe8f34e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:54:27.140Z",
            "finishedTime": "2022-09-20T08:54:27.474Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ba2d0c03-33e2-4e9f-9836-2567d838c7b8"
        },
        {
            "taskId": "55eaf467-d892-4b01-90f0-585d8dc47ded",
            "products": [
                {
                    "id": "50243820080",
                    "externalReferenceId": "external-reference-id-dafa9fef-df0c-4a6d-95d7-4ec56fe8f34e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:54:30.839Z",
            "finishedTime": "2022-09-20T08:54:31.337Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/55eaf467-d892-4b01-90f0-585d8dc47ded"
        },
        {
            "taskId": "cce86178-81de-4cb9-88ea-eba525c6daba",
            "products": [
                {
                    "id": "50243820080",
                    "externalReferenceId": "external-reference-id-dafa9fef-df0c-4a6d-95d7-4ec56fe8f34e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:54:37.964Z",
            "finishedTime": "2022-09-20T08:54:38.111Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/cce86178-81de-4cb9-88ea-eba525c6daba"
        },
        {
            "taskId": "91a4aca3-dedd-4f85-8d2e-e64a148a8ac6",
            "products": [
                {
                    "id": "50205620080",
                    "externalReferenceId": "external-reference-id-d55cd70e-7860-4d74-9301-9ca225d5c14e",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:55:48.727Z",
            "finishedTime": "2022-09-20T08:55:49.256Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/91a4aca3-dedd-4f85-8d2e-e64a148a8ac6"
        },
        {
            "taskId": "7db25652-fbf1-4c69-bae7-58a4aff5848e",
            "products": [
                {
                    "id": "50243830080",
                    "externalReferenceId": "external-reference-id-d2aea4bb-0c0f-4ee4-831f-82d7f3780423",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:56:31.353Z",
            "finishedTime": "2022-09-20T08:56:31.831Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7db25652-fbf1-4c69-bae7-58a4aff5848e"
        },
        {
            "taskId": "0ccad12b-a335-4686-9591-34c871b59009",
            "products": [
                {
                    "id": "50243830080",
                    "externalReferenceId": "external-reference-id-d2aea4bb-0c0f-4ee4-831f-82d7f3780423",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:56:38.680Z",
            "finishedTime": "2022-09-20T08:56:38.826Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/0ccad12b-a335-4686-9591-34c871b59009"
        },
        {
            "taskId": "7ae75259-2f9c-4a25-9711-12778930e64f",
            "products": [
                {
                    "id": "50243830080",
                    "externalReferenceId": "external-reference-id-d2aea4bb-0c0f-4ee4-831f-82d7f3780423",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:56:47.269Z",
            "finishedTime": "2022-09-20T08:56:47.497Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7ae75259-2f9c-4a25-9711-12778930e64f"
        },
        {
            "taskId": "8d7fb2ec-023a-4854-947e-8a36d7e79194",
            "products": [
                {
                    "id": "50243840080",
                    "externalReferenceId": "external-reference-id-427dfda4-b69f-47a2-9410-be2cc8dd1040",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:57:14.374Z",
            "finishedTime": "2022-09-20T08:57:15.000Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/8d7fb2ec-023a-4854-947e-8a36d7e79194"
        },
        {
            "taskId": "f6bd3994-69c9-43cc-8911-a6b93866b8b1",
            "products": [
                {
                    "id": "50243840080",
                    "externalReferenceId": "external-reference-id-427dfda4-b69f-47a2-9410-be2cc8dd1040",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-20T08:57:25.267Z",
            "finishedTime": "2022-09-20T08:57:25.496Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f6bd3994-69c9-43cc-8911-a6b93866b8b1"
        },
        {
            "taskId": "7a745bfd-2e86-4b59-a58a-db2ecad3ea05",
            "products": [
                {
                    "id": "50243840080",
                    "externalReferenceId": "external-reference-id-427dfda4-b69f-47a2-9410-be2cc8dd1040",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:57:31.843Z",
            "finishedTime": "2022-09-20T08:57:32.056Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7a745bfd-2e86-4b59-a58a-db2ecad3ea05"
        },
        {
            "taskId": "5ec16dea-0505-42ab-9796-c603a0347e75",
            "products": [
                {
                    "id": "50243840080",
                    "externalReferenceId": "external-reference-id-427dfda4-b69f-47a2-9410-be2cc8dd1040",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "DEPLOY_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-20T08:58:45.977Z",
            "finishedTime": "2022-09-20T08:58:46.373Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/5ec16dea-0505-42ab-9796-c603a0347e75"
        },
        {
            "taskId": "5dc976f0-8f53-42d9-b239-7a195b25d77c",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-22T18:58:28.495Z",
            "finishedTime": "2022-09-22T18:58:30.490Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/5dc976f0-8f53-42d9-b239-7a195b25d77c"
        },
        {
            "taskId": "7304115a-2123-4bff-93ff-584484805a4c",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-09-22T20:14:53.928Z",
            "finishedTime": "2022-09-22T20:14:55.434Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7304115a-2123-4bff-93ff-584484805a4c"
        },
        {
            "taskId": "80c2dff9-8e00-485e-b787-c60abd22343b",
            "products": [
                {
                    "id": "69888590080",
                    "externalReferenceId": "external-reference-id-7b2445a0-e291-40cf-aded-fc3f4b83d073",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:51:27.298Z",
            "finishedTime": "2022-09-28T08:51:29.002Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/80c2dff9-8e00-485e-b787-c60abd22343b"
        },
        {
            "taskId": "f7009158-4252-4eee-8235-9f6072fbcf90",
            "products": [
                {
                    "id": "69888600080",
                    "externalReferenceId": "external-reference-id-36aa954d-c91d-4abc-9aa0-2a568bab4c2c",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:51:45.401Z",
            "finishedTime": "2022-09-28T08:51:45.835Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f7009158-4252-4eee-8235-9f6072fbcf90"
        },
        {
            "taskId": "51768284-2d5b-4a90-97bc-40bd97fb8e4b",
            "products": [
                {
                    "id": "69888610080",
                    "externalReferenceId": "external-reference-id-36aa954d-c91d-4abc-9aa0-2a568bab4c2c",
                    "productType": "BASE"
                },
                {
                    "id": "69888620080",
                    "externalReferenceId": "external-reference-id-36aa954d-c91d-4abc-9aa0-2a568bab4c2c",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:52:13.864Z",
            "finishedTime": "2022-09-28T08:52:18.843Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/51768284-2d5b-4a90-97bc-40bd97fb8e4b"
        },
        {
            "taskId": "e541637c-72ff-4114-922f-400761496931",
            "products": [
                {
                    "id": "69888630080",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:52:34.916Z",
            "finishedTime": "2022-09-28T08:52:35.118Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/e541637c-72ff-4114-922f-400761496931"
        },
        {
            "taskId": "3c783b6d-dc37-4551-9a33-5b3c02942d42",
            "products": [
                {
                    "id": "69888640080",
                    "externalReferenceId": "external-reference-id-eaea54a6-8049-4c1d-bfc1-47f46258e8d6",
                    "productType": "BASE"
                },
                {
                    "id": "69888650080",
                    "externalReferenceId": "external-reference-id-eaea54a6-8049-4c1d-bfc1-47f46258e8d6",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:53:00.190Z",
            "finishedTime": "2022-09-28T08:53:01.522Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/3c783b6d-dc37-4551-9a33-5b3c02942d42"
        },
        {
            "taskId": "aba616d0-7db8-43ce-8df2-3bf3bc4b01e5",
            "products": [
                {
                    "id": "69888630080",
                    "externalReferenceId": "UpdateVariation2-eaea54a6-8049-4c1d-bfc1-47f46258e8d6",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-09-28T08:53:45.236Z",
            "finishedTime": "2022-09-28T08:53:47.088Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/aba616d0-7db8-43ce-8df2-3bf3bc4b01e5"
        }
    ],
    "totalSize": 61,
    "nextPage": {
        "startingAfter": "aba616d0-7db8-43ce-8df2-3bf3bc4b01e5"
    },
    "searchCriteria": {
        "beginReceivedTime": "2022-09-01T00:00:00.000Z",
        "endReceivedTime": "2022-10-01T00:00:00.000Z",
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

### endReceivedTime

This optional `endReceivedTime` query parameter filters a list on the `finishedTime` field. The value can be a string with an ISO-8601 UTC format `datetime` (for example, `yyyy-mm-ddT00:00:00.000Z`).  The response displays results for 30 days before and including the specified date.\
\
`GET 'https://api.digitalriver.com/v1/products/tasks?endReceivedTime=2022-10-31T00:00:00.000Z'`

#### Getting tasks by `endReceivedTime`

The following [`GET /products/tasks?endReceivedTime={yyyy-mm-ddT00:00:00.000Z}` ](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Get-Product-Task-Status-\(Synchronous-API\)/paths/\~1products\~1tasks\~1/get)request filters tasks by the [`finishedTime`](tasks.md#received-and-finished-time) (for example, `2022-10-30T23:00:00.000Z`). The end received time includes everything ending on the specified finished time date and going backward.&#x20;

{% tabs %}
{% tab title="endReceivedTime cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/tasks?endReceivedTime=2022-10-30T23:00:00.000Z' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK Response" %}
{% code overflow="wrap" %}
```json
{
    "tasks": [
        {
            "taskId": "7a6cb254-73ef-4a2e-a4b6-04dafbeda462",
            "products": [
                {
                    "id": "50274880080",
                    "externalReferenceId": "external-reference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-05T06:29:14.424Z",
            "finishedTime": "2022-10-05T06:29:16.091Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7a6cb254-73ef-4a2e-a4b6-04dafbeda462"
        },
        {
            "taskId": "87c96f67-e866-48da-9886-10c52ae5d282",
            "products": [
                {
                    "id": "50274890080",
                    "externalReferenceId": "external-reference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "BASE"
                },
                {
                    "id": "50274900080",
                    "externalReferenceId": "external-reference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-05T06:32:55.788Z",
            "finishedTime": "2022-10-05T06:32:56.604Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/87c96f67-e866-48da-9886-10c52ae5d282"
        },
        {
            "taskId": "1ac97c1b-313d-4d8f-a2db-2e7db51f88a9",
            "products": [
                {
                    "id": "50274890080",
                    "externalReferenceId": "UpdateBasereference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-05T08:06:29.676Z",
            "finishedTime": "2022-10-05T08:06:30.672Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/1ac97c1b-313d-4d8f-a2db-2e7db51f88a9"
        },
        {
            "taskId": "396816a4-3a59-4a8e-be82-64a31b2c32b8",
            "products": [
                {
                    "id": "50274900080",
                    "externalReferenceId": "external-reference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T08:07:28.829Z",
            "finishedTime": "2022-10-05T08:07:29.387Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/396816a4-3a59-4a8e-be82-64a31b2c32b8"
        },
        {
            "taskId": "51acb43d-9b92-4c48-98cd-18760588f374",
            "products": [
                {
                    "id": "50274900080",
                    "externalReferenceId": "UpdateVariation2-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-05T08:08:37.302Z",
            "finishedTime": "2022-10-05T08:08:37.894Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/51acb43d-9b92-4c48-98cd-18760588f374"
        },
        {
            "taskId": "cd51e61f-1487-4240-a055-6ce45959cc6c",
            "products": [
                {
                    "id": "50274890080",
                    "externalReferenceId": "UpdateBasereference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-05T08:08:58.331Z",
            "finishedTime": "2022-10-05T08:08:58.805Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/cd51e61f-1487-4240-a055-6ce45959cc6c"
        },
        {
            "taskId": "0069835e-7b7a-4239-ac45-bc3ccc6925aa",
            "products": [
                {
                    "id": "50274900080",
                    "externalReferenceId": "UpdateVariation2-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-05T08:32:31.161Z",
            "finishedTime": "2022-10-05T08:32:31.690Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/0069835e-7b7a-4239-ac45-bc3ccc6925aa"
        },
        {
            "taskId": "fa01ad62-0a28-4175-a5ca-69e235ea2de2",
            "products": [
                {
                    "id": "50274900080",
                    "externalReferenceId": "UpdateVariation2-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T08:34:31.910Z",
            "finishedTime": "2022-10-05T08:34:32.934Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/fa01ad62-0a28-4175-a5ca-69e235ea2de2"
        },
        {
            "taskId": "dc4e9c4a-02ad-4c0f-a3e0-3f59adf11d77",
            "products": [
                {
                    "id": "50274900080",
                    "externalReferenceId": "UpdateVariation2-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T08:34:46.997Z",
            "finishedTime": "2022-10-05T08:34:47.453Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/dc4e9c4a-02ad-4c0f-a3e0-3f59adf11d77"
        },
        {
            "taskId": "426cc543-966f-43c2-96cb-3210ca77cba9",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T09:07:38.609Z",
            "finishedTime": "2022-10-05T09:07:39.704Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/426cc543-966f-43c2-96cb-3210ca77cba9"
        },
        {
            "taskId": "75ef1404-99b5-42c1-b5fe-6d0b4e8bb004",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T09:08:58.755Z",
            "finishedTime": "2022-10-05T09:08:59.353Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/75ef1404-99b5-42c1-b5fe-6d0b4e8bb004"
        },
        {
            "taskId": "356d536d-4ea4-418f-b063-25f0beee5a33",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T09:09:38.888Z",
            "finishedTime": "2022-10-05T09:09:39.509Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/356d536d-4ea4-418f-b063-25f0beee5a33"
        },
        {
            "taskId": "d07bc170-b984-48d4-9723-fed186669441",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T09:11:25.315Z",
            "finishedTime": "2022-10-05T09:11:25.998Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/d07bc170-b984-48d4-9723-fed186669441"
        },
        {
            "taskId": "899c7882-c69a-474e-ab48-256bf27d82d6",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T09:12:57.362Z",
            "finishedTime": "2022-10-05T09:12:58.060Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/899c7882-c69a-474e-ab48-256bf27d82d6"
        },
        {
            "taskId": "208d0ce5-8d37-4ef7-9bd9-f39b1c6920eb",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-05T09:13:40.132Z",
            "finishedTime": "2022-10-05T09:13:40.494Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/208d0ce5-8d37-4ef7-9bd9-f39b1c6920eb"
        },
        {
            "taskId": "096b9def-9e57-4aff-92eb-f30f8bbf5d2c",
            "products": [
                {
                    "id": "50275050080",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-05T09:14:05.899Z",
            "finishedTime": "2022-10-05T09:14:06.270Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/096b9def-9e57-4aff-92eb-f30f8bbf5d2c"
        },
        {
            "taskId": "79a7906b-771d-4804-80b9-bc209e57c9cb",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T07:13:01.867Z",
            "finishedTime": "2022-10-06T07:13:03.423Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/79a7906b-771d-4804-80b9-bc209e57c9cb"
        },
        {
            "taskId": "e7608e79-0b7f-49b3-855c-52641802acf3",
            "products": [
                {
                    "id": "50434630080",
                    "productType": "BASE"
                },
                {
                    "id": "50434640080",
                    "productType": "VARIATION"
                },
                {
                    "id": "50434650080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-06T07:14:37.034Z",
            "finishedTime": "2022-10-06T07:14:37.773Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/e7608e79-0b7f-49b3-855c-52641802acf3"
        },
        {
            "taskId": "2d962745-0529-4621-8545-56a889da0973",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T07:14:54.728Z",
            "finishedTime": "2022-10-06T07:14:55.622Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/2d962745-0529-4621-8545-56a889da0973"
        },
        {
            "taskId": "d7e99baf-efde-48c5-92ce-6ad710281a2e",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T07:17:17.561Z",
            "finishedTime": "2022-10-06T07:17:18.149Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/d7e99baf-efde-48c5-92ce-6ad710281a2e"
        },
        {
            "taskId": "73f32e97-1ff6-43bf-bea2-c12bfe9666a8",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T07:17:32.710Z",
            "finishedTime": "2022-10-06T07:17:33.215Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/73f32e97-1ff6-43bf-bea2-c12bfe9666a8"
        },
        {
            "taskId": "24655e38-54d8-437c-8224-80cefe16e415",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T07:19:05.306Z",
            "finishedTime": "2022-10-06T07:19:05.923Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/24655e38-54d8-437c-8224-80cefe16e415"
        },
        {
            "taskId": "6270bd8a-7e40-4cd5-aa22-ac9c2d56f4ea",
            "products": [
                {
                    "id": "50275270080",
                    "externalReferenceId": "external-reference-id-9aafe028-8b26-4666-927f-0a26775f178c",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-06T08:00:49.199Z",
            "finishedTime": "2022-10-06T08:00:50.921Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/6270bd8a-7e40-4cd5-aa22-ac9c2d56f4ea"
        },
        {
            "taskId": "e5750d7c-bbd4-4a43-ae3f-b0e96d1397dd",
            "products": [
                {
                    "id": "50275280080",
                    "externalReferenceId": "external-reference-id-9aafe028-8b26-4666-927f-0a26775f178c",
                    "productType": "BASE"
                },
                {
                    "id": "50275290080",
                    "externalReferenceId": "external-reference-id-9aafe028-8b26-4666-927f-0a26775f178c",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-06T08:00:59.497Z",
            "finishedTime": "2022-10-06T08:01:00.348Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/e5750d7c-bbd4-4a43-ae3f-b0e96d1397dd"
        },
        {
            "taskId": "9a385a9a-19c1-4b65-a1f2-44526e528e04",
            "products": [
                {
                    "id": "50275270080",
                    "externalReferenceId": "external-reference-id-9aafe028-8b26-4666-927f-0a26775f178c",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:01:22.973Z",
            "finishedTime": "2022-10-06T08:01:23.307Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/9a385a9a-19c1-4b65-a1f2-44526e528e04"
        },
        {
            "taskId": "388eff2c-bbc7-47da-bb36-1f5c93d50fe4",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:02:47.570Z",
            "finishedTime": "2022-10-06T08:02:48.172Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/388eff2c-bbc7-47da-bb36-1f5c93d50fe4"
        },
        {
            "taskId": "10c67a90-186b-4311-b33b-9895073500d7",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:03:58.038Z",
            "finishedTime": "2022-10-06T08:03:58.499Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/10c67a90-186b-4311-b33b-9895073500d7"
        },
        {
            "taskId": "10f0ae3c-55b3-4a60-a79e-56ee13229984",
            "products": [],
            "requestType": "CREATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:04:23.491Z",
            "finishedTime": "2022-10-06T08:04:24.070Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/10f0ae3c-55b3-4a60-a79e-56ee13229984"
        },
        {
            "taskId": "00ce5d1c-30ba-443e-9e5a-912ed3c8dd32",
            "products": [
                {
                    "id": "50274890080",
                    "externalReferenceId": "UpdateBasereference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:05:12.415Z",
            "finishedTime": "2022-10-06T08:05:12.809Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/00ce5d1c-30ba-443e-9e5a-912ed3c8dd32"
        },
        {
            "taskId": "23d11f97-cea0-4d8a-8cda-75815acd9f7d",
            "products": [
                {
                    "id": "50274890080",
                    "externalReferenceId": "UpdateBasereference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:05:38.659Z",
            "finishedTime": "2022-10-06T08:05:39.083Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/23d11f97-cea0-4d8a-8cda-75815acd9f7d"
        },
        {
            "taskId": "aab67bd9-a7c6-4cd7-80ec-d8cb0b496eca",
            "products": [
                {
                    "id": "50275270080",
                    "externalReferenceId": "external-reference-id-9aafe028-8b26-4666-927f-0a26775f178c",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:05:51.172Z",
            "finishedTime": "2022-10-06T08:05:51.440Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/aab67bd9-a7c6-4cd7-80ec-d8cb0b496eca"
        },
        {
            "taskId": "6b52c446-2aee-4b7f-9e95-39ccbf0cc712",
            "products": [
                {
                    "id": "50275270080",
                    "externalReferenceId": "external-reference-id-9aafe028-8b26-4666-927f-0a26775f178c",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:09:44.506Z",
            "finishedTime": "2022-10-06T08:09:44.982Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/6b52c446-2aee-4b7f-9e95-39ccbf0cc712"
        },
        {
            "taskId": "217b9f1b-73aa-4f6a-a957-f724e6a80c26",
            "products": [
                {
                    "id": "50274890080",
                    "externalReferenceId": "UpdateBasereference-id-67336703-11c9-4c6a-8a64-fb2dfa11a7d0",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:10:05.706Z",
            "finishedTime": "2022-10-06T08:10:05.985Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/217b9f1b-73aa-4f6a-a957-f724e6a80c26"
        },
        {
            "taskId": "14cab78b-7a9a-464c-98ad-a24e84a14c89",
            "products": [
                {
                    "id": "50275270080",
                    "externalReferenceId": "external-reference-id-9aafe028-8b26-4666-927f-0a26775f178c",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:10:28.823Z",
            "finishedTime": "2022-10-06T08:10:29.064Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/14cab78b-7a9a-464c-98ad-a24e84a14c89"
        },
        {
            "taskId": "1ffd37ff-40d6-4da2-8259-22d1ecb2500b",
            "products": [
                {
                    "id": "50275310080",
                    "externalReferenceId": "external-reference-id-adadef2a-5b59-4888-a6d1-ea97d49d7c16",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-06T08:14:54.787Z",
            "finishedTime": "2022-10-06T08:14:55.434Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/1ffd37ff-40d6-4da2-8259-22d1ecb2500b"
        },
        {
            "taskId": "953f0703-0f15-4341-81c0-98ec1b605ea4",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:15:09.521Z",
            "finishedTime": "2022-10-06T08:15:09.894Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/953f0703-0f15-4341-81c0-98ec1b605ea4"
        },
        {
            "taskId": "dae4202f-0683-4091-be72-2e5bfe22b517",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:15:40.696Z",
            "finishedTime": "2022-10-06T08:15:41.094Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/dae4202f-0683-4091-be72-2e5bfe22b517"
        },
        {
            "taskId": "f493aa00-49f1-4867-8aed-413f2b8c08a9",
            "products": [
                {
                    "id": "50275310080",
                    "externalReferenceId": "external-reference-id-adadef2a-5b59-4888-a6d1-ea97d49d7c16",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:17:12.756Z",
            "finishedTime": "2022-10-06T08:17:13.212Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f493aa00-49f1-4867-8aed-413f2b8c08a9"
        },
        {
            "taskId": "cd4a1bb7-c1b4-46b4-9cbd-0b5c18b197ee",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:17:55.238Z",
            "finishedTime": "2022-10-06T08:17:55.650Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/cd4a1bb7-c1b4-46b4-9cbd-0b5c18b197ee"
        },
        {
            "taskId": "85085271-146f-4c3c-8cb4-99ca2dbcc213",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-06T08:18:21.194Z",
            "finishedTime": "2022-10-06T08:18:21.555Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/85085271-146f-4c3c-8cb4-99ca2dbcc213"
        },
        {
            "taskId": "40945365-4f0e-4fc6-a597-e857239dbdd1",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-10T20:13:22.935Z",
            "finishedTime": "2022-10-10T20:13:26.664Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/40945365-4f0e-4fc6-a597-e857239dbdd1"
        },
        {
            "taskId": "2925cb0a-c65a-456d-a0de-72f3843b82b5",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-10T21:11:11.411Z",
            "finishedTime": "2022-10-10T21:11:14.218Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/2925cb0a-c65a-456d-a0de-72f3843b82b5"
        },
        {
            "taskId": "2a27c5dd-2efc-455e-a2c3-3bf41d34cf6b",
            "products": [
                {
                    "id": "50246610080",
                    "externalReferenceId": "external-reference-id-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-18T03:19:16.717Z",
            "finishedTime": "2022-10-18T03:19:19.921Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/2a27c5dd-2efc-455e-a2c3-3bf41d34cf6b"
        },
        {
            "taskId": "b20ecdee-8455-45ac-a26c-dddc75bb15fc",
            "products": [
                {
                    "id": "50246620080",
                    "externalReferenceId": "external-reference-id-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "BASE"
                },
                {
                    "id": "50246630080",
                    "externalReferenceId": "external-reference-id-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-18T03:43:57.705Z",
            "finishedTime": "2022-10-18T03:43:58.444Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/b20ecdee-8455-45ac-a26c-dddc75bb15fc"
        },
        {
            "taskId": "fe17a533-9811-4393-a23a-246e874c58af",
            "products": [
                {
                    "id": "50246620080",
                    "externalReferenceId": "UpdateBasereference-id-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-18T07:29:55.522Z",
            "finishedTime": "2022-10-18T07:29:56.300Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/fe17a533-9811-4393-a23a-246e874c58af"
        },
        {
            "taskId": "bcd6fe1a-bd3f-45a9-bd6d-42fcbb05d2b3",
            "products": [
                {
                    "id": "50246630080",
                    "externalReferenceId": "UpdateVariation2-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION_LIVE_CHANGE",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-18T07:30:01.951Z",
            "finishedTime": "2022-10-18T07:30:02.347Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/bcd6fe1a-bd3f-45a9-bd6d-42fcbb05d2b3"
        },
        {
            "taskId": "a1eb9ffa-fe87-4b95-8e8f-c5a4a78c01f3",
            "products": [
                {
                    "id": "50246640080",
                    "productType": "BASE"
                },
                {
                    "id": "50246650080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-18T08:47:12.489Z",
            "finishedTime": "2022-10-18T08:47:13.329Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/a1eb9ffa-fe87-4b95-8e8f-c5a4a78c01f3"
        },
        {
            "taskId": "f6b07dcc-5f16-4631-82b0-86e128b084e2",
            "products": [
                {
                    "id": "50246660080",
                    "externalReferenceId": "external-reference-id-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "BASE"
                },
                {
                    "id": "50246670080",
                    "externalReferenceId": "external-reference-id-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-10-18T09:06:00.676Z",
            "finishedTime": "2022-10-18T09:06:01.378Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f6b07dcc-5f16-4631-82b0-86e128b084e2"
        },
        {
            "taskId": "52790e7f-07d7-4003-bb94-d6ff52f6338d",
            "products": [
                {
                    "id": "50246660080",
                    "externalReferenceId": "external-reference-id-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "BASE"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-18T09:06:49.368Z",
            "finishedTime": "2022-10-18T09:06:49.935Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/52790e7f-07d7-4003-bb94-d6ff52f6338d"
        },
        {
            "taskId": "f2f2f826-fa91-43b2-b60e-95844f052ffa",
            "products": [
                {
                    "id": "50246670080",
                    "externalReferenceId": "external-reference-id-127aa133-26ea-4ea1-adec-d8cae4064457",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "UPDATE_VARIATION",
            "taskStatus": "FAILED",
            "receivedTime": "2022-10-18T09:07:15.438Z",
            "finishedTime": "2022-10-18T09:07:15.821Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f2f2f826-fa91-43b2-b60e-95844f052ffa"
        }
    ],
    "totalSize": 80,
    "nextPage": {
        "startingAfter": "f2f2f826-fa91-43b2-b60e-95844f052ffa"
    },
    "searchCriteria": {
        "beginReceivedTime": "2022-09-30T23:00:00.000Z",
        "endReceivedTime": "2022-10-30T23:00:00.000Z",
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

#### Getting the previous page

Use the `endReceivedTime` parameter to filter dates based on the date when the task was received. The following example shows how to display the next page.

{% tabs %}
{% tab title="endReceivedTime cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/v1/products/tasks?endReceivedTime=2022-10-30T23:00:00.000Z' \
--header 'Authorization: Bearer <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The response displays the previous page.

{% code overflow="wrap" %}
```json
{
    "tasks": [
        {
            "taskId": "475d2620-6b77-4dc6-b6c3-3829c1991163",
            "products": [
                {
                    "id": "52734680080",
                    "externalReferenceId": "external-reference-id-a722592b-04dc-4516-a36b-45f375c510ee",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-08T07:40:51.528Z",
            "finishedTime": "2022-12-08T07:40:52.973Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/475d2620-6b77-4dc6-b6c3-3829c1991163"
        },
        {
            "taskId": "7e473bf1-7863-44fa-b00a-436596089448",
            "products": [
                {
                    "id": "51772610080",
                    "externalReferenceId": "external-reference-id-a722592b-04dc-4516-a36b-45f375c510ee",
                    "productType": "BASE"
                },
                {
                    "id": "51772620080",
                    "externalReferenceId": "external-reference-id-a722592b-04dc-4516-a36b-45f375c510ee",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-13T08:22:42.218Z",
            "finishedTime": "2022-12-13T08:22:43.606Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/7e473bf1-7863-44fa-b00a-436596089448"
        },
        {
            "taskId": "c952ace1-2c13-448d-b75a-553687387b30",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-12-13T08:58:40.869Z",
            "finishedTime": "2022-12-13T08:58:41.689Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/c952ace1-2c13-448d-b75a-553687387b30"
        },
        {
            "taskId": "05f7ada1-a086-469c-a4dc-015fb463b379",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-12-13T08:59:07.481Z",
            "finishedTime": "2022-12-13T08:59:08.402Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/05f7ada1-a086-469c-a4dc-015fb463b379"
        },
        {
            "taskId": "26e799a3-261f-459e-921a-7f1d8b643246",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-12-13T09:00:24.895Z",
            "finishedTime": "2022-12-13T09:00:25.329Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/26e799a3-261f-459e-921a-7f1d8b643246"
        },
        {
            "taskId": "bc596e2b-47d7-48f4-9c8d-2b33904f879d",
            "products": [],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-12-13T09:08:28.647Z",
            "finishedTime": "2022-12-13T09:08:29.130Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/bc596e2b-47d7-48f4-9c8d-2b33904f879d"
        },
        {
            "taskId": "f29d0700-26ae-4dce-9ac6-7cc7f5ecaad4",
            "products": [
                {
                    "id": "51762670080",
                    "productType": "BASE"
                },
                {
                    "id": "51762680080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-13T09:10:03.174Z",
            "finishedTime": "2022-12-13T09:10:04.276Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f29d0700-26ae-4dce-9ac6-7cc7f5ecaad4"
        },
        {
            "taskId": "add1797e-2f98-4e7a-9894-c71d6b5640bb",
            "products": [
                {
                    "id": "51762690080",
                    "productType": "BASE"
                },
                {
                    "id": "51762700080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-13T09:13:24.370Z",
            "finishedTime": "2022-12-13T09:13:25.019Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/add1797e-2f98-4e7a-9894-c71d6b5640bb"
        },
        {
            "taskId": "f66f8c0c-61e7-4fe5-8876-8b157e337de3",
            "products": [
                {
                    "id": "51762790080",
                    "productType": "BASE"
                },
                {
                    "id": "51762800080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-16T08:06:14.070Z",
            "finishedTime": "2022-12-16T08:06:15.128Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f66f8c0c-61e7-4fe5-8876-8b157e337de3"
        },
        {
            "taskId": "e275f7dc-e6d5-4f97-bdb1-4e352ddf9c0c",
            "products": [
                {
                    "id": "51762810080",
                    "productType": "BASE"
                },
                {
                    "id": "51762820080",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-16T08:07:28.436Z",
            "finishedTime": "2022-12-16T08:07:29.335Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/e275f7dc-e6d5-4f97-bdb1-4e352ddf9c0c"
        },
        {
            "taskId": "f0711fb9-e127-4120-be8e-15d797743fdf",
            "products": [
                {
                    "id": "52167640080",
                    "externalReferenceId": "external-reference-id-a722592b-04dc-4516-a36b-45f375c510ee",
                    "productType": "BASE"
                },
                {
                    "id": "52167650080",
                    "externalReferenceId": "external-reference-id-a722592b-04dc-4516-a36b-45f375c510ee",
                    "productType": "VARIATION"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-22T01:57:16.004Z",
            "finishedTime": "2022-12-22T01:57:17.245Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/f0711fb9-e127-4120-be8e-15d797743fdf"
        },
        {
            "taskId": "473bc471-a544-4376-8faf-72841e24671f",
            "products": [
                {
                    "id": "52167640080"
                }
            ],
            "requestType": "UPDATE_PRODUCT",
            "taskStatus": "FAILED",
            "receivedTime": "2022-12-22T01:59:50.563Z",
            "finishedTime": "2022-12-22T01:59:50.738Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/473bc471-a544-4376-8faf-72841e24671f"
        },
        {
            "taskId": "ca72117f-5e7d-4872-a210-25d095c8d347",
            "products": [
                {
                    "id": "51945740080",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-29T07:01:50.798Z",
            "finishedTime": "2022-12-29T07:01:52.544Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/ca72117f-5e7d-4872-a210-25d095c8d347"
        },
        {
            "taskId": "fcac98e2-ee7e-47a5-86ea-3f39fb740148",
            "products": [
                {
                    "id": "51945750080",
                    "productType": "INDIVIDUAL"
                }
            ],
            "requestType": "CREATE_PRODUCT",
            "taskStatus": "COMPLETED",
            "receivedTime": "2022-12-29T07:16:55.099Z",
            "finishedTime": "2022-12-29T07:16:55.961Z",
            "uri": "https://dispatch-test.digitalriver.com/products/tasks/fcac98e2-ee7e-47a5-86ea-3f39fb740148"
        }
    ],
    "totalSize": 14,
    "searchCriteria": {
        "beginReceivedTime": "2022-12-06T21:19:06.927Z",
        "endReceivedTime": "2023-01-05T21:19:06.927Z",
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

### Limit

This optional `limit` query parameter filters a list on the `finishedTime` field. The value can be a string with an ISO-8601 UTC format datetime (for example, `yyyy-mm-ddT00:00:00.000Z`).  The response displays results for 30 days before and including the specified date.\
\
`GET 'https://api.digitalriver.com/v1/products/tasks?endReceivedTime=2022-10-31T00:00:00.000Z?limit=10'`

### Product identifier

This optional `productId` query parameter filters a list by the [product identifier](../common-shoppers-and-admin-apis-reference/product-identifier.md) (`productId`). \
\
`GET 'https://api.digitalriver.com/v1/products/tasks?productId={productId or productERID}'`

{% hint style="info" %}
**Note**: If you specify `productERID`, you must include `x-erid-as-pid=true` in the request header.
{% endhint %}

### Starting after

This optional `startingAfter` query parameter filters a list based on `taskId`.\
Use the `startingAfter` value in the `nextPage` object from the previous request when requesting the next page of tasks.\
\
`GET 'https://api.digitalriver.com/v1/products/tasks?startingAfter=`[`{taskId}`](tasks.md#task-identifier)`'`

### Ending before

This optional `endingBefore` query parameter filters a list based on `taskId`. Use the `endingBefore` value in the `previousPage` object from the previous request when requesting the next page of tasks.\
\
`GET 'https://api.digitalriver.com/v1/products/tasks?endingefore=`[`{taskId}`](tasks.md#task-identifier)`'`

### Task status

This query `taskStatus` parameter filters a list based on the [`taskStatus`](tasks.md#task-status). You can add multiple values separated by a comma. The request returns tasks with the specified values.\
\
`GET 'https://api.digitalriver.com/v1/products/tasks?staskStatus=COMPLETED,FAILED'`
