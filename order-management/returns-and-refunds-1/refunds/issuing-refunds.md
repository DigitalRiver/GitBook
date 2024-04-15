---
description: Learn how to use the Refunds API to issue full and partial refunds
---

# Issuing refunds

The [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) allows you to reimburse customers for product costs, shipping expenses, taxes, duties, and regulatory fees.

Once you [configure and create a refund](issuing-refunds.md#configuring-and-creating-refunds), your integration should be set up to [handle refund state changes](issuing-refunds.md#handling-refund-state-changes).&#x20;

To tailor a refund so that customers are _only_ reimbursed for specific, non-product related expenses, you must specify  [`type`](issuing-refunds.md#refund-types).&#x20;

## Refund preconditions

Before submitting a [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) request, make sure you have:

* [Fulfilled the order](issuing-refunds.md#order-fulfilled)
* [Checked the available to refund amount](issuing-refunds.md#available-to-refund-amount)
* [Specified the appropriate currency](issuing-refunds.md#currency)

### Order fulfilled

The [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) should only be used once an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is partially or completely fulfilled.&#x20;

This is due to the fact that [refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) can only be created on [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) with [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) [`captures[]`](../../orders/payment-charges/#captures) in a `state` of `complete`. To be notified of this `state` change event, you can subscribe to [`order.charge.capture.complete`](../../informing-digital-river-of-a-fulfillment.md#successful-charge-captures).

{% hint style="info" %}
If you'd like to [cancel a charge](../../orders/payment-charges/#cancels) before it's captured, use the [Fulfillments API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments). For details, refer to [Capturing and cancelling payment charges](../../informing-digital-river-of-a-fulfillment.md).
{% endhint %}

Once a [capture](../../orders/payment-charges/#captures) is `complete`, Digital River increases [`availableToRefundAmount`](issuing-refunds.md#available-to-refund-amount).

{% code title="Order" %}
```javascript
{
    "id": "219965900336",
    ...
    "items": [
        {
            "id": "145174060336",
            ...
            "availableToRefundAmount": 27.01,
            ...
        }
    ],
    "payment": {
        "charges": [
            {
                "id": "07f84c7b-6412-4f75-b0fa-562958ad0b76",
                ...
                "captures": [
                    {
                        "id": "d9202f29-6ec9-40d7-a6bc-73510b4e030b",
                        ...
                        "amount": 27.01,
                        "state": "complete"
                    }
                ],
                ...
            }
        ],
        ...
   "availableToRefundAmount": 27.01
   ...
}
```
{% endcode %}

### Available to refund amount

Prior to submitting a [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds), you can make a [`GET/orders/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveOrders)to determine whether the `amount` you're requesting is less than or equal to what's available.

A `200 OK` response contains an `availableToRefundAmount` at both the [order-level](issuing-refunds.md#available-to-refund-amount-order-level) and the [item-level](issuing-refunds.md#available-to-refund-amount-item-level).&#x20;

{% hint style="info" %}
The value of `availableToRefundAmount` reflects both [pending](issuing-refunds.md#pending-refunds) and [completed](issuing-refunds.md#completed-refunds) refunds.
{% endhint %}

{% code title="Order" %}
```javascript
{
    "id": "219496900336",
    ...
    "items": [
        {
            "id": "144659950336",
            ...
            "availableToRefundAmount": 15.0,
            ...
        },
        {
            "id": "144659940336",
            ...
            "availableToRefundAmount": 27.01,
            ...
        }
    ],
    ...
    "availableToRefundAmount": 42.01,
    ...
}
```
{% endcode %}

At a high level, Digital River calculates these values by using the following formula:

`availableToRefundAmount =` [`charge(s)`](../../orders/payment-charges/)`amount` [`captured`](../../orders/payment-charges/#captures) `− (`[`completed refunds`](issuing-refunds.md#completed-refunds) `amount +` [`pending refunds`](issuing-refunds.md#pending-refunds) `amount)`

If you submit a `POST/refunds` whose `amount` is greater than the [order's `availableToRefundAmount`](issuing-refunds.md#available-to-refund-amount-order-level), or whose `items[].amount` is greater than that [`items[].availableToRefundAmount`](issuing-refunds.md#available-to-refund-amount-item-level), then a `400 Bad Request` is thrown:

{% code title="Error" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "amountRequested",
            "message": "The requested refund amount is greater than the available amount."
        }
    ]
}
```
{% endcode %}

#### Available to refund amount: order-level

At the order-level, `availableToRefundAmount` reflects the unrefunded portion of an order's [`capturedAmount`](../../orders/payment-charges/#captures). This `availableToRefundAmount` may include product prices, along with any expenses related to shipping, duties, fees, and assessed taxes.

{% code title="Order" %}
```json
{
    "id": "235507650336",
    ...
    "capturedAmount": 27.01,
    ...
    "availableToRefundAmount": 13.5,
    ...
}
```
{% endcode %}

#### Available to refund amount: item-level

In [orders](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), `items[].availableToRefundAmount` reflects the unrefunded portion of that line item's [captured](../../orders/payment-charges/#captures) `amount` plus its `tax.amount`. It _doesn't_ include expenses related to shipping, duties, or fees.

{% hint style="success" %}
If you'd like to refund shipping costs associated with an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) individual `items[]`, then you can determine what customers paid by accessing `items[].shipping.amount` and `items[].shipping.taxAmount`.
{% endhint %}

In the following example, note that each line item's `availableToRefundAmount` excludes its `shipping.amount` and `shipping.taxAmount`.

{% code title="Order" %}
```json
{
    "id": "237455490336",
    ...
    "items": [
        {
            ...
            "amount": 10.0,
            ...
            "tax": {
                ...
                "amount": 0.8
            },
            ...
            "availableToRefundAmount": 10.8,
            ...
            "shipping": {
                "amount": 2.5,
                "taxAmount": 0.2
            }
        },
        {
            ...
            "amount": 10.0,
            ...
            "tax": {
               ...
                "amount": 0.8
            },
            ...
            "availableToRefundAmount": 10.8,
            ...
            "shipping": {
                "amount": 2.5,
                "taxAmount": 0.2
            }
        }
    ],
    ...
}
```
{% endcode %}

### Currency

A [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) requires `currency`. After you submit this request, Digital River doesn't perform a currency conversion. As a result, the value you pass must be the same as the associated [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `currency`. If they're different, a `400 Bad Request` is thrown:

{% code title="Error" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "currency",
            "message": "Currency EUR is not supported."
        }
    ]
}
```
{% endcode %}

## Configuring and creating refunds

Prior to submitting a [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) request, [specific preconditions](issuing-refunds.md#refund-preconditions) must exist. Once satisfied, you can request a variety of refunds. The following sections provide information on how to reimburse:

* [Product costs](issuing-refunds.md#product-refunds)
* [Taxes](issuing-refunds.md#refunding-taxes)
* [Shipping expenses](issuing-refunds.md#refunding-shipping)

### Product refunds

You can issue product refunds at the [order level](issuing-refunds.md#order-level-product-refunds) and the [line item level](issuing-refunds.md#line-item-level-product-refunds).

#### Order level product refunds

If you'd like to refund an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) product costs, then ensure that the body of your [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds/operation/createRefunds):

* Omits `type`
* Either (1) sets `percent` to a value in the range of `0.01` to `100.00` inclusive or (2) sets `amount` to a value that's less than or equal to the [order's `availableToRefundAmount`](issuing-refunds.md#available-to-refund-amount-order-level)&#x20;

{% tabs %}
{% tab title="Order-level percent refund request" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/refunds' \
...
--data-raw '{
    "orderId": "219974470336",
    "currency": "USD",
    "percent": 100
}'
```
{% endtab %}

{% tab title="Order-level amount refund request" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/refunds' \
...
--data-raw '{
    "orderId": "219974470336",
    "currency": "USD",
    "amount": "27.01"
}'. 
```
{% endtab %}
{% endtabs %}

If you set `percent` to `100` or `amount` to the [order's `availableToRefundAmount`](issuing-refunds.md#available-to-refund-amount-order-level), then Digital River attempts to reimburse the full `availableToRefundAmount`.&#x20;

If you pass any lower `percent` or `amount`, then an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) product costs, shipping expenses, duties, and taxes are proportionally refunded.

{% hint style="info" %}
Product refund requests do not reimburse [regulatory fees](../../../product-management/regulatory-fees/). To do that, you must set [`type`](issuing-refunds.md#refund-types) to `fees` in a separate [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds)
{% endhint %}

{% tabs %}
{% tab title="POST/refunds" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/refunds' \
...
--data-raw '{
    "orderId": "219975310336",
    "currency": "USD",
    "percent": 50
}'
```
{% endtab %}

{% tab title="Refund" %}
```javascript
{
    "id": "re_c19de38c-22cc-46b7-8e7f-2e4681cc2941",
    "amount": 13.51,
    ...
    "orderId": "219975310336",
    "refundedAmount": 13.51,
    "state": "succeeded",
    "liveMode": false,
    "charges": [
        {
            "id": "7c99d449-117a-4502-b1ea-b1e1a5343412",
            "captured": true,
            "refunded": true,
            "refunds": [
                {
                    "createdTime": "2022-03-17T21:04:04Z",
                    "amount": 13.51,
                    "state": "complete"
                }
            ],
            "sourceId": "9dcee2b0-ce84-4374-84fc-6317729b4dd3"
        }
    ]
}
```
{% endtab %}

{% tab title="Order" %}
```javascript
{
    "id": "219975310336",
    ...
    "totalAmount": 27.01,
    "subtotal": 25.0,
    ...
    "totalTax": 2.01,
    ...
    "totalShipping": 5.0,
    ...
    "payment": {
        "charges": [
            {
                ...
                "captures": [
                    {
                        ...
                        "amount": 27.01,
                        "state": "complete"
                    }
                ],
                "refunded": true,
                "refunds": [
                    {
                        ...
                        "amount": 13.51,
                        "state": "complete"
                    }
                ],
                ...
            }
        ],
    ...
    "refundedAmount": 13.51,
    ...
    "capturedAmount": 27.01,
    ...
    "availableToRefundAmount": 13.5,
    ...
}
```
{% endtab %}
{% endtabs %}

#### Line-item level product refunds

If you'd like to refund an `items[]` product costs, then ensure that the body of your [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds/operation/createRefunds):

* Omits `items[].type`
* Specifies an `items[].quantity` that is less than or equal to the corresponding `items[].quantity` in the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders)
* Either (1) sets `items[].percent` to a value in the range of `0.01` to `100.00`, inclusive or (2) sets `items[].amount` to a value that's less than or equal to that [`items[].availableToRefundAmount`](issuing-refunds.md#available-to-refund-amount-item-level).

If you configure the request this way, Digital River attempts to refund the specified `quantity` of `items[]` by the given `percent` or `amount`.

{% tabs %}
{% tab title="POST/refunds" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/refunds' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer sk_test_ea6f3e97c3f94b33b58e39d1c013f364' \
--header 'Cookie: incap_ses_1326_1638494=K9W9dx/1/jBJpcH6UeZmEjJ1PGIAAAAAX3ucdBSpIP2TivcLZF6BfQ==; incap_ses_6522_1638494=KObzY36wLi46+CuXdsyCWgXRPGIAAAAAMZkNGsosFQyIXLdAZCcVCQ==; nlbi_1638494_1914372=0JbidDMPHxouUSQviXZ5LAAAAABdyRk6JGyNhyte+5r6KG2E; nlbi_1638494_2412637=aTFZdFXsLCM1uYBtiXZ5LAAAAAB+sX1j1Jq8H0j4gBwzktpi; visid_incap_1638494=S/ubAWkHTB+qbgwhFj7HgMXaSWEAAAAAQUIPAAAAAADUpxCyuVm7HqaQDmEdHhTm; visid_incap_2137235=YibR5HAMTw28J10M4p6Omyb+vWEAAAAAQUIPAAAAAADLOejzH/0oGlmJVXjAkh4Q; visid_incap_2223514=75hpreQFTEeUoJQziq2pkFOccWEAAAAAQUIPAAAAAADefDtHFYydOaHYPCytcnKS' \
--data-raw '{
    "orderId": "220821660336",
    "currency": "USD",
    "items": [
        {
            "itemId": "146111340336",
            "quantity": "2",
            "percent": 100
        },
        {
            "itemId": "146111350336",
            "quantity": "4",
            "percent": 50
        }
    ]
}'
```
{% endtab %}

{% tab title="Refund" %}
```javascript
{
    "id": "re_ebbf8180-50f2-4ec7-8a58-f490d1e239d1",
    "createdTime": "2022-03-24T20:27:16Z",
    "currency": "USD",
    "items": [
        {
            "amount": 21.61,
            "quantity": 2,
            "refundedAmount": 21.61,
            "skuId": "2758690d-01a5-4a3b-b0d7-2081793de8b8",
            "itemId": "146111340336"
        },
        {
            "amount": 21.61,
            "quantity": 4,
            "refundedAmount": 21.61,
            "skuId": "dd9d7dc4-3ee2-4003-9e23-c67b6fafac87",
            "itemId": "146111350336"
        }
    ],
    "orderId": "220821660336",
    "refundedAmount": 43.22,
    "state": "succeeded",
    "liveMode": false,
    "charges": [
        {
            "id": "b5a497f7-d650-4279-8a70-942e72e8232c",
            "captured": true,
            "refunded": true,
            "refunds": [
                {
                    "createdTime": "2022-03-24T20:28:41Z",
                    "amount": 43.22,
                    "state": "complete"
                }
            ],
            "sourceId": "3d94448d-d9b9-4ebf-ae74-c5839a1a9840"
        }
    ]
```
{% endtab %}
{% endtabs %}

Along with product costs, line item-level refund requests using this configuration proportionally reimburse that `items[].tax.amount`. They do not, however, refund any shipping, regulatory fee, importer tax, or duty amounts (along with taxes assessed on those amounts) that are associated with that `items[]`.

To get those expenses back, you could submit a separate `POST/refunds` that specifies [`items[].type`](issuing-refunds.md#refund-types).

## Refund types

If you want to _only_ reimburse specific, non-product related costs, such as shipping, duties, [regulatory fees](../../../product-management/regulatory-fees/), and taxes, your [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) must specify `type` at either the order-level or the line item-level.

{% hint style="success" %}
When [issuing refunds on product costs](issuing-refunds.md#product-refunds), make sure you omit `type` in your `POST/refunds` request.&#x20;
{% endhint %}

{% tabs %}
{% tab title="Order-level" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/refunds' \
...
--data-raw '{
    "orderId": "222671410336",
    "currency": "USD",
    "type": "shipping",
    "percent": 75
}'
```
{% endtab %}

{% tab title="Item-level" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/refunds' \
...
--data-raw '{
    "orderId": "222671410336",
    "currency": "USD",
    "items": [
        {
            "type": "shipping",
            "itemId": "148089050336",
            "quantity": "2",
            "percent": 75
        }
    ]
}'
```
{% endtab %}
{% endtabs %}

When `type` is `shipping`, `fees`, or `duty`, any taxes assessed on those particular components of the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) are also refunded.

For details on how to configure a refund request when `type` is `tax` or `importer_tax`, refer to [Refunding taxes](issuing-refunds.md#refunding-taxes).

#### Refunding taxes

In `POST/refunds`, by setting [`type`](issuing-refunds.md#refund-types) to `tax`, you can reimburse just the tax component of an order. You can't, however, partially refund taxes using `type`.&#x20;

{% hint style="info" %}
The [Refunds API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) doesn't support tax-only reimbursements at the `items[]` level.
{% endhint %}

If you submit a [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) that specifies a `type` of `tax`, then either (1) `percent` must be `100` or (2) `amount` must be equal to the unrefunded portion of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `totalTax`. If either of these conditions are not met, then a `400 Bad Request` is returned.

{% code title="Error" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "percentRequested",
            "message": "Only full tax refunds are supported."
        }
    ]
}
```
{% endcode %}

When refunding taxes, we recommend you use `percent` instead of `amount`. This is because an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `totalTax` doesn't always reflect how much refundable tax exists. Previous refunds may have reduced what's available.

In these cases, if you retrieve an order's `totalTax`, and use that value to set `amount` in a `POST/refunds`, then a `400 Bad Request` is returned.

{% code title="Error" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "invalid_parameter",
            "parameter": "amountRequested",
            "message": "The requested refund amount is greater than the available amount."
        }
    ]
}
```
{% endcode %}

After you successfully submit a `POST/refunds` with a `type` of `tax`, Digital River attempts to reclaim the unrefunded portion of an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `totalTax`.

{% tabs %}
{% tab title="POST/refunds" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/refunds' \
...
--data-raw '{
    "orderId": "219965900336",
    "currency": "USD",
    "type": "tax",
    "percent": 100
}'
```
{% endtab %}

{% tab title="Refund" %}
```javascript
{
    "id": "re_9d55374c-da56-43ea-8da7-5a933f34aa1a",
    "amount": 2.01,
    "createdTime": "2022-03-17T15:30:18Z",
    "currency": "USD",
    "type": "tax",
    "items": [],
    "orderId": "219965900336",
    "refundedAmount": 2.01,
    "state": "succeeded",
    "liveMode": false,
    "charges": [
        {
            "id": "07f84c7b-6412-4f75-b0fa-562958ad0b76",
            "captured": true,
            "refunded": true,
            "refunds": [
                {
                    "createdTime": "2022-03-17T15:32:45Z",
                    "amount": 2.01,
                    "state": "complete"
                }
            ],
            "sourceId": "68868a82-b0d7-41c7-9868-03feb145546d"
        }
    ]
}
```
{% endtab %}

{% tab title="Order" %}
```javascript
{
    "id": "219965900336",
    ...
    "totalAmount": 27.01,
    "subtotal": 25.0,
    ...
    "totalTax": 2.01,
    ...
    "payment": {
        "charges": [
            {
                "id": "07f84c7b-6412-4f75-b0fa-562958ad0b76",
                ...
                "captures": [
                    {
                        "id": "d9202f29-6ec9-40d7-a6bc-73510b4e030b",
                        ...
                        "amount": 27.01,
                        "state": "complete"
                    }
                ],
                "refunded": true,
                "refunds": [
                    {
                        ...
                        "amount": 2.01,
                        "state": "complete"
                    }
                ],
                ...
            }
        ],
    ...
    "refundedAmount": 2.01,
    ...
    "capturedAmount": 27.01,
    ...
    "availableToRefundAmount": 25.0,
    ...
}
```
{% endtab %}
{% endtabs %}

#### Refunding shipping

You also have the ability to issue refunds only on shipping costs. To do this, set [`type`](issuing-refunds.md#refund-types) to `shipping` and specify an `amount` or `percent`.

We recommend using `percent` instead of `amount`. This is because an [order's ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders)`totalShipping` doesn't always reflect the actual refundable shipping costs. Previous refunds may have reduced what's available.

In these cases, if you retrieve `totalShipping`, and use that value to set `amount` in a `POST/refunds`, then a `400 Bad Request` is returned.

Depending on the value you assign `percent`, passing a `type` of `shipping` fully or partially refunds both an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `shippingChoice.amount` and `shippingChoice.tax`

{% tabs %}
{% tab title="POST/refunds" %}
```javascript
curl --location --request POST 'https://api.digitalriver.com/refunds' \
...
--data-raw '{
    "orderId": "220527740336",
    "currency": "USD",
    "type": "shipping",
    "percent": 100
}'
```
{% endtab %}

{% tab title="Refund" %}
```javascript
{
    "id": "re_7cc420ed-7089-43ba-bb0b-0b5dc95105bd",
    "amount": 5.4,
    "createdTime": "2022-03-22T20:17:49Z",
    "currency": "USD",
    "type": "shipping",
    "items": [],
    "orderId": "220527740336",
    "refundedAmount": 5.4,
    "state": "succeeded",
    "liveMode": false,
    "charges": [
        {
            "id": "1abef982-0ede-4faa-a493-d100e5d2c6c1",
            "captured": true,
            "refunded": true,
            "refunds": [
                {
                    "createdTime": "2022-03-22T20:23:20Z",
                    "amount": 5.4,
                    "state": "complete"
                }
            ],
            "sourceId": "798b0ff3-81c3-45f4-b779-29b1ac2a3aac"
        }
    ]
}
```
{% endtab %}

{% tab title="Order" %}
```javascript
{
    "id": "220527740336",
    ...
    "totalAmount": 27.01,
    "subtotal": 25.0,
    ...
    "totalTax": 2.01,
    ...
    "totalShipping": 5.0,
    ...
    "shippingChoice": {
        ...
        "amount": 5.0,
        ...
        "taxAmount": 0.4,
        ...
    },
    ...
    "payment": {
        "charges": [
            {
                ...
                "refunded": true,
                "refunds": [
                    {
                        ...
                        "amount": 5.4,
                        "state": "complete"
                    }
                ],
                ...
            }
        ],
    ...
    "refundedAmount": 5.4,
    ...
    "capturedAmount": 27.01,
    ...
    "availableToRefundAmount": 21.61,
    ...
}
```
{% endtab %}
{% endtabs %}

## Handling refund state changes

After submitting a refund request, we recommend that your integration be set up to listen for the following [events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events):

* [`refund.pending`](issuing-refunds.md#pending-refunds)
* [`refund.pending_information`](issuing-refunds.md#pending-information-refunds)
* [`refund.complete`](issuing-refunds.md#completed-refunds)
* [`refund.failed`](issuing-refunds.md#failed-refunds)

### Pending refunds

When a [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) is successful, Digital River sets the [refund's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) `state` to `pending` and creates a `refund.pending` event.

This `state` indicates that Digital River and the payment processor have all the information they need to initiate the refund process.

{% hint style="warning" %}
A `201 Created` response code doesn't signify that the bank approved the refund. It only means that your refund request was successfully sent. To be notified of approved refunds, listen for the [`refund.complete`](issuing-refunds.md#completed-refunds) event.
{% endhint %}

In [refunds](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) that have a `state` of `pending` , `refundedAmount` is always `0.0`.

{% tabs %}
{% tab title="refund.pending (order-level)" %}
```javascript
{
    "id": "07b04605-0089-4789-af46-4cefb34786ef",
    "type": "refund.pending",
    "data": {
        "object": {
            "id": "re_252eb3f4-81b2-4576-aabd-6af2df248e99",
            "amount": 13.51,
            "createdTime": "2022-03-17T16:17:54Z",
            "currency": "USD",
            "items": [],
            "orderId": "219966860336",
            "refundedAmount": 0.0,
            "state": "pending",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2022-03-17T16:17:54.93644Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}

{% tab title="refund.pending (item-level)" %}
```javascript
{
    "id": "749267cf-a86e-471e-ab70-e4b315c9b9c4",
    "type": "refund.pending",
    "data": {
        "object": {
            "id": "re_e0779bb1-7af2-43f5-9225-35a282d86f66",
            "createdTime": "2022-03-21T21:46:54Z",
            "currency": "USD",
            "items": [
                {
                    "amount": 21.61,
                    "quantity": 2,
                    "refundedAmount": 0.0,
                    "skuId": "4dc8b640-0c74-48f1-bec0-39b947c5dde7",
                    "itemId": "145634580336"
                },
                {
                    "amount": 72.92,
                    "quantity": 3,
                    "refundedAmount": 0.0,
                    "skuId": "4dc8b640-0c74-48f1-bec0-39b947c5dde7",
                    "itemId": "145634590336"
                }
            ],
            "orderId": "220400480336",
            "refundedAmount": 0.0,
            "state": "pending",
            "liveMode": false
        }
    },
    "liveMode": false,
    "createdTime": "2022-03-21T21:46:55.215753Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

You can use `refund.pending` to trigger a notification to customers, informing them that their refund is being processed. Make sure you also update the status of the refund on their order details page.

### Pending information refunds

In some cases, customers must first supply their banking details before payment processors act on a refund request. This is common when the purchase was made with a [wire transfer](../../../payments/supported-payment-methods/#wire-transfer) or other [delayed payment method](../../../payments/payment-sources/#synchronous-or-asynchronous).

When the bank requests this additional information, Digital River moves the [refund's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) `state` to `pending_information` and creates a `refund.pending_information` event.

For more information on how to handle this `state` change, refer to the [Refunding asynchronous payment methods](handling-refunds-for-asynchronous-payment-methods.md) page.

### Completed refunds

When a [refund](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) is successfully processed, Digital River moves its `state` to `succeeded` and creates an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](../../events-and-webhooks-1/events-1/#event-types) of `refund.complete`.

{% hint style="info" %}
To [notify customers of successfully processed refunds](../../customer-notifications.md#refund-confirmation), you can also [configure a webhook](../../../administration/dashboard/developers/webhooks/) to listen for [`order.refunded`](../../events-and-webhooks-1/events-1/event-types.md#order.refunded).
{% endhint %}

In the payload, `amount` is how much you requested be refunded and `refundedAmount` is the actual reimbursed amount.

{% tabs %}
{% tab title="refund.complete (order-level)" %}
```javascript
{
    "id": "ebd5dcb3-7028-4a78-8efb-3d7ca918e96e",
    "type": "refund.complete",
    "data": {
        "object": {
            "id": "re_252eb3f4-81b2-4576-aabd-6af2df248e99",
            "amount": 13.51,
            "createdTime": "2022-03-17T16:17:54Z",
            "currency": "USD",
            "items": [],
            "orderId": "219966860336",
            "refundedAmount": 13.51,
            "state": "succeeded",
            "liveMode": false,
            "charges": [
                {
                    "id": "b46e2189-fd69-4819-a886-f43c89283bda",
                    "captured": true,
                    "refunded": true,
                    "refunds": [
                        {
                            "createdTime": "2022-03-17T16:22:14Z",
                            "amount": 13.51,
                            "state": "complete"
                        }
                    ],
                    "sourceId": "cca536f3-93ed-40e8-bd79-99a3dcf2edf8"
                }
            ]
        }
    },
    "liveMode": false,
    "createdTime": "2022-03-17T16:23:29.233283Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}

{% tab title="refund.complete (item-level)" %}
```javascript
{
    "id": "a1afc456-338a-427f-b888-33cdd11ea1e4",
    "type": "refund.complete",
    "data": {
        "object": {
            "id": "re_e0779bb1-7af2-43f5-9225-35a282d86f66",
            "createdTime": "2022-03-21T21:46:54Z",
            "currency": "USD",
            "items": [
                {
                    "amount": 21.61,
                    "quantity": 2,
                    "refundedAmount": 21.61,
                    "skuId": "4dc8b640-0c74-48f1-bec0-39b947c5dde7",
                    "itemId": "145634580336"
                },
                {
                    "amount": 72.92,
                    "quantity": 3,
                    "refundedAmount": 72.92,
                    "skuId": "4dc8b640-0c74-48f1-bec0-39b947c5dde7",
                    "itemId": "145634590336"
                }
            ],
            "orderId": "220400480336",
            "refundedAmount": 94.53,
            "state": "succeeded",
            "liveMode": false,
            "charges": [
                {
                    "id": "f83bb9a4-9a52-4aae-862d-0731fd65fbf9",
                    "captured": true,
                    "refunded": true,
                    "refunds": [
                        {
                            "createdTime": "2022-03-21T21:52:51Z",
                            "amount": 94.53,
                            "state": "complete"
                        }
                    ],
                    "sourceId": "3aa42f3f-673d-4ca9-bf5e-8afd33c4c611"
                }
            ]
        }
    },
    "liveMode": false,
    "createdTime": "2022-03-21T21:53:33.901789Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endtab %}
{% endtabs %}

You can use `refund.complete` to trigger a [refund confirmation email to customers](../../customer-notifications.md#refund-confirmation). The message (typically an email) should notify them that their refund request was successful and inform them how much they were reimbursed. Make sure you also update the status of the refund on their order details page.&#x20;

### Failed refunds

If your refund request fails, Digital River moves the [refund's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) `state` to `failed` and creates a `refund.failed` event. In these cases, `refundedAmount` is `0.0`.

{% hint style="info" %}
For information on how to test refund failures, refer to [Testing scenarios](../../../developer-resources/testing-scenarios.md).
{% endhint %}

{% code title="refund.failed" %}
```javascript
{
    "id": "73f6350d-bd03-48fc-a1a4-080dc538002a",
    "type": "refund.failed",
    "data": {
        "object": {
            "id": "re_9ed7d5b1-186c-492f-bcb1-a4177d9ceead",
            "amount": 27.01,
            "createdTime": "2022-03-18T13:18:40Z",
            "currency": "USD",
            "items": [],
            "orderId": "220072430336",
            "refundedAmount": 0.0,
            "state": "failed",
            "liveMode": false,
            "charges": [
                {
                    "id": "5bb706f7-fb2d-4b02-906e-f8fb4f10d34a",
                    "captured": true,
                    "refunded": true,
                    "refunds": [
                        {
                            "createdTime": "2022-03-18T13:22:36Z",
                            "amount": 27.01,
                            "state": "failed"
                        }
                    ],
                    "sourceId": "824f65eb-2270-402f-9dee-1346db324070"
                }
            ]
        }
    },
    "liveMode": false,
    "createdTime": "2022-03-18T13:23:33.253931Z",
    "webhookIds": [
        "bbac1929-580c-4629-b648-4c096b1a104a",
        "6d7055fc-b3b6-42fb-97a8-2443386199fb"
    ],
    "digitalriverVersion": "2021-12-13"
}
```
{% endcode %}

Some common reasons for a refund failure include:

* A closed account
* A frozen account due to suspected fraud
* An expired credit card

If a refund fails, your integration can attempt to submit another [`POST/refunds`](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/createRefunds) using the same `itemId`(s) and/or `orderId`. Alternatively, you can try to [manually process the refund in Digital River Dashboard](../../../administration/dashboard/order-management/orders/creating-a-refund.md).

## Providing a total refunded amount

An [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `refundedAmount` contains the total amount of all refunds issued on an order. This is a useful value to display to customers on their order details page.
