---
description: >-
  Gain a better understanding of what causes a webhook to get disabled and how
  to prevent that from happening
---

# Preventing webhooks from getting disabled

To reduce stress on our nodes and minimize unwanted downtimes, Digital River automatically disables [webhooks](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Webhooks) that repeatedly time out, do not respond, or return errors.

To prevent a webhook from being deactivated, we recommend that you:

* [Configure it to deliver an immediate response](preventing-webhooks-from-getting-disabled.md#respond-immediately)
* [Deselect problematic events](preventing-webhooks-from-getting-disabled.md#deselect-problematic-events)
* [Provide descriptive error messages](preventing-webhooks-from-getting-disabled.md#provide-informative-error-messages)
* [Keep your endpoints available](preventing-webhooks-from-getting-disabled.md#keep-endpoints-available)
* [Correctly map test environments](preventing-webhooks-from-getting-disabled.md#map-test-environments)

## Respond immediately

Make sure your [webhooks](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Webhooks) respond to Digital River’s callbacks within 3000 milliseconds. Anything longer than that is considered a timeout.&#x20;

To let us know that you're planning on handling a callback asynchronously, your webhooks should immediately acknowledge it by sending an [HTTP status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) of `202 Accepted`. Once that operation is complete, you can process the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) on your end.

## Deselect problematic events

If you have a [webhook](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Webhooks) that frequently fails or experiences timeouts, it might be subscribed to an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) containing JSON keys that it can't process. To solve this, either deselect the problematic event by [editing the webhook in the Dashboard](../../administration/dashboard/developers/webhooks/editing-a-webhook.md) or modify your handler’s logic.  Additionally, ensure that the webhook only subscribes to events required by your application and deselect any that are not.

## Provide informative error messages

If the [`data.object`](events-1/#event-data) of an [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) is not what you expected, perhaps because it's missing a key or a value is incorrectly formatted, respond with an [HTTP status code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) of  `400 Bad Request` and ensure the error has a descriptive `message`. By detailing the specific issue (missing field, invalid value, etc.), Digital River is able to better identify and resolve the problem.

## Keep endpoints available

Your webhook endpoints should always be up and running. If you plan on terminating an endpoint after  your testing is complete, first disable the webhook that it belongs to. You can [do this in Dashboard](../../administration/dashboard/developers/webhooks/editing-a-webhook.md) or by submitting a [webhook patch request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Webhooks/operation/updateWebhooks) with `enabled` set to `false`.  &#x20;

## Map test environments

Your Digital River account gives you access to two of Digital River's environments, [test and production](../../developer-resources/api-structure.md#test-and-production-environments). Your system, however, may have more than a single test environment. For instance, developers on your team might write code in their local environments and then promote it to dev, where QA runs various tests before advancing it to staging once they're satisfied with it.

However, if each of these environments has a different [webhook](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Webhooks) endpoint that handles the same event and they're all [saved to the same Digital River test account](../../administration/dashboard/developers/webhooks/creating-a-webhook.md), you're likely to encounter problems.

For example, let’s say you have three testing environments: A, B, and C. Each has a unique webhook `address` within the same [Digital River Dashboard](https://dashboard.digitalriver.com/login) account, and all are listening for the [event](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events) with a [`type`](events-1/#event-types) of  `order.accepted`. If you create an [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) in A and its [`state`](../orders/the-order-lifecycle.md#order-states-and-events) moves to `accepted`, then your webhook handler in that environment is likely to succeed. But since that [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders) doesn’t exist in B and C, the handlers in those environments will likely return an error.

{% hint style="success" %}
This doesn’t mean your Digital River test account should only contain a single webhook. There are valid reasons for having multiple endpoints. For instance, you might want one to handle `order.accepted` by initiating product fulfillment and another to handle `fulfillment.created` by sending an email to customers to let them know their products have shipped.
{% endhint %}

The recommended solution to this problem is to have a single environment on your end that maps to Digital River’s test environment. This ensures our webhook processor will deliver [event payloads](events-1/#event-data) with JSON keys that have values which exist in your environment, thereby reducing the probability of returning an error.
