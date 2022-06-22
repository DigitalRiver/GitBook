---
description: Learn how to manage your events and webhooks.
---

# Events and webhooks

Digital River uses webhooks to notify your application (endpoint URL) when events occur in [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do). A webhook contains the event and timestamp for the event. You can use the Webhooks Service in Global Commerce to [search](webhooks/searching-for-a-webhook.md), [edit](webhooks/editing-a-webhook.md), [create](webhooks/creating-a-webhook.md), and [delete webhooks](webhooks/deleting-a-webhook.md).

When you register your webhook URLs with Digital River, Digital River creates a Data object and sends webhook events that notify your application any time an event occurs.&#x20;

The Data object includes the type of event and the data associated with that event. Digital River sends the Data object to the endpoint URLs you define in the [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do)'s Webhook Service settings for your account. You can set up multiple webhook endpoints to receive a single event.
