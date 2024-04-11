---
description: Learn how to refund transactions that use delayed payment methods
---

# Refunding asynchronous payment methods

Prior to issuing a refund on an [asynchronous payment method](../../../payments/payment-sources/#synchronous-or-asynchronous), such as [Wire Transfer](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/wire-transfer.md), [Online Banking](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/online-banking.md), and [Konbini](../../../payments/payment-integrations-1/digitalriver.js/payment-methods/konbini.md), payment providers must usually collect additional information from customers.

After you [request a refund](issuing-refunds.md) be applied to these types of payment methods, Digital River typically moves the [refund's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Refunds) `state` to `pending_information`, which triggers the creation of a [`refund.pending_information`](issuing-refunds.md#pending-information-refunds) event.

The [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) `data.object` contains `tokenInformation`. Within this data structure is a `token` and an `expiresTime`. The `expiresTime` of the `token` is 30 days after the event's `createdTime`.

{% code title="refund.pending_information" %}
```javascript
{
    "id": "3830d505-f004-4924-b1d5-8c877f164726",
    "type": "refund.pending_information",
    "data": {
        "object": {
            "id": "re_d1988e09-eec8-48f4-8077-b6c955c84e69",
            "amount": 33.0,
            "createdTime": "2022-03-11T20:35:21Z",
            "currency": "JPY",
            "items": [],
            "orderId": "219187180336",
            "refundedAmount": 0.0,
            "state": "pending_information",
            "tokenInformation": {
                "token": "17bc3273-b588-420f-bd1f-49a89eec6322",
                "expiresTime": "2022-06-09T20:37:21.087Z"
            },
            "liveMode": false,
            "charges": [
                {
                    "id": "5253e76e-e92f-4128-acad-78c26d7999b8",
                    "captured": true,
                    "refunded": true,
                    "refunds": [
                        {
                            "createdTime": "2022-03-11T20:37:21Z",
                            "amount": 33.0,
                            "state": "pending_information"
                        }
                    ],
                    "sourceId": "0e311505-0955-47df-9808-beb34b5a8b30"
                }
            ]
        }
    },
    "liveMode": false,
    "createdTime": "2022-03-11T20:37:30.556222Z",
    ...
    "digitalriverVersion": "2021-12-13"
}
```
{% endcode %}

Handle `refund.pending_information` events by passing `tokenInformation` and `expiresTime` to your front-end.

On your page that is dedicated to collecting bank information during refunds, use `token` to set `refundToken` in the [create offline refund element's](../../../developer-resources/reference/elements/offline-refund-elements.md#creating-an-offline-refund-element) configuration object. Once invoked, this method sends the token to Digital River's payment services, requesting a schema that defines the data fields customers must complete.

On the same page, [mount the element](../../../developer-resources/reference/elements/offline-refund-elements.md#offlinerefund-mount) and inform customers that they must enter and submit the requested information by `expiresTime`. In the designated container, a form with the required fields is displayed to customers and the [on ready event](../../../developer-resources/reference/elements/offline-refund-elements.md#ready) is triggered.

{% hint style="info" %}
Make sure you display the expiration time in a more human readable form.
{% endhint %}

Once customers follow these instructions and the data is accepted, Digital River sends a[ change event](../../../developer-resources/reference/elements/offline-refund-elements.md#change). Handle it by redirecting customers to a page that notifies them the refund request has been successfully submitted. You can also use either [`unmount()`](../../../developer-resources/reference/elements/offline-refund-elements.md#offlinerefund-unmount) or [`destroy()`](../../../developer-resources/reference/elements/offline-refund-elements.md#offlinerefund-destroy)to remove the offline refund element from the data collection page.

Once you receive either the `refund.complete` or `refund.failed` event, send the appropriate notification to customers.
