---
description: Learn how to verify the successful completion of a specific product task.
---

# Getting the latest information on a product task

The following [`GET /v1/products/tasks/{taskId}`](https://www.digitalriver.com/docs/commerce-admin-api/#tag/Get-Product-Task-Status-\(Synchronous-API\)/paths/\~1products\~1tasks\~1%7BtaskId%7D/get) request gets the latest product information for an asynchronous task. It indicates whether the request was completed successfully and lists all products associated with that task. This request requires the task identifier (`taskId`) provided in the response when you [created or updated the product](../manage-products-asynchronous-api/creating-or-updating-a-product.md).

{% hint style="info" %}
You cannot [change or modify a product](getting-the-latest-information-on-a-product-task.md#updating-a-product) until the [create product request](getting-the-latest-information-on-a-product-task.md#creating-a-base-or-individual-product) completes successfully.
{% endhint %}

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```
curl --location --request GET 'https://api.digitalriver.com/v1/products/tasks/{taskId}' \
--header 'Authorization: Basic <API_key>' \
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
The response returns the [product data](../../../general-resources/admin-apis-reference/tasks.md#products), the [task identifier (`taskId`)](../../../general-resources/admin-apis-reference/tasks.md#task-identifier), the [request type (`requestType`)](../../../general-resources/admin-apis-reference/tasks.md#request-type), and [task status (`taskStatus`)](../../../general-resources/admin-apis-reference/tasks.md#task-status) in the [synchronous ](../getting-started.md#asynchronous-and-synchronous-calls)response.&#x20;

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
