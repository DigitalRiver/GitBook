---
description: >-
  Understand when a shopper receives a subscription renewal reminder
  notification.
---

# Sending a subscription renewal reminder notification

This notification triggers when it's time to send a shopper an automatic, manual, or trial automatic, or trial manual renewal reminder for a subscription. The renewal reminder email will:

* Tell the shopper their subscription is about to expire.
* Instruct the shopper on how to renew their subscription. If the subscription uses automatic renewal, the renewal reminder email will tell the shopper when their renewal will take place.
* List the renewal price (not including tax and shipping, if applicable), and all renewals will respect the pricing quoted to the shopper.
* Contain other information about the renewal order as customized for your site.

The settings defined in the product determine when or how often the system sends the shopper a renewal reminder email.

{% hint style="success" %}
Set up all your subscription products to send reminder emails to ensure that the system charges the shopper the price listed in the reminder emails. See [Notifications](https://help.digitalriver.com/help/gc/Products/All-Products/Configuring-the-product-settings.htm?Highlight=Product%20Settings#Notifications) for more information.
{% endhint %}

Once the shopper renews the subscription, the system sends the shopper another email that contains the details of their renewal order. Assuming you configured your store to send that email.

See [Setting up subscription renewal reminders](setting-up-subscription-renewal-reminders.md) or [Setting up trial subscription renewal reminders](../../../general-resources/admin-apis-reference/subscriptions/setting-renew-reminders-for-trial-subscriptions.md) for instructions on configuring a subscription renewal reminder email.

## Notification triggers

* `SubscriptionNotificationTask`
* `RenewalReminderNotificationTask`
* `AutoRenewalReminderNotificationTask`
* `TrialReminderNotificationTask`
* `ManualRenewalReminderNotificationTask`
* `TrialManaulRenewalReminderNotificationTask`
