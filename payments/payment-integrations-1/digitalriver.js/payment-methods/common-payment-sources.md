---
description: Learn about payment sources that are common to all payment methods.
---

# Common payment sources

Choosing the right payment source in electronic transactions is crucial for facilitating smooth and secure payments. Payment sources, often called payment methods or instruments, are the backbone of any financial transaction, enabling the transfer of funds from a buyer to a seller. From traditional methods like bank transfers and credit cards to modern digital wallets and cryptocurrency, the diversity of payment sources caters to the varied preferences and requirements of consumers and businesses alike. This section delves into some of the most common payment source types, highlighting their unique features and use cases. Whether you're a merchant looking to expand your payment options or a customer seeking convenience and security, understanding these payment source types can help you make informed decisions in the evolving digital payment landscape.

## Payment source statuses

A payment status indicates the current state of a payment source, ranging from its initial creation to its potential use in a transaction. It encompasses various stages, such as requiring action from the customer or becoming unusable. Each status, such as `pending_redirect`, `chargeable`, or `cancelled`, provides specific information about the needed actions or the source's current capabilities.

| Status            | Definition                                                                                                                                                   |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| pending\_redirect | The source requires further action before you can use it in a transaction. Redirect the customer to authorize the payment on the payment provider's website. |
| pending\_funds    | The source requires further action before you can use it in a transaction. Instruct the customer to push funds to the account specified on the source.       |
| chargeable        | The source can be used to create a charge.                                                                                                                   |
| consumed          | The source has been used to create a charge and is not reusable.                                                                                             |
| cancelled         | The source is no longer usable.                                                                                                                              |
| failed            | The source cannot be created.                                                                                                                                |

## Payment source types <a href="#payment-source-types" id="payment-source-types"></a>

A payment source type refers to the method or instrument used for making a payment or transaction. This can vary widely, from traditional methods like credit cards and wire transfers to digital and mobile payment solutions such as Apple Pay, Google Pay, and PayPal. Each type has unique characteristics, requirements, and applicable regions, offering customers and merchants flexible transaction management options. Here's a list of some common payment source types:

| Type                                 | Identifier       |
| ------------------------------------ | ---------------- |
| Afterpay                             | afterPay         |
| Alipay (domestic)                    | alipay           |
| Alipay (cross-border)                | alipayCn         |
| Amazon Pay                           | amazonPay        |
| Apple Pay                            | applePay         |
| Bancontact                           | bancontact       |
| BLIK                                 | blik             |
| BNP Paribas                          | bnpParibas       |
| Clearpay                             | clearPay         |
| Credit Card                          | creditCard       |
| Google Pay                           | googlepay        |
| Klarna                               | klarnaCredit     |
| Konbini                              | konbini          |
| Online Banking (FPX)                 | fpxOnlineBanking |
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

Each payment source type is designed to suit different transaction scenarios, providing a framework that supports various payment methods to accommodate the diverse preferences of consumers globally.
