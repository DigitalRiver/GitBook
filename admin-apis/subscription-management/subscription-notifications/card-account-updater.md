---
description: Understand how the Card Account Updater works.
---

# Card Account Updater

Outdated credit card information, such as an expired credit card, is one of the most frequent causes of renewal failure among auto-renewing subscriptions. To reduce customer churn, Digital River uses Card Account Updater. The Card Account Updater is an automated script that checks all cards on file for active subscriptions with partnering banks regularly. It returns information that notifies you when there are changes to the shopper's card, such as a new card number (that we will use to replace the old one on file) or expiry date for the same customer.

The Card Account Updater checks Visa, Mastercard, Discover, and American Express cards before the first scheduled billing attempt, as well as after each payment failure. Card updates are processed automatically. Clients using Digital River’s subscription management platform do not need to do anything to take advantage of this service.

The partnering bank will not provide updated payment information when a card is stolen or lost, or the account is deactivated. The partnering bank returns a "Contact the Customer" message for stolen or lost cards and an “Account Closed” message for deactivated accounts.

### **How the Card Account Updater works**

1. The Renewal Job Manager initiates the process for the Card Account Updater request when the subscription renewal fails on or after its expiration date. The request will create a pending "account update" transaction for later processing.
   * When the site configuration attribute is enabled, the system issues the request when you enable the site configuration attribute.
   * When the site configuration attribute is disabled, the system does not issue the Card Account Updater request. \
     \
     Contact your Digital River representative if you want to enable or disable this attribute.&#x20;
2. A Batch Job Manager picks up all pending transactions.
3. The Submission Job Manager submits batched transactions to the payment processor.
4. The payment processor processes the batched transactions.
5. The Reconciliation Manager checks the Card Account Updater results.

{% hint style="info" %}
The grace date will never be less than five days. This allows the Card Account Updater request to process in due time.
{% endhint %}
