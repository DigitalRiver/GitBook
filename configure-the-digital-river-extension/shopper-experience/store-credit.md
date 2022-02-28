---
description: Learn how shoppers can use store credit.
---

# Store credit

{% hint style="info" %}
**Note:** Store credit is only available in the Adobe Commerce edition.
{% endhint %}

Shoppers can use Magento Store Credit to pay for all or part of an order processed by Digital River. Store Credit can be used in combination with multiple [payment methods](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/payment-sources/using-the-source-identifier#combining-primary-and-secondary-payment-sources).&#x20;

For orders paid with a combination of Store Credit and one of the other supported payment methods, the **DR Payment Method** will be listed as the non-Store Credit payment instrument (for example,  PayPal). For orders paid entirely with Store Credit, the **DR Payment Method** will be **CustomerCredit**.

![](<../../.gitbook/assets/Store Credit (1).png>)

## Refunding orders paid with Store Credit

Orders paid partially or entirely with Store Credit can be refunded through the normal Magento admin screens.&#x20;

If a shopper pays part of the transaction with Store Credit and the other part with their chosen payment method, Digital River will always refund the payment method first.&#x20;

{% hint style="info" %}
**Note**: Digital River will never refund more than what the shopper paid using any payment method for the original purchase.
{% endhint %}

![](<../../.gitbook/assets/Refund order paid\_Store Credit (1).png>)

## Refunding to Store Credit when the shopper paid using another payment method

When a shopper pays an order without Store Credit on the initial transaction, refunding to the shopper’s store credit account must be done per _Digital River’s Guidelines and Best Practices._

The **Magento Credit Memo** page only allows refunds to the original payment methods used on the original purchase.

You can return Store Credit to the shopper’s account by adding it directly to their account from the Customer’s Admin page in the Magento Admin UI.

![](<../../.gitbook/assets/Refunding to store credit (1).png>)
