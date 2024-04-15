---
description: Learn about the structure of events and when they are created.
---

# Events

When something noteworthy happens in your account, we create an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events). More specifically, an event is created when the state of another API resource changes. Your integration can use these events to listen for and handle important updates in your account.

In the Digital River APIs, there are numerous [event types](./#event-types) that you can subscribe to. There are, however, certain [key event types](event-types.md) that we recommend every integration monitors.

In nearly all cases, an [event's data](./#event-data) contains the resource whose state changed.&#x20;

You can also subscribe to expanded events, which contain more data.&#x20;

To subscribe to an event, you need to set up [webhooks](../webhooks/) that send designated events directly to an endpoint on your server. In [Digital River Dashboard](../../../administration/dashboard/), you'll find a complete list of our supported event types. To access this list, [create a webhook](../../../administration/dashboard/developers/webhooks/creating-a-webhook.md) or [view the details of an existing webhook](../../../administration/dashboard/developers/webhooks/).

You can also use the [Events API](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) to [return a list of events](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/listEvents) or [retrieve an individual event](https://www.digitalriver.com/docs/digital-river-api-reference/#operation/retrieveEvents).‌

## Event types

[Events](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) use the following naming convention: `resource.event`.

The [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) `type` usually reflects the current state of that resource. For example, when an [order's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) [`state`](../../orders/the-order-lifecycle.md#order-states-and-events) moves to `accepted`, we create an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose `type` is [`order.accepted`](../../creating-and-updating-an-order.md#listening-for-the-order-accepted-event) and when an [invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices) becomes [`uncollectible`](../../../integration-options/checkouts/subscriptions/invoices.md#invoice-states), we create an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) whose `type` is `invoice.uncollectible`.

{% code title="Event" %}
```json
{
    "id": "86976837-18b5-473c-9a2e-7e774a827670",
    "type": "order.accepted",
    "data": {
        "object": {
            "id": "247468780336",
            ...
            "state": "accepted",
            ...
        }
    },
    ...
}
```
{% endcode %}

There are, however, certain exceptions. For example, an event with a `type` of [`subscription.extended`](event-types.md#subscription.extended) indicates that the [subscription's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions) [`state`](../../../developer-resources/digital-river-api-reference/subscriptions.md#state) remains  `active`. And even though [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) don't contain a state attribute, you can listen for `checkout.created`, `checkout.updated`, and `checkout.deleted` events.

{% hint style="info" %}
When an event occurs on a sub-resource, such as those with a `type` of `order.charge.cancelled`, the parent resource's state update event is not activated.
{% endhint %}

Some API requests trigger multiple events. For example, when a [subscription](../../../developer-resources/digital-river-api-reference/subscriptions.md) is created, two event types, `subscription.created` and `checkout.created`, are emitted.

## Event data

An [event's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) `data.object` typically contains the resource that changed.

Here are a couple of examples: (1) the `data.object` of an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](./#event-types) of [`order.blocked`](../../creating-and-updating-an-order.md#the-fraud-review-failure-event) is an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) whose [`state`](../../orders/the-order-lifecycle.md#order-states-and-events) is `blocked` and (2) the `data.object` of an event with a [`type`](./#event-types) of `order.charge.capture.complete` is a [charge](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Charges) that contains a [capture](../../orders/payment-charges/#captures) whose `state` is `complete`.

In a few cases, however, this pattern isn't strictly followed. For example, the `data.object` of a [`fulfillment_order.shipped`](../../../integration-options/checkouts/handling-digital-river-coordinated-fulfillments/global-fulfillments.md#shipped-events) contains a [shipment](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Shipments) resource and the payload of [`subscription.reminder`](../../../integration-options/checkouts/subscriptions/digital-river-coordinated-subscriptions.md#sending-a-reminder) is both a [subscription](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Subscriptions) and an [invoice](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Invoices).

An event's `data.previousAttributes` lists the resource's attributes that changed, along with the previous values of these attributes.‌
