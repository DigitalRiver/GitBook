---
description: Learn how to use webhooks.
---

# Webhooks

Digital River uses webhooks to notify your application when events occur.

When an event occurs, Digital River will create an [Event ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)object and then send a webhook to your application (endpoint URL) through a `POST` request that contains the event and a timestamp for the event. You can set up multiple webhook endpoints to receive a single event. This allows you to receive real-time updates on the state of your SKUs, orders, fulfillments, returns, and refunds.

The Webhook resource can take specific actions when events occur. For example, you can expect to receive a `checkout.created` event when a customer begins the checkout process. An `order.accepted` event signals that the order is [ready to fulfill](../../fulfillments.md) and a `fulfillment.created` event indicates an invoice is generated.

Webhook endpoints can be better secured by using a signing secret and authenticating via [OAuth](creating-a-webhook.md#oauth-transport-type) or [basic authorization](creating-a-webhook.md#http-transport-type).

You can send webhooks to your customer that includes this tracking information. You can [create a webhook](creating-a-webhook.md) to subscribe to the event. When you receive the webhook, you can then share a file link with the customer without using a secret key.
