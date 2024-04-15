---
description: >-
  Learn about what a charge is, how it's created, and how captures, cancels, and
  refunds work
---

# Charges

A [charge ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges)represents a payment authorization. The [charge creation process](./#how-a-charge-is-created) is handled by Digital River. Throughout a [charge's lifecycle](./#the-charge-lifecycle), the object can contain one or more [captures, cancels, and refunds](./#how-captures-cancels-and-refunds-work).

## How a charge is created

Whether you're using [Low-code checkouts](../../../integration-options/low-code-checkouts/) or [Direct Integrations](../../../integration-options/checkouts/), the payment authorization process remains the same.&#x20;

At the time of [order creation](../../creating-and-updating-an-order.md), Digital River creates a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) whose `amount` is equal to the associated [source's](../../../payments/payment-sources/) `amount` and then submits an authorization request that gets routed to the appropriate payment provider.&#x20;

For example, as you [build a Direct Integrations' checkout](../../../integration-options/checkouts/creating-checkouts/), customers might provide credit card information during the [payment collection stage](../../../integration-options/checkouts/creating-checkouts/#collecting-payment). This information is then used to [create a primary source](../../../payments/payment-sources/using-the-source-identifier.md#creating-primary-sources) that you [associate with the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts). After you [convert the checkout to an order](../../creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), Digital River creates a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) and then sends an authorization request to a payment processor who forwards it to a payment provider. If the request is approved by the payment provider, then Digital River moves the charge's  [`state`](./#the-charge-lifecycle) to `capturable` and creates an `order.charge.capturable` [event](../../events-and-webhooks-1/events-1/).&#x20;

{% hint style="info" %}
Once a provider authorizes payment, the charge on a credit card typically remains `capturable` for seven days.
{% endhint %}

A [charge's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) `amount` represents the initial authorization on a customer's payment method. But it's ultimately all the [captures, cancellations, and refunds](./#how-captures-cancels-and-refunds-work) during [an order's lifecycle](../the-order-lifecycle.md) that determines how much a customer pays.

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "178727320336",
    ...
    "state": "accepted",
    ...
    "payment": {
        "charges": [
            {
                "id": "b469adb4-d9d1-4baa-80b1-e55c26feb4e8",
                "createdTime": "2020-07-02T20:10:47Z",
                "currency": "USD",
                "amount": 145.16,
                "state": "capturable",
                "captured": false,
                "refunded": false,
                "sourceId": "9d9cff59-2b43-4b0a-a171-f49a243e5ea8"
            }
        ],
        ...
    }
    ...
}
```
{% endtab %}
{% endtabs %}

## How captures, cancels, and refunds work

An [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `payment.charges[]` contains an enduring record of all the [`captures[]`](./#captures), [`cancels[]`](./#cancels), and [`refunds[]`](./#refunds) that occur during that [order's lifecycle](../the-order-lifecycle.md).

{% code title="Order" %}
```javascript
{
    "id": "178728710336",
    "createdTime": "2020-07-02T21:43:28Z",
    ...
    "payment": {
        "charges": [
            {
                "id": "c23d5317-3410-4abb-af86-8c8570b9dc90",
                "createdTime": "2020-07-02T21:43:30Z",
                "currency": "USD",
                "amount": 145.16,
                "state": "complete",
                "captured": true,
                "captures": [
                    {
                        "id": "075224cd-0d07-440f-9c16-a17f16cb9692",
                        "createdTime": "2020-07-02T21:50:35Z",
                        "amount": 64.52,
                        "state": "complete"
                    },
                    {
                        "id": "966387d3-3693-4d35-bf8e-9f190b58e2a8",
                        "createdTime": "2020-07-02T21:50:35Z",
                        "amount": 24.2,
                        "state": "complete"
                    }
                ],
                "refunded": true,
                "refunds": [
                    {
                        "createdTime": "2020-07-02T22:39:00Z",
                        "amount": 53.77,
                        "state": "complete"
                    }
                ],
                "cancels": [
                    {
                        "id": "5c13a17a-8c30-4550-be27-ddd84894b45e",
                        "createdTime": "2020-07-02T21:54:51Z",
                        "amount": 32.26,
                        "state": "complete"
                    },
                    {
                        "id": "58d9ff72-d043-4e00-9552-fb6dd8144a6c",
                        "createdTime": "2020-07-02T21:54:51Z",
                        "amount": 24.18,
                        "state": "complete"
                    }
                ],
                "sourceId": "9d9cff59-2b43-4b0a-a171-f49a243e5ea8",
                "type": "customer_initiated"
            }
        ],
    ...
}
```
{% endcode %}

All captures, cancels, and refunds have an initial `state` of `pending` and then either transition to `complete` or `failed`. With each of these `state` transitions, a corresponding [event](../../events-and-webhooks-1/events-1/) is created.

For example, when you initiate the [payment cancellation process](../../informing-digital-river-of-a-fulfillment.md), Digital River creates an `order.charge.cancel.pending` event. This is eventually followed either by [`order.charge.cancel.complete`](../../informing-digital-river-of-a-fulfillment.md#successful-charge-captures) or [`order.charge.cancel.failed`](../../informing-digital-river-of-a-fulfillment.md#failed-charge-captures).

During an [order's lifecycle](../the-order-lifecycle.md), an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `totalAmount` and each of its `payment.charges[].amount`(s) remain unaltered. The actual amount a payment method is debited or credited is reflected by `capturedAmount` and `refundedAmount`, respectively.

{% code title="Order" %}
```javascript
{
    "id": "178728710336",
    ...
    "totalAmount": 145.16,
    ...
    "refundedAmount": 53.77,
    "state": "complete",
    ...
    "charges": [
        {
            "id": "c23d5317-3410-4abb-af86-8c8570b9dc90",
            "createdTime": "2020-07-02T21:43:30Z",
            "currency": "USD",
            "amount": 145.16,
            "state": "processing",
            "captured": true,
            "captures": [
                ...
            ],
            "refunded": true,
            "refunds": [
                {
                    "createdTime": "2020-07-02T22:39:00Z",
                    "amount": 53.77,
                    "state": "complete"
                }
            ],
            "cancels": [
                ...
            ],
            "sourceId": "9d9cff59-2b43-4b0a-a171-f49a243e5ea8"
        }
    ],
    ...
    "capturedAmount": 88.72,
    "cancelledAmount": 56.44,
    "availableToRefundAmount": 34.94,
    ...
}
```
{% endcode %}

### Captures

A capture represents the settling of an authorization. In other words, how much a customer's payment method is debited. Some payment methods require that a [charge's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) full `amount` be captured all at once, while others permit multiple captures.

When you submit a [`POST/fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments) that specifies an `items[].quantity`, Digital River attempts to capture payment.&#x20;

{% hint style="info" %}
For more details, refer to the [Capturing and cancelling payment charges](../../informing-digital-river-of-a-fulfillment.md) page.&#x20;
{% endhint %}

The following [`POST/fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments) seeks to partially capture payment on an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).&#x20;

{% tabs %}
{% tab title="POST/fulfillments" %}
```
curl --location --request POST 'https://api.digitalriver.com/fulfillments' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
  "orderId": "178728710336",
  "items": [
    {
      "itemId": "98014170336",
      "quantity": 1
    },
    {
      "itemId": "98014180336",
      "quantity": 2
    }
  ]
}'
```
{% endtab %}
{% endtabs %}

Once submitted, you can be notified that the capture process has begun by listening for the `order.charge.capture.pending` event.

In the above example, the `POST/fulfillments` informed our payment services that two line items were fulfilled. As a result, the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) contains two `captures[]`, each with a unique `id` and a captured `amount`. As more goods are fulfilled, and you respond by submitting additional `POST/fulfillments`, an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `capturedAmount` provides a running total of how much has been settled.

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "178728710336",
    ...
    "payment": {
        "charges": [
            {
                "id": "c23d5317-3410-4abb-af86-8c8570b9dc90",
                "createdTime": "2020-07-02T21:43:30Z",
                "currency": "USD",
                "amount": 145.16,
                "state": "complete",
                "captured": true,
                "captures": [
                    {
                        "id": "075224cd-0d07-440f-9c16-a17f16cb9692",
                        "createdTime": "2020-07-02T21:50:35Z",
                        "amount": 64.52,
                        "state": "complete"
                    },
                    {
                        "id": "966387d3-3693-4d35-bf8e-9f190b58e2a8",
                        "createdTime": "2020-07-02T21:50:35Z",
                        "amount": 24.2,
                        "state": "complete"
                    }
                ],
                ...
                "sourceId": "9d9cff59-2b43-4b0a-a171-f49a243e5ea8",
                "type": "customer_initiated"
            }
        ],
        "sources": [
            {
                "id": "9d9cff59-2b43-4b0a-a171-f49a243e5ea8",
                "type": "creditCard",
                "amount": 145.16,
                ...
                },
                "creditCard": {
                    "brand": "Visa",
                    "expirationMonth": 7,
                    "expirationYear": 2027,
                    "lastFourDigits": "1111"
                }
            }
        ],
        ...
    },
    ...
    "capturedAmount": 88.72,
    ...
}
```
{% endtab %}
{% endtabs %}

In this example, since the order's [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) has a `type` of `creditCard`, each `captures[]` will (typically) briefly transition to a `state` of `pending` before becoming `complete`. Once a capture moves into this `state`, Digital River creates an [`order.charge.capture.complete`](../../informing-digital-river-of-a-fulfillment.md#successful-charge-captures) event.

### Cancels

A cancel negates all or part of a payment authorization. Cancels don't result in the debiting or crediting of a customer's payment method. That same underlying payment method determines whether a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) can be partially cancelled or only supports full cancellations.

When you send a [`POST/fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createFulfillments) that specifies an `items[].cancelQuantity`, Digital River attempts to cancel payment.

{% hint style="info" %}
For more details, refer to the [Capturing and cancelling payment charges](../../informing-digital-river-of-a-fulfillment.md) page.&#x20;
{% endhint %}

{% tabs %}
{% tab title="POST/fulfillments" %}
```
curl --location --request POST 'https://api.digitalriver.com/fulfillments' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API_key>' \
...
--data-raw '{
  "orderId": "178728710336",
  "items": [
    {
      "itemId": "98014170336",
      "cancelQuantity": 1
    },
    {
      "itemId": "98014180336",
      "cancelQuantity": 1
    }
  ]
}'
```
{% endtab %}
{% endtabs %}

Once submitted, you can be notified that the cancellation process has begun by listening for the `order.charge.cancel.pending` event.

In the above example, the `POST/fulfillments` informed our payment services that two line items were cancelled. As a result, the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) contains two `cancels[]`, each with a unique `id` and a cancelled `amount`.

In this particular example, since all of the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `charges[]` are either captured or cancelled, the order's [`state`](../the-order-lifecycle.md#order-states-and-events) moves to `complete` and an [`order.complete`](../../informing-digital-river-of-a-fulfillment.md#handling-the-order-complete-event) event is triggered.&#x20;

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "178728710336",
    ...
    "totalAmount": 145.16,
    ...
    "state": "complete",
    ...
    "payment": {
        "charges": [
            {
                "id": "c23d5317-3410-4abb-af86-8c8570b9dc90",
                "createdTime": "2020-07-02T21:43:30Z",
                "currency": "USD",
                "amount": 145.16,
                "state": "processing",
                "captured": true,
                "captures": [
                    ...
                ],
                "refunded": false,
                "cancels": [
                    {
                        "id": "5c13a17a-8c30-4550-be27-ddd84894b45e",
                        "createdTime": "2020-07-02T21:54:51Z",
                        "amount": 32.26,
                        "state": "complete"
                    },
                    {
                        "id": "58d9ff72-d043-4e00-9552-fb6dd8144a6c",
                        "createdTime": "2020-07-02T21:54:51Z",
                        "amount": 24.18,
                        "state": "complete"
                    }
                ],
                "sourceId": "9d9cff59-2b43-4b0a-a171-f49a243e5ea8"
            }
        ],
    ...
    }
    "capturedAmount": 88.72,
    "cancelledAmount": 56.44,
    "availableToRefundAmount": 88.71,
    ...
}
```
{% endtab %}
{% endtabs %}

### Refunds

A refund represents funds returned to a customer. Once funds have been [captured](./#captures), all or part of the captured amount can be refunded. All the refunds on a particular [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) are contained in its `refunds[]` array.

You should be aware however that `refunds[]` in [charges](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) are not the same object as [refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) you create when submitting [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds). This is because, for batch processing purposes, Digital River often aggregates charge `refunds[]`.

{% hint style="info" %}
For details on how to create refunds, refer to the [Issuing refunds](../../returns-and-refunds-1/refunds/issuing-refunds.md) page.&#x20;
{% endhint %}

The following attempts to demonstrate this distinction:

{% tabs %}
{% tab title="Refunds" %}
The following [`GET/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listRefunds) request is searching for all the [refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) created by a client system that are associated with a specific [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).&#x20;

```
curl --location --request GET 'https://api.digitalriver.com/refunds?orderId=178728710336' \
--header 'Authorization: Bearer <API_key>' \
```

In the response, `data[]` lists these [refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listRefunds). In this particular example, only a single [refund](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) has been created by a client system.

{% code title="Refunds" %}
```javascript
{
    "hasMore": false,
    "data": [
        {
            "id": "re_40af9cbd-0f38-4362-9e24-c6338f3795c4",
            ...
            "items": [
                {
                    "amount": 21.51,
                    "quantity": 1,
                    "refundedAmount": 21.51,
                    ...
                },
                {
                    "amount": 32.26,
                    "quantity": 1,
                    "refundedAmount": 32.26,
                    ...
                }
            ],
            "orderId": "178728710336",
            ...
            "refundedAmount": 53.769999999999996,
            ...
        }
    ]
}
```
{% endcode %}
{% endtab %}

{% tab title="Order" %}
The following [`GET/orders/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveRefunds) request retrieves the same [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders).

```
curl --location --request GET 'https://api.digitalriver.com/orders/178728710336' \
--header 'Authorization: Bearer <API_key>' \
```

The [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `payment.charges[].refunds[]` array contains a single element. But, despite being associated with the same [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) and despite have nearly identical amount values, this [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges)-level refund is not the same object as the [refund](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) created by the client system.

```javascript
{
    "id": "178728710336",
    ...
    "payment": {
        "charges": [
            {
                "id": "c23d5317-3410-4abb-af86-8c8570b9dc90",
                ...
                "refunds": [
                    {
                        "createdTime": "2020-07-02T22:39:00Z",
                        "amount": 53.77,
                        "state": "complete"
                    }
                ],
                ...    
            }
        ],
    ...
    "refundedAmount": 53.77,
    ...
}
```
{% endtab %}

{% tab title="Charge" %}
The following [`GET/charges/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveCharges) request passes the [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) identifier from the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) as a a path parameter.

```
curl --location --request GET 'https://api.digitalriver.com/charges/c23d5317-3410-4abb-af86-8c8570b9dc90' \
--header 'Authorization: Bearer <API_key>' \
```

The response contains an array of charge `refunds[]`, each with a unique `id`. Note that the `id` of the charge-level refund is not the same as the `id` of the client system created [refund](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds).

```javascript
{
    "id": "c23d5317-3410-4abb-af86-8c8570b9dc90",
    ...
    "orderId": "178728710336",
    ...
    "refunded": true,
    "refunds": [
        {
            "id": "5e32af54-aff5-49a8-b72e-37aa8e3d03af",
            "createdTime": "2020-07-02T22:39:00Z",
            "amount": 53.77,
            "state": "complete"
        }
    ],
    ...
}
```
{% endtab %}
{% endtabs %}

## Handling charge failures <a href="#handling-failures" id="handling-failures"></a>

When a payment authorization request fails, the [charge's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) [`state`](./#the-charge-lifecycle) becomes `failed`. The same is true for failed [captures](./#captures), [cancels](./#cancels), and [refunds](./#refunds).

Each of these objects contains a `failureMessage` and `failureCode` that you may be able to use to pinpoint a reason for the failure.

For more information, refer to [authorization declines](../../../payments/authorization-declines.md) and [handling rejected orders](../../resubmitting-an-order.md).

## The charge lifecycle

A [charge's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) `state` can be `pending`, `capturable`, `processing`, `complete`, `cancelled`, or `failed`.

When a charge's `state` changes, Digital River creates a corresponding [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events). For example, when the charge's `state` changes from `pending` to `capturable` an `order.charge.capturable` event is emitted.

The `state` values for a successful charge (i.e. the happy path) are `pending` > `capturable` > `processing` > `complete` .

The following table lists the possible states of a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) and their corresponding events:

| 1) When the charge...                                                                                                 | (2) its state transitions to... | (3) and an...event is emitted. |
| --------------------------------------------------------------------------------------------------------------------- | ------------------------------- | ------------------------------ |
| ...is awaiting authorization, typically because additional customer action is required                                | `pending`                       | `order.charge.pending`         |
| ...is authorized by the payment provider                                                                              | `capturable`                    | `order.charge.capturable`      |
| ...is being processed by the payment provider                                                                         | `processing`                    | `order.charge.processing`      |
| ...is captured in full (or captured in part with the remainder cancelled) and there are no pending charge operations. | `complete`                      | `order.charge.complete`        |
| ...is cancelled in full and there are no pending charge operations.                                                   | `cancelled`                     | `order.charge.cancelled`       |
| fails to authorize                                                                                                    | `failed`                        | `order.charge.failed`          |

For different success and error scenarios, you can [create tests](../../../developer-resources/testing-scenarios.md) to determine whether your integration returns the expected `state` value.
