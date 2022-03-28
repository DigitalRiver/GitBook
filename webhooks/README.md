---
description: Learn about the webhooks.
---

# Webhooks

Digital River uses webhooks to notify your application ([endpoint URL](./#endpoint-url)) when events occur. A webhook contains the event and timestamp for the event. You can use the Webhook Service page in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do) to [search](../events-and-webhooks/webhooks/searching-for-a-webhook.md), [create](../events-and-webhooks/webhooks/creating-a-webhook.md), [edit](../events-and-webhooks/webhooks/editing-a-webhook.md), [enable](enabling-or-disabling-webhooks.md), [disable](enabling-or-disabling-webhooks.md), and [delete ](../events-and-webhooks/webhooks/deleting-a-webhook.md)webhooks. You can also [reveal ](../events-and-webhooks/webhooks/revealing-a-webhooks-secret.md)and [rotate ](../events-and-webhooks/webhooks/rotating-a-webhooks-secret.md)webhook secrets. When you register your webhook URLs with Digital River, Digital River creates a Data object and sends webhook events that notify your application any time an event occurs. The Data object includes the type of event and the data associated with that event.&#x20;

## **Webhook ID**

Each webhook has a unique identifier (ID). If you know the webhook ID, you can [search ](../events-and-webhooks/webhooks/searching-for-a-webhook.md)for it from the Webhook Service page in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). A webhook ID only appears in the search results if it exactly matches the text that you type in the **Search** field.

## **Endpoint URL**

An endpoint URL is where the payload will be sent to when the subscribed event happens. The endpoint URL must begin with either `http://` or `https://`.

The endpoint must return a `2xx` HTTP status code to acknowledge the receipt of an event. If the endpoint fails to acknowledge events over several days, the endpoint will be disabled. If Digital River receives any response codes outside this range, it indicates that you did not receive the event. For example, Digital River treats a URL redirection as a failure.

## **Secret**

A secret ensures that the received payload is the same as it is sent. When the payload is hacked, the secret will not match. You can [reveal ](../events-and-webhooks/webhooks/revealing-a-webhooks-secret.md)and [rotate ](../events-and-webhooks/webhooks/rotating-a-webhooks-secret.md)a webhook's secret.

## **Status**

The webhook status is Disabled by default. The system will prompt you to enable the webhook when you [create a webhook](../events-and-webhooks/webhooks/creating-a-webhook.md). If you chose to disable the webhook, no payload would be sent when an event occurs.&#x20;

After you create a webhook, you can choose to [enable or disable the webhook manually](enabling-or-disabling-webhooks.md). Enabling a webhook manually does not require confirmation. However, you are required to provide confirmation when you manually disable a webhook by entering the username (case sensitive).
