---
description: Learn how to apply store credit
---

# Applying store credit (legacy)

{% hint style="warning" %}
This page explains how to use store credit in [versions](../../../general-resources/versioning.md) `2020-09-30`, `2020-12-17`, and `2021-02-23`. For versions `2021-03-23` and higher, refer to [Applying store credit](applying-a-store-credit.md).&#x20;
{% endhint %}

For non-recurring transactions, customers can pay using store credit, a unique payment type that allows you to connect your credit management system to [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts). With store credit, you manage customers' credit on your end, and can display the amount available to them during the checkout process.

{% hint style="info" %}
Store credit is a [single-use payment source](../../../payments/payment-sources/#reusable-or-single-use) and therefore can't be saved to a [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) record.
{% endhint %}

You [create store credit payment sources](applying-store-credit-legacy.md#creating-store-credit) and then Digital River [attaches the store credit to the checkout](applying-store-credit-legacy.md#how-store-credit-is-attached-to-checkouts). &#x20;

When [funding the transaction](applying-store-credit-legacy.md#funding-the-transaction), you can [use store credit alone](applying-store-credit-legacy.md#using-store-credit-alone) or [pair it with a primary payment source](applying-store-credit-legacy.md#pairing-store-credit-with-a-primary-payment-source).

With store credit, the steps necessary to [handle fulfillments](../../../order-management/fulfillments.md) and [request refunds](../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md) remain the same, but, if an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `sources[]` contain store credit and a [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources), you should be aware of [how Digital River handles captures, cancels, and refunds](applying-store-credit-legacy.md#how-digital-river-handle-captures-cancels-and-refunds).

{% hint style="info" %}
Digital River API does not currently support Amazon Pay with store credit.
{% endhint %}

## Creating store credit

You create store credit by passing `creditAmount` in either a [`POST/ checkouts`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/createCheckouts) or [`POST/ checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts) request. The value you pass represents the amount of store credit you're extending to the customer.

### Handling multiple lines of credit

You can only send `creditAmount` once. If the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) already contains a `creditAmount` and you pass `creditAmount` in an [update request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts), then the following error is thrown:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "creditAmount_already_updated",
            "message": "Credit amount has already been updated."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

So, when customers opt to apply multiple lines of credit to the transaction, aggregate that amount and send `creditAmount` in a single API request.

## How store credit is attached to checkouts

After you [create store credit](applying-store-credit-legacy.md#creating-store-credit), Digital River adds a [`sources[]`](../../../payments/payment-sources/) with a [`type`](../../../payments/payment-sources/#supported-payment-methods) of `customerCredit` to the [checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts).&#x20;

{% tabs %}
{% tab title="Checkout " %}
```javascript
{
    "id": "ef285ef9-8bf8-4589-9eeb-2cabe5ac2f2b",
    ...
    "creditAmount": 10.0,
    "sources": [
        {
            "id": "f9b80c8f-07fd-4b2d-8c64-eea729712fc2",
            "createdTime": "2021-03-08T20:47:07Z",
            "type": "customerCredit",
            "currency": "USD",
            "amount": 5.0,
            "reusable": false,
            "state": "consumed",
            "owner": {
                "firstName": "John",
                "lastName": "Doe",
                "email": "anyemail@digitalriver.com",
                "address": {
                    "line1": "434 3rd Street",
                    "city": "Minneapolis",
                    "postalCode": "55401",
                    "state": "MN",
                    "country": "US"
                }
            },
            "clientSecret": "f9b80c8f-07fd-4b2d-8c64-eea729712fc2_d2829190-fd91-4455-8851-8b2e27affd54",
            "customerCredit": {}
        }
    ],
    "sourceId": "f9b80c8f-07fd-4b2d-8c64-eea729712fc2"
}
```
{% endtab %}
{% endtabs %}

## Funding the transaction

You can fund a transaction [entirely with store credit](applying-store-credit-legacy.md#using-store-credit-alone) or [pair store credit with a primary payment source](applying-store-credit-legacy.md#pairing-store-credit-with-a-primary-payment-source). In either case, Digital River first computes taxes based on the checkout's `totalAmount`, and then applies the store credit.

{% hint style="info" %}
For a list of [primary sources](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) that can be combined with `customerCredit`, refer to [combining payment sources](../../../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources) on the [Managing sources](../../../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources) page.
{% endhint %}

### Using store credit alone

A customer can make a purchase entirely with store credit. To do so, a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `creditAmount` must be equal to or greater than its `totalAmount` before you [create the order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier). In this case, you're not required to [pair store credit with a primary payment source](applying-store-credit-legacy.md#pairing-store-credit-with-a-primary-payment-source).

However, if a checkout's only `sources[]` has a `type` of `customerCredit`, you must set the checkout's [`billTo`](providing-address-information.md#billing-address-requirements). If you don't, you'll receive a `409 Conflict` when you submit the [create order request](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier).

### Pairing store credit with a primary payment source

If a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `creditAmount` is less than its `totalAmount`, then you'll need to associate a [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) with the checkout.&#x20;

If you don't do this, and you attempt to [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), you receive the following error:

{% tabs %}
{% tab title="400 Bad Request" %}
```javascript
{
    "type": "bad_request",
    "errors": [
        {
            "code": "order_submit_failed",
            "message": "Payment session status is invalid."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

{% hint style="success" %}
If a checkout's `sources[]` contains `customerCredit` as well as a [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources), you can replace the primary source with a different primary source by sending its  `sourceId` in the payload of a [`POST/checkouts/{id}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts).
{% endhint %}

How you sequence the use of store credit with a primary source depends on whether the latter is [single use](applying-store-credit-legacy.md#single-use-primary-sources) or [reusable](applying-store-credit-legacy.md#reusable-primary-sources).

#### Single use primary sources

If the [primary source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) has a [`reusable`](../../../payments/payment-sources/#reusable-or-single-use) value that's `false`, then you must first [create the store credit](applying-store-credit-legacy.md#creating-store-credit) before [attaching the primary source](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

If your integration attaches a single use primary payment source to a checkout, and then attempts to [update the checkout](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts) with a `creditAmount`, you'll receive the following `409 Conflict`:

{% tabs %}
{% tab title="409 Conflict" %}
```javascript
{
    "type": "conflict",
    "errors": [
        {
            "code": "source_not_supported",
            "parameter": "sourceId",
            "message": "The source status is invalid for this session."
        }
    ]
}
```
{% endtab %}
{% endtabs %}

#### Reusable primary sources

If the [primary source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) has a [`reusable`](../../../payments/payment-sources/#reusable-or-single-use) value that's `true`, thereby indicating that it's saved to the [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) record, then the sequence doesn't matter. In other words, your workflow can [create store credit](applying-store-credit-legacy.md#creating-store-credit) before or after [attaching a primary source to the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).

## Store credit in orders

If a [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) only `sources[]` has a `type` of `customerCredit`, then, upon [order creation](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), Digital River uses that [source](../../../payments/payment-sources/) to generate a single [charge](../../../order-management/orders/payment-charges/).

On the other hand, if you [pair store credit with a primary source in a checkout](applying-store-credit-legacy.md#pairing-store-credit-with-a-primary-payment-source), and then create the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), Digital River generates two charges. In the following example, the `sources[]` with a `type` of `customerCredit` is used to generate one of the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `charges[]` and the `creditCredit` source is used to generate the other.&#x20;

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "185314800336",
    ...
    "totalAmount": 21.51,
    "subtotal": 20.0,
    ...
    "creditAmount": 10.0,
    "sources": [
        {
            "id": "f04ac3b4-016a-4c75-a093-20115bd27b5b",
            ...
            "type": "creditCard",
            ...
            "amount": 21.51,
            "reusable": true,
            "state": "chargeable",
            ...
            "creditCard": {
                "brand": "Visa",
                "expirationMonth": 7,
                "expirationYear": 2027,
                "lastFourDigits": "1111"
            }
        },
        {
            "id": "3066c73f-0894-44ee-8ae6-4cd8be32642e",
            ...
            "type": "customerCredit",
            ...
            "amount": 10.0,
            "reusable": false,
            "state": "consumed",
            ...
            "customerCredit": {}
        }
    ],
    ...
    "charges": [
        {
            "id": "aa747a62-6b56-4053-a2b7-a89fccb38389",
            ...
            "amount": 10.0,
            "state": "capturable",
            ...
            "sourceId": "3066c73f-0894-44ee-8ae6-4cd8be32642e",
            ...
        },
        {
            "id": "2ad942b5-6e47-40ca-b991-9bbd02b36a44",
            ...
            "amount": 11.51,
            "state": "capturable",
            ...
            "sourceId": "f04ac3b4-016a-4c75-a093-20115bd27b5b",
            ...
        }
    ],
    ...
    "checkoutId": "afb203a4-6ca8-4748-9450-4586969a17ca"
}
```
{% endtab %}
{% endtabs %}

## How Digital River handles captures, cancels, and refunds

When[ pairing store credit with a primary payment source](applying-store-credit-legacy.md#pairing-store-credit-with-a-primary-payment-source), you should be aware of the logic Digital RIver uses to [capture charges](applying-store-credit-legacy.md#how-we-capture-store-credit), [cancel charges](applying-store-credit-legacy.md#how-we-cancel-store-credit) and[ process refunds](applying-store-credit-legacy.md#how-we-refund-store-credit).

### How we capture store credit

When you [notify Digital River that an order is partially or completely fulfilled](../../../order-management/informing-digital-river-of-a-fulfillment.md), we attempt to [capture](../../../order-management/orders/payment-charges/#captures) the [charge](../../../order-management/orders/payment-charges/) created from the `customerCredit` [source](../../../payments/payment-sources/) _before_ capturing the charge generated from the [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources).

The following example [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) demonstrates this concept. The order contains a single `items[]` with a `quantity` of `2` and its `totalAmount` is `26.89`. The order was created with a `creditAmount` of `11.0` and a supplemental credit card to cover the shortfall. As a result, two objects are contained in its `charges[]`.

So, in this example, when a [`POST /fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments/operation/createFulfillments) with a `quantity` of `1` gets submitted, thereby notifying Digital River of a partial fulfillment, we completely capture the charge `amount` created from `customerCredit` and move that charge's [`state`](../../../order-management/orders/payment-charges/#the-charge-lifecycle) to `complete`.&#x20;

But, since not all of the order's `items[]` are fulfilled, the charge `amount` created from the `creditCard` is only partially captured. As a result, that charge's `state` remains `capturable`.

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "185326550336",
    ...
    "totalAmount": 26.89,
    "subtotal": 25.0,
    "totalTax": 1.89,
    ...
    "items": [
        {
            "id": "106494910336",
            "skuId": "6b04ac06-0858-456c-90aa-235772dea9e2",
            "amount": 20.0,
            "quantity": 2,
            ...
        }
    ],
    ...
    "creditAmount": 11.0,
    "sources": [
        {
            "id": "21216ef6-d153-445a-8c81-3d912dfcf63a",
            ...
            "type": "customerCredit",
            ...
            "amount": 11.0,
            ...
            "customerCredit": {}
        },
        {
            "id": "10103f7f-ce6f-47f2-b064-47931779ebea",
            ...
            "type": "creditCard",
            ...
            "amount": 15.89,
            ...
            "paymentSessionId": "cac4fac7-8c54-46d8-86b1-c595a963d719",
            ...
            "creditCard": {
                "brand": "Visa",
                "expirationMonth": 7,
                "expirationYear": 2027,
                "lastFourDigits": "1111"
            }
        }
    ],
    ...
    "charges": [
        {
            "id": "84cdf3e6-f70e-49ca-8847-248d039f66d9",
            ...
            "amount": 11.0,
            "state": "complete",
            "captured": true,
            "captures": [
                {
                    "id": "a57b0805-4b57-46ec-a963-124ada0b536a",
                    "createdTime": "2021-03-08T21:14:51Z",
                    "amount": 11.0,
                    "state": "complete"
                }
            ],
            ...
            "sourceId": "21216ef6-d153-445a-8c81-3d912dfcf63a",
            ...
        },
        {
            "id": "60bbc0e7-affc-46ed-a3e8-3171d4de01cb",
            ...
            "amount": 15.89,
            "state": "capturable",
            "captured": true,
            "captures": [
                {
                    "id": "42253229-ad78-4c64-8096-9bb4138b4433",
                    "createdTime": "2021-03-08T21:14:51Z",
                    "amount": 2.45,
                    "state": "complete"
                }
            ],
            ...
            "sourceId": "10103f7f-ce6f-47f2-b064-47931779ebea",
            ...
        }
    ],
    ...
    "checkoutId": "9d92cc87-0e22-4dbe-bc76-e9d8eba1435f"
}
```
{% endtab %}
{% endtabs %}

### How we cancel store credit

When you [notify us that an order is partially or completely cancelled](../../../order-management/informing-digital-river-of-a-fulfillment.md), we attempt to [cancel](../../../order-management/orders/payment-charges/#cancels) the [charge](../../../order-management/orders/payment-charges/) created from the [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) _before_ cancelling the charge generated from the `customerCredit`.

The following example [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) demonstrates this concept. The order contains a single `items[]` with a `quantity` of `2` and its `totalAmount` is `20.0`. The order was created with a `creditAmount` of `5.0` and a supplemental credit card to cover the shortfall. As a result, two objects are contained in its `charges[]`.

So, in this example, when a [`POST /fulfillments`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Fulfillments/operation/createFulfillments) with a `cancelQuantity` of `1` gets submitted, we partially cancel the charge `amount` created from the `creditCard` source. Note that no cancels have been performed yet on the charge generated from the `customerCredit`.

{% tabs %}
{% tab title="Order" %}
```javascript
T{
    "id": "186017330336",
    ...
    "totalAmount": 20.0,
    "subtotal": 20.0,
    "totalTax": 0.0,
    ...
    "items": [
        {
            "id": "107253530336",
            "skuId": "c59bc37a-1351-4efe-939a-7f15381ed905",
            "amount": 20.0,
            "quantity": 2,
            ...
        }
    ],
    ...
    "creditAmount": 5.0
    "sources": [
        {
            "id": "9110f993-075c-446b-a557-858adce4463e",
            "type": "creditCard",
            "amount": 15.0,
            ...
            "creditCard": {
                "brand": "Visa",
                "expirationMonth": 7,
                "expirationYear": 2027,
                "lastFourDigits": "1111"
            }
        },
        {
            "id": "221e9fa6-2cdb-4bda-aaf4-1c6edb185441",
            "type": "customerCredit",
            "amount": 5.0,
            "customerCredit": {}
        }
    ],
    "charges": [
        {
            "id": "0d08d450-3c87-4456-9900-5c7e2009d7ce",
            ...
            "amount": 15.0,
            "state": "capturable",
            "captured": false,
            "refunded": false,
            "cancels": [
                {
                    "id": "c92fc885-d53b-42ba-ba5a-7a32a9e5f6d2",
                    "createdTime": "2021-03-18T20:27:20Z",
                    "amount": 10.0,
                    "state": "complete"
                }
            ],
            "sourceId": "9110f993-075c-446b-a557-858adce4463e",
            ...
        },
        {
            "id": "15f0f926-206a-4843-a96f-2fb07bc44087",
            ...
            "amount": 5.0,
            "state": "capturable",
            "captured": false,
            "refunded": false,
            "sourceId": "221e9fa6-2cdb-4bda-aaf4-1c6edb185441",
            ...
        }
    ],    
    ...
}
```
{% endtab %}
{% endtabs %}

### How we refund store credit

When you [issue a refund](../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md) on an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) that uses store credit, the refund is first applied to the [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources) and then the store credit.

The following example [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) demonstrates this concept. The order was funded with store credit and a supplemental credit card. It was completely fulfilled, meaning both of its [`charges[]`](../../../order-management/orders/payment-charges/) were fully [captured](../../../order-management/orders/payment-charges/#captures) and moved into a [`complete`](../../../order-management/orders/payment-charges/#the-charge-lifecycle) state.

After being fulfilled, the client system submitted an [order-level refund](../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md#order-level-percent-refund-request) of 50 percent.

Notice that the credit card is fully refunded. However, the `customerCredit` is only partially refunded. This means that in any subsequent refund requests, the order's remaining [`availableToRefundAmount`](../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md#available-to-refund-amount) will be issued to the `customerCredit`.

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "185317330336",
    ...
    "totalAmount": 26.89,
    "subtotal": 25.0,
    ...
    "totalTax": 1.89,
    ...
    "totalShipping": 5.0,
    "items": [
        {
            "id": "106484310336",
            "skuId": "6b04ac06-0858-456c-90aa-235772dea9e2",
            "amount": 20.0,
            "quantity": 2,
            ...
            "tax": {
                "rate": 0.07525,
                "amount": 1.51
            ...
            "availableToRefundAmount": 13.44,
            ...
        }
    ],
    ...
    "creditAmount": 20.0,
    "sources": [
        {
            "id": "b77fec60-590b-4330-8d6b-bb069cf5545e",
            ...
            "type": "customerCredit",
            ...
            "amount": 20.0,
            ...
            "state": "consumed",
            ...
            "customerCredit": {}
        },
        {
            "id": "b73d759c-eff0-4327-960f-75b86dd87764",
            ...
            "type": "creditCard",
            ...
            "amount": 6.89,
            ...
            "state": "consumed",
            ...
            "creditCard": {
                "brand": "Visa",
                "expirationMonth": 7,
                "expirationYear": 2027,
                "lastFourDigits": "1111"
            }
        }
    ],
    "refundedAmount": 13.45,
    "state": "complete",
    ...
    "charges": [
        {
            "id": "b80d59ee-546d-4f04-8fc9-8c4f630594aa",
            ...
            "amount": 20.0,
            "state": "complete",
            "captured": true,
            "captures": [
                {
                    "id": "012d0a54-8e34-48a5-b5e0-5d6735901d95",
                    "createdTime": "2021-03-08T20:01:34Z",
                    "amount": 20.0,
                    "state": "complete"
                }
            ],
            "refunded": true,
            "refunds": [
                {
                    "createdTime": "2021-03-08T20:06:44Z",
                    "amount": 6.56,
                    "state": "complete"
                }
            ],
            "sourceId": "b77fec60-590b-4330-8d6b-bb069cf5545e",
            ...
        },
        {
            "id": "c7464db6-33c8-45f6-9cb6-4fa5a2a658c9",
            ...
            "amount": 6.89,
            "state": "complete",
            "captured": true,
            "captures": [
                {
                    "id": "191c66ac-7713-49f3-a605-ec9fae84fbf9",
                    "createdTime": "2021-03-08T20:01:34Z",
                    "amount": 6.89,
                    "state": "complete"
                }
            ],
            "refunded": true,
            "refunds": [
                {
                    "createdTime": "2021-03-08T20:06:44Z",
                    "amount": 6.89,
                    "state": "complete"
                }
            ],
            "sourceId": "b73d759c-eff0-4327-960f-75b86dd87764",
            ...
        }
    ],
    ...
    "capturedAmount": 26.89,
    ...
    "availableToRefundAmount": 13.44,
    "checkoutId": "dc16d13b-d379-45bc-9be1-f3bd798410d2"
}
```
{% endtab %}
{% endtabs %}
