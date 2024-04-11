---
description: Learn how to apply store credit
---

# Applying store credit

{% hint style="warning" %}
This page explains how to use store credit in [versions](../../../general-resources/versioning.md) `2021-03-23` and higher. For versions `2020-09-30`, `2020-12-17`, and `2021-02-23`, refer to [Applying store credit (legacy)](applying-store-credit-legacy.md).
{% endhint %}

For non-recurring transactions, customers can pay using store credit, a unique payment type that allows you to connect your credit management system to the Digital River APIs. With store credit, you manage customers' credit on your end, and can display the amount available to them during the checkout process.

{% hint style="info" %}
Store credit is a [single-use payment source](../../../payments/payment-sources/#reusable-or-single-use) and therefore can't be saved to a [customer's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Customers) record.
{% endhint %}

You[ create the store credit payment source](applying-a-store-credit.md#creating-store-credit) and then [attach the resource to the checkout](applying-a-store-credit.md#attaching-store-credit-to-checkouts).  Once the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) is created, you'll also need to [search for store credit and deduct its amount](applying-a-store-credit.md#handling-store-credit-in-orders).&#x20;

With store credit, the steps necessary to [handle fulfillments](../../../order-management/fulfillments.md) and [request refunds](../../../order-management/returns-and-refunds-1/refunds/issuing-refunds.md) remain the same, but, if an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `sources[]` contain store credit and a [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources), you should be aware of how [Digital River handles captures, cancels, and refunds](../../../payments/payment-sources/using-the-source-identifier.md#how-we-handle-captures-cancels-and-refunds).

{% hint style="info" %}
Digital River API does not currently support Amazon Pay with store credit.
{% endhint %}

## Creating store credit

When customers opt to pay with store credit and they've specified an allowable amount, send your [confidential API key](../../../administration/dashboard/developers/api-keys/#standard-keys) in a [`POST /sources`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources/operation/createSources).

When defining the request:

* Retrieve the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`payment.session.id`](./#payment-session-identifier) and use it to set `paymentSessionId`.&#x20;
* Pass the `amount` of credit you're extending the customer.
* Set `type` to `customerCredit`.&#x20;
* Use `upstreamId` to pass the identifier of the line of credit in your system.&#x20;
* Send an empty `customerCredit` object.

{% hint style="info" %}
An `owner` hash table is optional and can be used to meet [our billing address requirements](providing-address-information.md#billing-address-requirements).&#x20;
{% endhint %}

```
curl --location --request POST 'https://api.digitalriver.com/sources' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <Your secret API key>' \
...
--data-raw '{
	"type": "customerCredit",
        "paymentSessionId": "96e199dc-e9a4-4bb1-86ca-2adc502e62bf",
    	"amount": 12.50,
    	"upstreamId": "76-87-1298",
	"customerCredit": {
	}
}'
```

A response with a `201 OK` status code contains a unique [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) with a `type` of `customerCredit` whose [`state`](../../../payments/payment-sources/#source-state) is `chargeable`.

{% hint style="info" %}
If you pass `paymentSessionId` and set the checkout's [`billTo`](providing-address-information.md#billing-address-requirements) prior to sending the create source request, Digital River retrieves that data and uses it to populate the source's `owner`. We also retrieve the checkout's [`currency`](selecting-a-currency.md) and use it to set the source's `currency`.&#x20;
{% endhint %}

{% tabs %}
{% tab title="Source" %}
```javascript
{
    "id": "f2f6bced-37a0-4b10-965a-7c4f27e59288",
    "createdTime": "2022-10-13T19:52:57Z",
    "type": "customerCredit",
    "currency": "USD",
    "amount": 12.5,
    "reusable": false,
    "state": "chargeable",
    "upstreamId": "76-87-1298",
    "owner": {
        "firstName": "Chase",
        "lastName": "Marshall",
        "address": {
            "line1": "4321 Any Road W",
            "city": "Minneapolis",
            "postalCode": "55401",
            "state": "MN",
            "country": "US"
        }
    },
    "paymentSessionId": "96e199dc-e9a4-4bb1-86ca-2adc502e62bf",
    "clientSecret": "f2f6bced-37a0-4b10-965a-7c4f27e59288_fba8241d-b0f4-4305-bad4-1ecff4e03d3b",
    "customerCredit": {},
    "liveMode": false
}
```
{% endtab %}
{% endtabs %}

## Attaching store credit to checkouts

After you [create a store credit payment source](applying-a-store-credit.md#creating-store-credit), you'll need to retrieve its `id` and use that value to [associate the source with the checkout](../../../payments/payment-sources/using-the-source-identifier.md#attaching-sources-to-checkouts).&#x20;

```
curl --location --request POST 'https://api.digitalriver.com/checkouts/e869b46e-dd24-4896-a79e-6ad80bbbd460/sources/f2f6bced-37a0-4b10-965a-7c4f27e59288' \
--header 'Content-Type: application/json' \
--header 'Authorization: <Your secret API key>' \
...
--data-raw ''
```

Before submitting this request, check to determine whether the source's `amount` is less than or equal to the checkout's [`payment.session.amountRemainingToContribute`](payment-sessions.md#amount-contributed-and-amount-remaining-to-be-contributed). If that's _not_ the case, then the following error is thrown:

{% code title="409 Conflict" %}
```json
{
    "type": "conflict",
    "errors": [
        {
            "code": "session_source_amount_too_large",
            "message": "Source amount(s) exceed session amount"
        }
    ]
}
```
{% endcode %}

At what point in the flow you should submit this request depends on whether customers are (1) paying entirely with store credit, (2) combining store credit with a single-use [primary payment source](../../../payments/payment-sources/using-the-source-identifier.md#primary-payment-sources), or (3) combining store credit with a [reusable](../../../payments/payment-sources/#reusable-or-single-use) primary payment source.

{% hint style="info" %}
For details, refer to [Combining primary and secondary sources](../../../payments/payment-sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources) on the [Managing sources](../../../payments/payment-sources/using-the-source-identifier.md) page.&#x20;
{% endhint %}

In any of these cases, Digital River first computes taxes based on the checkout's `totalAmount`, and then applies the store credit.

## Handling store credit in orders

After the [necessary payment preconditions](payment-sessions.md#how-to-determine-when-to-create-an-order) are met to successfully [convert the checkout to an order](../../../order-management/creating-and-updating-an-order.md#creating-an-order-with-the-checkout-identifier), and the [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) `state` is [`accepted`](../../../order-management/creating-and-updating-an-order.md#handling-accepted-orders), iterate through its `sources[]` and identify any that have a `type` of `customerCredit`. For each of these objects, use its `upstreamId` to look up the line of credit in your system and deduct what's available by `amount`.&#x20;

{% tabs %}
{% tab title="Order" %}
```javascript
{
    "id": "242764070336",
    ...
    "payment": {
        "charges": [
            {
                "id": "db5f33b5-3b1a-40c7-9e63-0e5b8a7dcad5",
                "createdTime": "2022-10-13T19:55:58Z",
                "currency": "USD",
                "amount": 12.5,
                "state": "capturable",
                "captured": false,
                "refunded": false,
                "sourceId": "f2f6bced-37a0-4b10-965a-7c4f27e59288",
                "type": "customer_initiated"
            },
            {
                "id": "f30999a2-23c3-46b0-ae35-335f7ddd967b",
                "createdTime": "2022-10-13T19:55:57Z",
                "currency": "USD",
                "amount": 14.51,
                "state": "capturable",
                "captured": false,
                "refunded": false,
                "sourceId": "a83ad586-c4ad-4b27-8676-1e0a897cf029",
                "type": "customer_initiated"
            }
        ],
        "sources": [
            {
                "id": "a83ad586-c4ad-4b27-8676-1e0a897cf029",
                "type": "creditCard",
                "amount": 14.51,
                "owner": {
                    "firstName": "Chase",
                    "lastName": "Marshall",
                    "email": "marshallsBillingEmail@digitalriver.com",
                    "address": {
                        "line1": "Any other road W",
                        "city": "Eagan",
                        "postalCode": "55122",
                        "state": "MN",
                        "country": "US"
                    }
                },
                "creditCard": {
                    "brand": "Visa",
                    "expirationMonth": 7,
                    "expirationYear": 2027,
                    "lastFourDigits": "1111"
                }
            },
            {
                "id": "f2f6bced-37a0-4b10-965a-7c4f27e59288",
                "type": "customerCredit",
                "amount": 12.5,
                "upstreamId": "76-87-1298",
                "owner": {
                    "firstName": "Chase",
                    "lastName": "Marshall",
                    "address": {
                        "line1": "4321 Any Road W",
                        "city": "Minneapolis",
                        "postalCode": "55401",
                        "state": "MN",
                        "country": "US"
                    }
                },
                "customerCredit": {}
            }
        ],
        "session": {
            "id": "96e199dc-e9a4-4bb1-86ca-2adc502e62bf",
            "amountContributed": 27.01,
            "amountRemainingToBeContributed": 0.0,
            "state": "complete",
            "clientSecret": "96e199dc-e9a4-4bb1-86ca-2adc502e62bf_57cb6a31-9594-4879-8cbd-740121cd35f7"
        }
    },
    "state": "accepted",
    "stateTransitions": {
        "accepted": "2022-10-13T19:55:59Z"
    },
    ...
    "checkoutId": "e869b46e-dd24-4896-a79e-6ad80bbbd460"
}
```
{% endtab %}
{% endtabs %}
