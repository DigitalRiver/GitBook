---
description: Understand why an expired credit card triggers a notification.
---

# Sending an expired credit card notification

This notification triggers before a shopper's credit card information associated with a subscription expires.

{% hint style="success" %}
If the credit card information expires, automatic subscription renewal will fail. The notification allows you to ask a shopper to update their credit card details before it expires, thereby increasing the card update and renewal success rate for a subscription.
{% endhint %}

<mark style="background-color:orange;">??? Explain</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`reasonCode`</mark><mark style="background-color:orange;">. Can someone provide information on the</mark> <mark style="background-color:orange;"></mark><mark style="background-color:orange;">`reasonCodes`</mark><mark style="background-color:orange;">? ????</mark>

## Notification trigger

The following classes trigger an expired credit card notification:

* `SubscriptionNotificationTask`
* `RenewalReminderNotificationTask`
* `AutoRenewalReminderNotificationTask`
* `TrialReminderNotificationTask`
* `ManualRenewalReminderNotificationTask`
* `TrialManaulRenewalReminderNotificationTask`
