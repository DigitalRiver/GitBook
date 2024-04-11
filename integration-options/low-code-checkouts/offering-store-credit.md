---
description: >-
  Learn how to offer your customers access to their store credit in low-code
  checkouts
---

# Offering store credit

Store credit is a unique payment type that allows you to connect your credit management system to the Digital River APIs.&#x20;

With store credit, you manage a customer's credit on your end and then pass that data to Digital River in [create checkout-session requests](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) so we can offer it as an option in [Prebuilt Checkou](drop-in-checkout.md)t or [Components](implementing-a-components-checkout.md), our [low-code checkout solutions](./).&#x20;

On this page, you'll find information on:

* [Providing a store credit endpoint](offering-store-credit.md#providing-a-store-credit-endpoint)
* [Managing store credit in checkouts](offering-store-credit.md#managing-store-credit-in-checkouts)
* [Processing store credit after it's been successfully applied to an order](offering-store-credit.md#processing-store-credit-in-orders)

## Providing a store credit endpoint

You can [provide a store credit endpoint in Digital River Dashboard](../../administration/dashboard/settings/prebuilt-checkout.md#configure-a-store-credit-callout). This allows you to manage the store credit you offer customers more closely and better defeat fraudulent attempts to abuse it. &#x20;

If customers request to use their store credit in the payment collection stage, Digital River calls this endpoint to determine whether it should be authorized. If your hosted service approves the request, Digital River applies the credit to the purchase. Otherwise, we prevent the customer from using it.

When configuring your endpoint, you must enter a username and password. In both the [payment authorization request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Store-credit-callout/operation/storeCreditsCallout) and the [removed store credit notification](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Store-credit-callout/operation/removeStoreCreditsCallout) that Digital River sends to your service, these credentials are transmitted using the [basic authentication scheme](https://en.wikipedia.org/wiki/Basic\_access\_authentication).

## Managing store credit in checkouts

If you want to give customers the option to use their store credit in a [Prebuilt Checkout](drop-in-checkout.md#drop-in-checkout-modal-window) or the [Payment component](../../developer-resources/digitalrivercheckout.js-reference/digitalrivercheckout-object/components/payment-component.md), then the body of your [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession) must include [`options.storeCredits[]`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#store-credits).&#x20;

In the payment collection stage, customers might request to use that credit. Once successfully applied to the transaction, they might also want to remove that payment option.

For details on handling both scenarios, refer to [Attaching store credit](offering-store-credit.md#attaching-store-credit) and [Removing store credit](offering-store-credit.md#removing-store-credit).

### Attaching store credit

Whenever a customer requests to use their store credit, Digital River checks whether you have a [saved endpoint](offering-store-credit.md#providing-a-store-credit-endpoint).  &#x20;

If none exists, we use the [`upStreamId`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#upstreamid) and [`amount`](../../developer-resources/digital-river-api-reference/checkout-sessions.md#amount) of the `storeCredits[]` selected by that customer to create a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) with a [`type`](../../payments/payment-sources/#supported-payment-methods) of `customerCredit`,  and then add it to the [checkout-session’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `sources[]`.

However, if we determine that a saved endpoint does exist, we send a [store credit authorization request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Store-credit-callout/operation/storeCreditsCallout) to it.

At a minimum, the body of this [`POST /checkouts/store-credits`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Store-credit-callout/operation/storeCreditsCallout) will contain the `amount` and `upstreamId` of the selected store credit, plus a `sessionId` that uniquely identifies the [checkout-session](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions). If you sent `upstreamId` in the [create checkout-session request](drop-in-checkout.md#creating-a-checkout-session), we also assign this value to `sessionUpstreamId`.

To handle our request, you’ll need to have a hosted service set up that uses `upstreamId` to look up that line of credit in your system and then checks whether its available amount is sufficient to cover the `amount` being requested.

If your authorization service determines this to be the case, send a reply with `approval` set to `true`. Make sure your response also specifies the `amount` that's been approved. This value can be lower than the `amount` Digital River sent in the request, but it should be greater than `0`.\
\
Otherwise, if you reject the request, set `approval` to `false`. In this case, you don't need to return `amount`.&#x20;

Whether your service approves or rejects the request, it should return a `200 OK` status code and the body of the response should pass back the same `upstreamId` so that we can check the values for parity.&#x20;

Digital River handles your response by looking at the value of `approval`.

If it’s `true`, we use `upstreamId` and `amount` to create a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources) with a [`type`](../../payments/payment-sources/#supported-payment-methods) of `customerCredit`, add it to the [checkout-session’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `sources[]` and then update the experience.

{% tabs %}
{% tab title="Prebuilt Checkout" %}
In [Prebuilt Checkout](drop-in-checkout.md), after customers request to apply or remove their store credit, Digital River updates the totals in the order summary section.

<figure><img src="../../.gitbook/assets/image (131).png" alt="" width="563"><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Payment component" %}
<figure><img src="../../.gitbook/assets/image (128).png" alt="" width="563"><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

If `approval` is `false`, Digital River doesn’t create a [source](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Sources). Instead, we display a generic error message to users.

{% tabs %}
{% tab title="Prebuilt Checkout" %}
<figure><img src="../../.gitbook/assets/store credit error.png" alt="" width="563"><figcaption></figcaption></figure>


{% endtab %}

{% tab title="Payment component" %}
<figure><img src="../../.gitbook/assets/image (104).png" alt="" width="563"><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

### Removing store credit

In the payment stage, customers might also attempt to remove a store credit that's already been successfully applied.

Each time a customer makes this request, Digital River removes that payment option from the [checkout-session’s](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions) `sources[]` and then determines whether you have a [saved store credit endpoint](offering-store-credit.md#providing-a-store-credit-endpoint).&#x20;

If an endpoint exists, Digital River passes the store credit’s `upstreamId` as a path parameter in a [removed payment notification](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Store-credit-callout/operation/removeStoreCreditsCallout). The purpose of this [`DELETE /checkouts/store-credits/{upstreamId}`](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Store-credit-callout/operation/removeStoreCreditsCallout) is to notify you that the customer has opted to remove that payment option.

Your service should respond with a `204 No Content` status code and an empty body.&#x20;

Once Digital River receives this code, we delete that `customerCredit` [source](../../payments/payment-sources/using-the-source-identifier.md).&#x20;

## Processing store credit in orders

If you're offering customers store credit, you should be set up to process it after it's been successfully applied to an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders). To do this, [configure a webhook](../../administration/dashboard/developers/webhooks/creating-a-webhook.md) to listen for the [event](../../order-management/events-and-webhooks-1/events-1/) with a [`type`](../../order-management/events-and-webhooks-1/events-1/#event-types) of `checkout_session.order.created`.&#x20;

If the event’s [`data.object`](../../order-management/events-and-webhooks-1/events-1/#event-data) contains one or more `payment.sources[]` whose `type` is `customerCredit`, then customers applied their store credit to that transaction.&#x20;

For each `payment.sources[]` of this `type`, we recommend that you use its `upstreamId` to look up the line of credit in your system and then deduct how much is available by `amount`.

```json
{
    "id": "bc7c8d7b-c9b6-473c-8de1-1381afcae70a",
    "type": "checkout_session.order.created",
    "data": {
        "object": {
            "id": "253375130336",
            "checkoutId": "d868418a-1302-4685-8a37-cab789164aea",
            "checkoutSessionId": "a5e8133f-d874-4b48-b2c5-88f31d9860eb",
            ...
            "payment": {
                ...
                "sources": [
                    {
                        "id": "3848c570-c12c-4383-9588-8d4765a6f753",
                        "createdTime": "2023-01-24T16:46:20Z",
                        "type": "customerCredit",
                        "currency": "USD",
                        "amount": 11.4,
                        "reusable": false,
                        "state": "consumed",
                        "upstreamId": "7654-2345-0987-123456",
                        "clientSecret": "3848c570-c12c-4383-9588-8d4765a6f753_56424640-f3e3-43a8-b641-d0c498f88e1d",
                        "customerCredit": {}
                    },
                    {
                        "id": "57a3df40-86d7-437f-bc9b-4de2e7b2d0d1",
                        "createdTime": "2023-01-24T16:47:07Z",
                        "type": "creditCard",
                        "currency": "USD",
                        "amount": 53.99,
                        "reusable": false,
                        "state": "consumed",
                        "owner": {
                            "firstName": "John",
                            "lastName": "Smith",
                            "email": "jsmith@digitalriver.com",
                            "address": {
                                "line1": "10380 Bren Rd W",
                                "city": "Minnetonka",
                                "postalCode": "55129",
                                "state": "MN",
                                "country": "US"
                            },
                            "organization": "Digital River",
                            "additionalAddressInfo": {
                                "neighborhood": "Centro",
                                "phoneticFirstName": "ヤマダ",
                                "phoneticLastName": "タロ",
                                "division": "営業部"
                            }
                        },
                        "paymentSessionId": "0afec58c-1f3a-4082-a0ad-86736a904ad7",
                        "clientSecret": "57a3df40-86d7-437f-bc9b-4de2e7b2d0d1_443ca230-4330-4f0c-9b6a-3ea288362227",
                        "creditCard": {
                            "brand": "MasterCard",
                            "expirationMonth": 12,
                            "expirationYear": 2023,
                            "lastFourDigits": "0008",
                            "fundingSource": "credit"
                        }
                    }
                ],
                ...
            },
            ...
        }
    },
    ...
}
```

