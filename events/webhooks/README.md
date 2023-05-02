---
description: Learn about the webhooks.
---

# Webhooks

Digital River uses webhooks to notify your application when events occur.&#x20;

When an event occurs, Digital River will create a data object and send a webhook to your application (endpoint URL) through a POST request containing the event and timestamp. You can set up multiple webhooks endpoints to receive a single event. This allows you to receive real-time updates on the state of your order, line item, subscriptions, returns, and refunds.

You can use the Webhook Service page in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) or the [Webhooks API](https://www.digitalriver.com/docs/commerce-api-reference/#tag/Webhook-Event-Management) to [search](searching-for-a-webhook.md), [create](creating-a-webhook.md), [edit](editing-a-webhook.md), [enable](enabling-or-disabling-webhooks.md), [disable](enabling-or-disabling-webhooks.md), and [delete ](deleting-a-webhook.md)webhooks. You can also [reveal ](revealing-a-webhooks-secret.md)and [rotate ](rotating-a-webhooks-secret.md)webhook secrets. When you register your webhook URLs with Digital River, Digital River creates a data object and sends webhook events that notify your application any time an event occurs. The data object includes the type of event and the data associated with that event.&#x20;

Digital River uses webhooks to notify your application (endpoint URL) when events occur in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). A webhook contains the event and timestamp for the event. You can use the Webhooks Service in Global Commerce to [search](searching-for-a-webhook.md), [edit](editing-a-webhook.md), [create](creating-a-webhook.md), and [delete webhooks](deleting-a-webhook.md).

## **Webhook ID**

Each webhook has a unique identifier (ID). If you know the webhook ID, you can [search ](searching-for-a-webhook.md)for it from the Webhook Service page in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). A webhook ID only appears in the search results if it matches the text you type in the **Search** field.

## **Endpoint URL**

An endpoint URL is where the payload will be sent when the subscribed event happens. The endpoint URL must begin with either `http://` or `https://`.

The endpoint must return a `2xx` HTTP status code to acknowledge the receipt of an event. If the endpoint fails to acknowledge events over several days, the endpoint will be disabled. You did not receive the event if Digital River receives any response codes outside this range, you did not receive the event. For example, Digital River treats a URL redirection as a failure.

## **Secret**

A secret ensures that the received payload is the same as it is sent. When the payload is hacked, the secret will not match. You can [reveal ](revealing-a-webhooks-secret.md)and [rotate ](rotating-a-webhooks-secret.md)a webhook's secret.

## **Status**

The webhook status is disabled by default. The system will prompt you to enable the webhook when creating one. If you choose to disable the webhook, no payload will be sent when an event occurs.&#x20;

After you create a webhook, you can choose to [enable or disable the webhook manually](enabling-or-disabling-webhooks.md). Enabling a webhook manually does not require confirmation. However, you must provide confirmation when you manually disable a webhook by entering the username (case sensitive).
