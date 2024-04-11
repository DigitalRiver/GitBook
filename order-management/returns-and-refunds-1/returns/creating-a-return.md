---
description: >-
  Learn how notify Digital River of returns when you have a third-party
  fulfiller.
---

# Third party coordinated returns

If you're using a third-party reverse logistics service, then you can use the [Returns API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns) to help manage the returns and refunds process.

Once a customer's request to return purchased products is approved, use this API to first notify Digital River that you authorized a return and then, after the returned goods have been received, inspected, and signed off, move them into an accepted state.

Once all the authorized goods are accepted, Digital River creates one or more refund pending events that you can listen for with a [configurable webhook](../../events-and-webhooks-1/webhooks/creating-a-webhook.md).

On this page, you'll find information on:

* [Authorizing returns](creating-a-return.md#authorizing-returns)
* [Accepting returns](creating-a-return.md#accepting-returns)
* [What conditions trigger a refund](creating-a-return.md#what-conditions-trigger-a-refund)

## Authorizing returns

If customers request a return, and you authorize their request, your order management system should [define](creating-a-return.md#defining-a-return-authorization) and [create](creating-a-return.md#creating-a-return-authorization) a return authorization in Digital River's system.

### Defining a return authorization

In a [`POST /returns`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createReturns), you're required to provide an [order identifier](creating-a-return.md#order-identifier) as well as [line item data](creating-a-return.md#items). You can optionally specify a return [reason and location](creating-a-return.md#reason-and-location).

#### Order identifier

The request must contain the [`orderId`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) associated with the products that are being returned.

#### Items

For each `items[]`, define `itemId` or [`skuId`](../../../product-management/creating-and-updating-skus.md#unique-identifier) and the `quantity` of goods authorized for return.

#### Reason and location

You can optionally provide a return `reason` and `location`. Both of these are pass-through values, but can be useful for tracking, customer notifications, and record keeping purposes.

### Creating a return authorization

To create a return authorization, send your [secret API key](../../../developer-resources/api-structure.md#confidential-keys) and [request payload](creating-a-return.md#defining-a-return-authorization) in a `POST /returns`.

```json
curl --location --request POST 'https://api.digitalriver.com/returns' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{secretKey}}' \
...
--data-raw '{
  "orderId": "215146200336",
  "reason": "Incorrect size",
  "items":
    [
      {
        "itemId": "139723170336",
        "quantity": "2"
      },
      {
        "itemId": "139723180336",
        "quantity": "2"
      }
    ]
}'
```

If  `items[].quantity` exceeds the quantity that's eligible for return, you receive the following error:

{% code title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "quantity_too_large",
            "parameter": "items[0].qty",
            "message": "Return quantity is larger than order quantity"
        }
    ]
}
```
{% endcode %}

### Return authorization

Once the request is successfully submitted, Digital River sets the `state` of the [return](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns) and each of its `items[]` to `created` and generates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a `type` of `return.created`.

In `items[]`, the `quantityAccepted` represents the number of products that have been received and accepted. In the `201 Created`, it's always `0` but may increase, depending on the results of the [return acceptance process](creating-a-return.md#accepting-returns).

Each `items[]` in the response contains a  `skuId` , which you can use to make a [`GET/skus/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveSkus) request and access [product data](../../../product-management/skus.md).

{% code title="Return " %}
```javascript
{
    "id": "ret_ea359ea9-b768-42fd-a48a-dc57f59b3d50",
    "createdTime": "2022-02-02T16:57:13Z",
    "currency": "USD",
    "items": [
        {
            "itemId": "139723170336",
            "amount": 21.62,
            "quantity": 2,
            "quantityAccepted": 0,
            "skuId": "5cd94c9b-82d7-4194-bd3f-48f33c6b7420",
            "state": "created"
        },
        {
            "itemId": "139723180336",
            "amount": 21.62,
            "quantity": 2,
            "quantityAccepted": 0,
            "skuId": "5c52b10b-4656-4234-8d0e-9e63f012bc72",
            "state": "created"
        }
    ],
    "orderId": "215146200336",
    "reason": "Incorrect size",
    "state": "created",
    "liveMode": false
}n
```
{% endcode %}

## Accepting returns

If customers follow the instructions you provided on how to return their goods, and they arrive in the expected quantity and quality, you'll need to notify Digital River that the return is accepted so that we can issue a [refund](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds).

How you do this depends on whether the goods arrive in a [single shipment](creating-a-return.md#single-shipment-returns) or [multiple shipments](creating-a-return.md#multiple-shipment-returns).

### Single shipment returns

If the full quantity of goods specified in the [return authorization](creating-a-return.md#return-authorization) arrives in a single shipment, and you or your third-party reverse logistics service accepts their condition, send a `POST /returns/{id}` with `state` set to `accepted` in the body of the request:

```json
curl --location --request POST 'https://api.digitalriver.com/returns/ret_e4dc1cb7-f8ac-488d-99bf-e14fa1162482' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{secretKey}}' \
...
--data-raw '{
    "state": "accepted"
}'
```

Digital River handles your request by setting the `state` of the [return](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns) and each of its `items[]` to `accepted`, and then creating two types of [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events), `return.accepted` and `refund.pending`.

If the refund is successfully processed, `refund.complete` is next created. If, for some reason, it's not, then you'll need to handle `refund.failed`.

{% tabs %}
{% tab title="Return" %}
```javascript
{
    "id": "ret_e4dc1cb7-f8ac-488d-99bf-e14fa1162482",
    "createdTime": "2022-02-17T21:12:33Z",
    "currency": "USD",
    "items": [
        {
            "itemId": "142042680336",
            "amount": 21.61,
            "quantity": 2,
            "quantityAccepted": 2,
            "skuId": "2cf3d5c0-c8ef-4df7-9e6f-470b469583f9",
            "state": "accepted"
        },
        {
            "itemId": "142042690336",
            "amount": 48.61,
            "quantity": 3,
            "quantityAccepted": 3,
            "skuId": "b3bccc18-cac8-4066-8304-e7d0ea615edd",
            "state": "accepted"
        }
    ],
    "orderId": "217222390336",
    "reason": "Damaged Goods",
    "state": "accepted",
    "liveMode": false
}
```
{% endtab %}

{% tab title="return.accepted" %}
```javascript
{
    "id": "e2df70ae-bf12-4ce0-bb5d-54ec2dddfcd3",
    "type": "return.accepted",
    "data": {
        "object": {
            "id": "ret_e4dc1cb7-f8ac-488d-99bf-e14fa1162482",
            "createdTime": "2022-02-17T21:12:33Z",
            "currency": "USD",
            "items": [
                {
                    "itemId": "142042680336",
                    "amount": 21.61,
                    "quantity": 2,
                    "quantityAccepted": 2,
                    "skuId": "2cf3d5c0-c8ef-4df7-9e6f-470b469583f9",
                    "state": "accepted"
                },
                {
                    "itemId": "142042690336",
                    "amount": 48.61,
                    "quantity": 3,
                    "quantityAccepted": 3,
                    "skuId": "b3bccc18-cac8-4066-8304-e7d0ea615edd",
                    "state": "accepted"
                }
            ],
            "orderId": "217222390336",
            "reason": "Damaged Goods",
            "state": "accepted",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2022-02-17T21:13:19.145329Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb",
        "9666a0f9-d2a5-4eba-8b56-ecf7e87bb84c",
        "f666c369-b0bb-4412-a5ca-bf37bef3b982"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}

{% tab title="refund.pending" %}
```javascript
{
    "id": "bc74b73e-970b-4466-ba78-93d3de28635b",
    "type": "refund.pending",
    "data": {
        "object": {
            "id": "re_8d150ec4-c107-45b2-8637-edc1c9338856",
            "createdTime": "2022-02-17T21:13:12Z",
            "currency": "USD",
            "items": [
                {
                    "amount": 21.6,
                    "quantity": 2,
                    "skuId": "2cf3d5c0-c8ef-4df7-9e6f-470b469583f9",
                    "itemId": "142042680336"
                },
                {
                    "amount": 48.6,
                    "quantity": 3,
                    "skuId": "b3bccc18-cac8-4066-8304-e7d0ea615edd",
                    "itemId": "142042690336"
                }
            ],
            "orderId": "217222390336",
            "reason": "Damaged Goods",
            "refundedAmount": 0.0,
            "state": "pending",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2022-02-17T21:13:16.609757Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb",
        "8044a862-e7c9-4a8f-a3bb-b6b987a2be9e",
        "9666a0f9-d2a5-4eba-8b56-ecf7e87bb84c",
        "f666c369-b0bb-4412-a5ca-bf37bef3b982"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

### Multiple shipment returns

If the goods in the [return authorization](creating-a-return.md#return-authorization) don't all arrive in a single shipment, you or your third-party reverse logistics service can accept each item separately.

For example, you might have created a return authorization that contains two `items[]`.

{% code title="Return authorization" %}
```javascript
{
    "id": "ret_b4e2a7f9-82f5-4133-bbcf-4423e8fae4d1",
    "createdTime": "2022-02-21T19:06:23Z",
    "currency": "USD",
    "items": [
        {
            "itemId": "142282650336",
            "amount": 21.62,
            "quantity": 2,
            "quantityAccepted": 0,
            "skuId": "8dfbf79b-658d-4ee4-bada-9c7f476b84e4",
            "state": "created"
        },
        {
            "itemId": "142282660336",
            "amount": 64.83,
            "quantity": 3,
            "quantityAccepted": 0,
            "skuId": "66ec1069-7afe-48f6-87f2-4df8c723eef0",
            "state": "created"
        }
    ],
    "orderId": "217431410336",
    "reason": "Products don't match description",
    "state": "created",
    "liveMode": false
}
```
{% endcode %}

For the first `items[]` in this example, the full, authorized `quantity` might arrive in an initial shipment that doesn't contain any products from the second `items[]`.

To handle this, in the body of an [update return request](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/updateReturns), set the `quantity` of the first `items[]` to the appropriate value and it's `state` to `accepted`.

```json
curl --location --request POST 'https://api.digitalriver.com/returns/ret_b4e2a7f9-82f5-4133-bbcf-4423e8fae4d1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{secretKey}}' \
...
--data-raw '{
    "items": [
        {
            "itemId": "142282650336",
            "quantity": "2",
            "state":"accepted"
        }
    ]
}'
```

Since the second `items[]` is not yet `accepted`, the `refund.pending` event isn't created.

{% code title="Return" %}
```javascript
{
    "id": "ret_b4e2a7f9-82f5-4133-bbcf-4423e8fae4d1",
    "createdTime": "2022-02-21T19:06:23Z",
    "currency": "USD",
    "items": [
        {
            "itemId": "142282650336",
            "amount": 21.61,
            "quantity": 2,
            "quantityAccepted": 2,
            "skuId": "8dfbf79b-658d-4ee4-bada-9c7f476b84e4",
            "state": "accepted"
        },
        {
            "itemId": "142282660336",
            "amount": 64.82,
            "quantity": 3,
            "quantityAccepted": 0,
            "skuId": "66ec1069-7afe-48f6-87f2-4df8c723eef0",
            "state": "created"
        }
    ],
    "orderId": "217431410336",
    "reason": "Products don't match description",
    "state": "created",
    "liveMode": false
}
```
{% endcode %}

If the remainder of products authorized for return arrive in a second shipment, then submit another update request that sets the `quantity` of that `items[]` to the appropriate value and it's `state` to `accepted`.

```json
curl --location --request POST 'https://api.digitalriver.com/returns/ret_b4e2a7f9-82f5-4133-bbcf-4423e8fae4d1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{secretKey}}' \
...
--data-raw '{
    "items": [
        {
            "itemId": "142282660336",
            "quantity": "3",
            "state":"accepted"
        }
    ]
}'
```

A successful request moves the [return's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns) `state` to `accepted` and generates `return.accepted` as well as one or more `refund.pending` events, each containing unique [refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds).

{% tabs %}
{% tab title="Return" %}
```javascript
{
    "id": "ret_b4e2a7f9-82f5-4133-bbcf-4423e8fae4d1",
    "createdTime": "2022-02-21T19:06:23Z",
    "currency": "USD",
    "items": [
        {
            "itemId": "142282650336",
            "amount": 21.61,
            "quantity": 2,
            "quantityAccepted": 2,
            "skuId": "8dfbf79b-658d-4ee4-bada-9c7f476b84e4",
            "state": "accepted"
        },
        {
            "itemId": "142282660336",
            "amount": 64.82,
            "quantity": 3,
            "quantityAccepted": 3,
            "skuId": "66ec1069-7afe-48f6-87f2-4df8c723eef0",
            "state": "accepted"
        }
    ],
    "orderId": "217431410336",
    "reason": "Products don't match description",
    "state": "accepted",
    "liveMode": false
}
```
{% endtab %}

{% tab title="return.accepted" %}
```javascript
{
    "id": "a09bcf72-f952-41ad-95c2-ee6706a3b767",
    "type": "return.accepted",
    "data": {
        "object": {
            "id": "ret_b4e2a7f9-82f5-4133-bbcf-4423e8fae4d1",
            "createdTime": "2022-02-21T19:06:23Z",
            "currency": "USD",
            "items": [
                {
                    "itemId": "142282650336",
                    "amount": 21.61,
                    "quantity": 2,
                    "quantityAccepted": 2,
                    "skuId": "8dfbf79b-658d-4ee4-bada-9c7f476b84e4",
                    "state": "accepted"
                },
                {
                    "itemId": "142282660336",
                    "amount": 64.82,
                    "quantity": 3,
                    "quantityAccepted": 3,
                    "skuId": "66ec1069-7afe-48f6-87f2-4df8c723eef0",
                    "state": "accepted"
                }
            ],
            "orderId": "217431410336",
            "reason": "Products don't match description",
            "state": "accepted",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2022-02-21T19:12:16.969768Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb",
        "9666a0f9-d2a5-4eba-8b56-ecf7e87bb84c",
        "f666c369-b0bb-4412-a5ca-bf37bef3b982"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}

{% tab title="refund.pending (1)" %}
```java
{
    "id": "fe9705a5-c8bf-4420-93e3-df1941af5434",
    "type": "refund.pending",
    "data": {
        "object": {
            "id": "re_b084add2-36c3-4301-8443-91a8c5c8a610",
            "createdTime": "2022-02-21T19:06:39Z",
            "currency": "USD",
            "items": [
                {
                    "amount": 21.6,
                    "quantity": 2,
                    "refundedAmount": 21.6,
                    "skuId": "8dfbf79b-658d-4ee4-bada-9c7f476b84e4",
                    "itemId": "142282650336"
                }
            ],
            "orderId": "217431410336",
            "reason": "Products don't match description",
            "refundedAmount": 21.6,
            "state": "succeeded",
            "liveMode": false,
            "charges": [
                {
                    "id": "3efabd66-9f1c-4ec4-b0fc-ac8d8bda31b0",
                    "captured": true,
                    "refunded": true,
                    "refunds": [
                        {
                            "createdTime": "2022-02-21T19:07:57Z",
                            "amount": 21.6,
                            "state": "complete"
                        }
                    ],
                    "sourceId": "8816e6b9-c865-4088-a68b-661a0198141b"
                }
            ]
        }
    },
    "liveMode": false,
    "createdTime": "2022-02-21T19:12:17.194945Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb",
        "8044a862-e7c9-4a8f-a3bb-b6b987a2be9e",
        "9666a0f9-d2a5-4eba-8b56-ecf7e87bb84c",
        "f666c369-b0bb-4412-a5ca-bf37bef3b982"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}

{% tab title="refund.pending (2) " %}
```javascript
{
    "id": "a0d9795e-c75a-40a7-98c8-f3be3de52fdc",
    "type": "refund.pending",
    "data": {
        "object": {
            "id": "re_9bab4039-25f2-42c6-b3c4-a168b4d0b189",
            "createdTime": "2022-02-21T19:11:58Z",
            "currency": "USD",
            "items": [
                {
                    "amount": 64.81,
                    "quantity": 3,
                    "skuId": "66ec1069-7afe-48f6-87f2-4df8c723eef0",
                    "itemId": "142282660336"
                }
            ],
            "orderId": "217431410336",
            "reason": "Products don't match description",
            "refundedAmount": 0.0,
            "state": "pending",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2022-02-21T19:12:16.79817Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb",
        "8044a862-e7c9-4a8f-a3bb-b6b987a2be9e",
        "9666a0f9-d2a5-4eba-8b56-ecf7e87bb84c",
        "f666c369-b0bb-4412-a5ca-bf37bef3b982"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

## What conditions trigger a refund

[Refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) are only created when a [return's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns) `state` moves to `accepted`. For this to occur, each `items[].state` in that resource must also be `accepted`. To make that happen, the authorized `quantity` of each `items[]` must be equal to its `quantityAccepted`.

In other words, the [Returns API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Returns) is designed to handle the scenario where the full quantity of goods in a [return authorization](creating-a-return.md#return-authorization) is sent back and approved and only then is the customer issued a refund.&#x20;

If you'd like to provide refunds on partial returns, then your application should use the [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds). For details, refer to [Issuing refunds](../refunds/issuing-refunds.md).

{% code title="Return" %}
```javascript
{
    "id": "ret_b4e2a7f9-82f5-4133-bbcf-4423e8fae4d1",
    "createdTime": "2022-02-21T19:06:23Z",
    "currency": "USD",
    "items": [
        {
            "itemId": "142282650336",
            "amount": 21.61,
            "quantity": 2,
            "quantityAccepted": 2,
            "skuId": "8dfbf79b-658d-4ee4-bada-9c7f476b84e4",
            "state": "accepted"
        },
        {
            "itemId": "142282660336",
            "amount": 64.82,
            "quantity": 3,
            "quantityAccepted": 3,
            "skuId": "66ec1069-7afe-48f6-87f2-4df8c723eef0",
            "state": "accepted"
        }
    ],
    "orderId": "217431410336",
    "reason": "Products don't match description",
    "state": "accepted",
    "liveMode": false
}
```
{% endcode %}
