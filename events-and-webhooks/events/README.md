---
description: Learn about the structurer of events and when they are created.
---

# Events

When something noteworthy happens in your account, we create a data object. More specifically, an event is created when the state of another API resource changes. Your integration can use these events to listen for and handle important updates in your account.

In the Commerce APIs, there are numerous [event types](./#event-types) that you can subscribe to when you [create ](../webhooks/creating-a-webhook.md)or [edit a webhook](../webhooks/editing-a-webhook.md). There are, however, certain [key event types](event-types.md) that we recommend every integration monitor.

In nearly all cases, an [event's data](./#event-data) contains the resource whose state changed.

To subscribe to an event, you need to set up [webhooks ](../webhooks/)that send designated events directly to an endpoint on your server. In [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), you'll find a complete list of our supported event types. To access this list, sign in to [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), select **Administration**, **** and click **Webhook Service**.

## Event types

[Event types](event-types.md) use the following naming conventions: `subscription.created`

The name of the event usually reflects the current state of the resource. For example, when a subscription moves into the created state, we create a `subscription.created` event, and when a subscription moves into a `renewed` state, we create a `subscription.renewed` event.

## Event data

In the payload of an event, the data object typically contains the resource that changed. For example, the data object of a `subscription.created` event is a `subscription` in the created state.
