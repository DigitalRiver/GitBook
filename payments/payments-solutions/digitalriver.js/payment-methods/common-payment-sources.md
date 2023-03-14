---
description: Learn about payment sources that are common to all payment methods.
---

# Common payment sources

## Payment source statuses

| Status            | Definition                                                                                                                                                   |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| pending\_redirect | The source requires further action before you can use it in a transaction. Redirect the customer to authorize the payment on the payment provider's website. |
| pending\_funds    | The source requires further action before you can use it in a transaction. Instruct the customer to push funds to the account specified on the source.       |
| chargeable        | The source can be used to create a charge.                                                                                                                   |
| consumed          | The source has been used to create a charge and is not reusable.                                                                                             |
| cancelled         | The source is no longer usable.                                                                                                                              |
| failed            | The source cannot be created.                                                                                                                                |

## Payment source types <a href="#payment-source-types" id="payment-source-types"></a>

| Type                                 | Identifier       |
| ------------------------------------ | ---------------- |
| Afterpay                             | afterPay         |
| Alipay                               | alipay           |
| Amazon Pay                           | amazonPay        |
| Apple Pay                            | applePay         |
| Bancontact                           | bancontact       |
| BLIK                                 | blik             |
| Boleto                               | boletoBancario   |
| Credit Card                          | creditCard       |
| Google Pay                           | googlepay        |
| Klarna                               | klarnaCredit     |
| Konbini                              | konbini          |
| Online banking (FXP)                 | fpxOnlineBanking |
| Online Banking (IBP)                 | onlineBanking    |
| Online Banking (Korea Bank Transfer) | bankTransfer     |
| PayCo                                | payco            |
| PayPal                               | payPal           |
| PayPal Billing Agreement             | payPalBilling    |
| PayPal Credit                        | payPalCredit     |
| SEPA Direct Debit                    | directDebit      |
| TreviPay                             | msts             |
| Trustly                              | trustly          |
| Wire Transfer                        | wireTransfer     |
