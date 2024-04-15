---
description: Learn how to manage your webhooks.
---

# Webhooks

Digital River uses webhooks to notify your application (endpoint URL) when events occur. A webhook contains the event and timestamp for the event. You can use the Webhooks section to view, edit, create, and delete webhooks.\


<figure><img src="../../../../.gitbook/assets/1 Webhooks.png" alt=""><figcaption></figcaption></figure>

When you register your webhook URLs with Digital River, Digital River creates an [Event ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)object and sends webhook events that notify your application any time an event occurs. You can also assign the webhook to a specific API version.

The [Event ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)object includes the type of event and the data associated with that event. Digital River sends the [Event ](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Events)object to the endpoint URLs you define in the [Digital River Dashboard](https://dashboard.digitalriver.com)'s Webhooks settings for your account through an HTTP POST request. You can set up multiple webhook endpoints to receive a single event.

The [Event logs](../event-logs/) list webhook events where you can drill down to the event details.
