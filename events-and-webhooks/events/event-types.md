---
description: Understand the event types supported by Digital River.
---

# Event types

Every event type uses the following format: `resource.event`. This makes coding easier since you know all event types use a consistent format. Digital River supports the following event types:

| Event Type                   | Description                                                                                                                |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `subscription.created`       | Occurs whenever a subscription is created.                                                                                 |
| `subscription.renewed`       | Occurs whenever a subscription is renewed.                                                                                 |
| `subscription.auto_reminder` | Occurs whenever a subscription reaches a point in the subscription cycle that satisfies the product level reminder setup.  |

In [Global Commerce](https://gc.digitalriver.com/gc/ent/login.do), when you [create a webhook](../webhooks/creating-a-webhook.md) or [view the details of an existing webhook](../webhooks/searching-for-a-webhook.md), you can find the latest list of event types supported in the Commerce API.

## Subscription created

{% hint style="info" %}
**Event trigger**: When a customer purchases a new subscription.
{% endhint %}

During the shopping experience, a customer orders a subscription to one of your products. They may order a trial subscription or a purchased subscription.

If you [created a webhook](../webhooks/creating-a-webhook.md) using the `subscription.created` event for your application (endpoint URL), Digital River notifies your application when a successful subscription acquisition event occurs.

## Subscription renewal

{% hint style="info" %}
**Event trigger**: When an existing subscription renews (either auto or manual).
{% endhint %}

At the end of a subscription period, the shopper must renew the subscription for continued access to the product. A shopper can accomplish a renewal in two ways:

* **Automatic Renewal (Auto Renew)**–The shopper provides a payment method that the system automatically debits a specified number of days before the subscription expiration date. If the renewal fails because the billing information is not correct (for example, an expired credit card) shoppers are notified and given a chance to update their billing information. Digital River will attempt to bill a shopper for automatic renewals several times. After which Digital River will cancel the subscription and list the billing attempt as failed.
* **Manual Renewal**–The shopper receives emails at preconfigured time intervals before the expiration date that asks the shopper to complete a renewal transaction. The shopper has to renew the subscription manually. The customer can choose one of the following options to renew their product:
  * Log in to their My Account portal and renew using the features available in the self-service options.
  * Call Customer Service to renew the subscription.

In either case, the system renews the subscription when the payment is complete.

If you [created a webhook](../webhooks/creating-a-webhook.md) using the `subscription.renewed` event for your application (endpoint URL), Digital River notifies your application when a successful subscription renewal event occurs.

## Subscription auto reminder

{% hint style="info" %}
**Event trigger**: When an existing subscription nears the end of its subscription cycle.
{% endhint %}

Digital River sends an automatic renewal reminder when a subscription nears the end of its subscription cycle.&#x20;

If you [created a webhook](../webhooks/creating-a-webhook.md) using the `subscription.auto_reminder` event for your application (endpoint URL), Digital River notifies your application when a subscription nears the end of its subscription cycle.
