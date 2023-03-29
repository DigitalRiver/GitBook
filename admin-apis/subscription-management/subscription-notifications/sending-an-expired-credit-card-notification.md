---
description: Understand why an expired credit card triggers a notification.
---

# Sending an expired credit card notification

This notification triggers before a shopper's credit card information associated with a subscription expires.

{% hint style="success" %}
If the credit card information expires, automatic subscription renewal will fail. The notification allows you to ask a shopper to update their credit card details before it expires, thereby increasing the card update and renewal success rate for a subscription.
{% endhint %}

If a credit card transaction fails, see [Credit card error and declined information](../../../common-shopper-and-admin-apis/error-codes/error-format-for-shopper-apis/credit-card-error-and-declined-messages.md) for more information.&#x20;

## Notification trigger

The following classes trigger an expired credit card notification:

* `SubscriptionNotificationTask`
* `RenewalReminderNotificationTask`
* `AutoRenewalReminderNotificationTask`
* `TrialReminderNotificationTask`
* `ManualRenewalReminderNotificationTask`
* `TrialManaulRenewalReminderNotificationTask`
