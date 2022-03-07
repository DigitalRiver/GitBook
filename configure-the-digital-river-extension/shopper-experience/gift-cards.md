---
description: Learn how shoppers can use gift cards.
---

# Gift Cards

Shoppers can use one or more Magento Gift Cards to pay for all or part of an order processed by Digital River. They can use Gift Cards in combination with multiple [payment methods](https://docs.digitalriver.com/digital-river-api/checkouts-and-orders/payment-sources/using-the-source-identifier#combining-primary-and-secondary-payment-sources).

With Store Credit, when a shopper pays for an order using a combination of Gift Card and one of the other supported payment methods, the DR **Payment Method** will be the non-Gift Card payment instrument (for example, PayPal). When the shopper pays an order entirely with a Gift Card, the **DR Payment Method** will be **CustomerCredit**.

![](<../../.gitbook/assets/Gift Cards (1).png>)

## Refunding orders paid with Gift Cards

You can process refunds for orders paid partially or entirely with Gift Cards through the normal Magento admin screens.

If a shopper used Gift Cards to partially pay for a transaction and used a standard payment method to pay for the remainder of that transaction, Digital River will always refund the standard payment method first up to the amount paid using that payment method on the original purchase. Digital River will then refund any additional amounts to the Gift Card, up to the amount paid with a Gift Card on the original purchase as store credit.

**Note**: Digital River will never refund more to any payment instrument than what was originally paid using that payment instrument on the original purchase.

![](<../../.gitbook/assets/Refunding orders with Gift Card (1).png>)
