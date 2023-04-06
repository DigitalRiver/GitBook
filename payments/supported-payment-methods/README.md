---
description: >-
  Learn more about the payment methods supported by Drop-in Payments and
  DigitalRiver.js
---

# Supported payment methods

The following table lists the supported payment methods in [Drop-in payments](../payments-solutions/drop-in/) and [DigitalRiver.js with elements](../payments-solutions/digitalriver.js/). All of these payment methods can be used to make [non-recurring payments](../sources/#reusable-or-single-use). But only some of them support [recurring payments](../sources/#reusable-or-single-use).&#x20;

The table also lists each [payment method's flow](../sources/#payment-flow) and indicates whether that payment method is supported in our [test environment](broken-reference).

For a complete list of payment methods that can be paired with [store credit](../../shopper-apis/shopper-basics/common-use-cases/applying-store-credit.md), refer to [combining primary and secondary sources](../sources/using-the-source-identifier.md#combining-primary-and-secondary-payment-sources) on the [Managing sources](../sources/using-the-source-identifier.md) page.

| Payment method                                                                          | Drop-in Payments | DigitalRiver.js with Elements | Non-recurring payments | Recurring payments | Authentication flow |
| --------------------------------------------------------------------------------------- | :--------------: | :---------------------------: | :--------------------: | :----------------: | :-----------------: |
| [Afterpay](afterpay.md)                                                                 |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Alipay (domestic)](alipay-domestic.md)                                                 |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Alipay+ (cross-border)](alipay+-cross-border.md)                                       |         ✔        |               ✔               |            ✔           |          ✔         |      `redirect`     |
| [Apple Pay](apple-pay.md)                                                               |         ✔        |               ✔               |            ✔           |          -         |      `standard`     |
| [Amazon Pay](amazon-pay.md)                                                             |         -        |               ✔               |            ✔           |          ✔         |      `redirect`     |
| [Bancontact](bancontact.md)                                                             |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [BLIK](blik.md)                                                                         |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Boleto](boleto.md)                                                                     |         -        |               ✔               |            ✔           |          ✔         |      `redirect`     |
| [Clearpay](clearpay.md)                                                                 |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Credit Cards](credit-cards.md)                                                         |         ✔        |               ✔               |            ✔           |          ✔         |      `standard`     |
| [Google Pay](google-pay.md)                                                             |         ✔        |               ✔               |            ✔           |          ✔         |      `standard`     |
| [iDEAL](ideal.md)                                                                       |         ✔        |               ✔               |            ✔           |        ✔[^1]       |      `redirect`     |
| [Klarna](klarna.md)                                                                     |         ✔        |               ✔               |            ✔           |          ✔         |      `redirect`     |
| [Konbini](konbini.md)                                                                   |         ✔        |               ✔               |            ✔           |          -         |      `receiver`     |
| [Online Banking (FPX)](fpx-online-banking.md)                                           |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Online Banking (IBP)](online-banking-ibp.md)                                           |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Online Banking (Korea Bank Transfer)](korea-bank-transfer-online-banking.md)           |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [PayCo](payco.md)                                                                       |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [PayPal](paypal.md)                                                                     |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [PayPal Billing](paypal-billing-agreement.md)                                           |         ✔        |               ✔               |            ✔           |          ✔         |      `redirect`     |
| [PayPal Credit](paypal-credit.md)                                                       |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Pay in 3](paypal-pay-in-3.md)                                                          |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Pay in 4](paypal-pay-in-4.md)                                                          |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [PayPal RatenZahlung (Installment Payment)](paypal-ratenzahlung-installment-payment.md) |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [SEPA Direct Debit](sepa-direct-debit.md)                                               |         ✔        |               ✔               |            ✔           |          ✔         |      `redirect`     |
| [TreviPay](trevipay.md)                                                                 |         ✔        |               ✔               |            ✔           |          ✔         |      `redirect`     |
| [Trustly](trustly.md)                                                                   |         ✔        |               ✔               |            ✔           |          -         |      `redirect`     |
| [Wire Transfer](wire-transfer.md)                                                       |         ✔        |               ✔               |            ✔           |          -         |      `receiver`     |

[^1]: Digital River supports iDEAL for recurring with SEPA direct debit transactions.
